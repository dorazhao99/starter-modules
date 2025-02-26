# LLooM Documentation
|  Key | Value|
| ------------- | ------------- |
| Description | Documentation for the LlooM Python Package |


# Get Started <Badge type="tip" text="^0.8.0" />

LLooM is currently designed as a Python package for computational notebooks. Follow the instructions on this page to get started with LLooM Workbench on your dataset. We suggest starting with this [**template Colab Notebook**](https://colab.research.google.com/github/michelle123lam/lloom/blob/main/docs/public/nb/24_11_LLooM_GettingStartedTemplate_v1.ipynb).

<a target="_blank" href="https://colab.research.google.com/github/michelle123lam/lloom/blob/main/docs/public/nb/24_11_LLooM_GettingStartedTemplate_v1.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

### 1: Installation
First, install the LLooM Python package, available on PyPI as [`text_lloom`](https://pypi.org/project/text_lloom/). We recommend setting up a virtual environment with [venv](https://docs.python.org/3/library/venv.html#creating-virtual-environments) or [conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands).
```
pip install text_lloom
```

Now, you can use the LLooM package in a computational notebook! Create your notebook (i.e., with [JupyterLab](https://jupyterlab.readthedocs.io/en/latest/)) and then you can import the LLooM package:

```py
import text_lloom.workbench as wb
```

### 2a: Quick LLooM instance (OpenAI defaults)
By default, LLooM uses the **OpenAI API** under the hood to support its core operators (using GPT-4o mini and GPT-4o). If you use this default setting, you first need to locally set the `OPENAI_API_KEY` environment variable to use your own account.
```py
import os
os.environ["OPENAI_API_KEY"] = "sk-YOUR-KEY-HERE"
```

::: tip
LLooM provides (1) **cost estimation functions** that automatically run before operations that make calls to the OpenAI API and (2) **cost summary functions** to review tracked usage, but we encourage you to monitor usage on your account as always.
:::

After loading your data as a Pandas DataFrame, **create a new LLooM instance**. You will need to specify the name of the column that contains your input text documents (`text_col`). The ID column (`id_col`) is optional.
```py
l = wb.lloom(
    df=df,
    text_col="your_doc_text_col",
    id_col="your_doc_id_col",  # Optional
    # By default, when not specified, uses the following models:
    # - distill_model: gpt-4o-mini
    # - cluster_model: text-embedding-3-large
    # - synth_model: gpt-4o
    # - score_model: gpt-4o-mini
)
```

### 2b: Custom LLooM instance
Alternatively, users can specify **other LLMs** to support the LLooM operators, including:
1. **Different OpenAI models** (e.g., swapping in `gpt-4` for the Synthesis operator)
2. **Alternative LLM providers** (e.g., Gemini, Claude)
3. **Open source** models (e.g., Llama, Mistral)

Please visit the [Custom Models](./custom-models.md) page for information about these custom setups along with sample notebooks.
The custom LLM setup also allows users to specify custom rate limits for each operator.


### 3: Concept generation
Next, you can go ahead and start the concept induction process by generating concepts. The **seed term** can steer concept induction towards more specific areas of interest (e.g., social issues" for political discussion or "evaluation methods" for academic papers). You can omit the `seed` parameter if you do not want to use a seed.
```py
await l.gen(
    seed="your_optional_seed_term",  # Optional
)
```

We also provide a one-function **"auto" mode** that grants less control over the process, but simplifies the concept generation and scoring process into a single function. If you use the `gen_auto` function, you do not need to run concept scoring, but can directly proceed to visualize the results.
```py
score_df = await l.gen_auto(
    max_concepts=5,
    seed="your_optional_seed_term",  # Optional
)
```

### 4: Concept scoring
#### Review concepts
Review the generated concepts and select concepts to inspect further:
```py
l.select()
```

In the output, each box contains the concept name, concept inclusion criteria, and representative example(s).
![LLooM select() function output](/media/ui/select_output.png)

#### Score concepts
Then, apply these concepts to the full dataset with `score()`. This function will score all documents with respect to each concept to indicate the extent to which the document matches the concept inclusion criteria.
```py
score_df = await l.score()
```

### 5: Visualization
Now, you can visualize the results in the main LLooM Workbench view. An interactive widget will appear when you run this function:
```py
l.vis()
```
Check out [Using the LLooM Workbench](./vis-guide.md) for a more detailed guide on the visualization components.
![LLooM vis() function output](/media/ui/vis_output.png)

#### Add slices (columns)
If you want to additionally slice your data according to a pre-existing metadata column in your dataframe, you can optionally provide a `slice_col`. Numeric or string columns are supported. Currently, numeric columns are automatically binned into quantiles, and string columns are treated as categorical variables.
```py
l.vis(slice_col="n_likes")
```
Optional parameters for slices:
- `max_slice_bins`: For numeric columns, the maximum number of bins to create (default=5)
- `slice_bounds`: For numeric columns, the manual bin boundaries to use (ex: [0, 10, 50, 100])

#### Normalize counts
By default, the concept matrix shows the raw document counts. You can normalize by **concept**, meaning that the size of the circles in each concept row represents the fraction of examples *in that concept* that fall into each slice column. 
```py
l.vis(slice_col="n_likes", norm_by="concept")
```

You can also normalize by **slice** so that the size of circles in each slice column represents the fraction of examples *in that slice* that fall into each concept row.
```py
l.vis(slice_col="n_likes", norm_by="slice")
```
![LLooM vis() function output with slices](/media/ui/vis_output_slice.png)

### Manual concepts
You may also manually add your own **custom concepts** by providing a name and prompt. This will automatically score the data by that concept.
```py
await l.add(
    # Your new concept name
    name="Government Critique",
    # Your new concept prompt
    prompt="Does this text criticize government actions or policies?", 
)
```
Then, re-run the `vis()` function to see the new concept results.

### Saving and exporting

#### Submit your results
::: tip 🖼️ ✨ Submit your work for a chance to be featured!
If you'd like to share what you've done with LLooM or would like your work featured in a gallery of results, please submit your LLooM instance with the `submit()` function! If your submission is selected, we'll reach out to you to follow up and hear more about your work with LLooM.
:::
To submit your results, you just need to run the following function:
```py
l.submit()
```
You will be prompted to provide a few more details: 
- **Email address**: Please provide an email address so that we can contact you if your work is selected.
- **Analysis goal**: Share as much detail as you'd like about your analysis: What data were you using? What questions were you trying to answer? What did you find?

#### Save LLooM instance
You can save your LLooM instance to a pickle file to reload at a later point.
```py
l.save(folder="your/path/here", file_name="your_file_name")
```

You can then reload the LLooM instance by opening the pickle file:
```py
import pickle
with open("your/path/here/your_file_name.pkl", "rb") as f:
    l = pickle.load(f)
```

#### Export results
Export a summary of the results in Pandas Dataframe form. 
```py
export_df = l.export_df()
```
The dataframe will include the following columns:
- `concept`: The concept name
- `criteria`: The concept inclusion criteria
- `summary`: A generated summary of the examples that matched this concept
- `rep_examples`: A few representative examples for the concept from the concept generation phase
- `prevalence`: The proportion of documents in the dataset that matched this concept
- `n_matches`: The number of documents in the dataset that matched this concept
- `highlights`: An illustrative sample of n=3 highlighted quotes from documents that matched the concept that were relevant to the concept

### Cost tracking
LLooM provides cost estimation functions as well as cost summary functions to review usage.

#### estimate_gen_cost
`l.estimate_gen_cost(params=None, verbose=False)`

Estimates the cost of running `gen()` with the given parameters. If no parameters are provided, the function uses auto-suggested parameters. The function is automatically run within calls to `gen()` for the user to review before proceeding with concept generation.

#### estimate_score_cost
`l.estimate_score_cost(n_concepts=None, verbose=False)`

Estimates the cost of running `score()` on the provided number of concepts. If `n_concepts` is not specified, the function uses the current number of active (selected) concepts. The function is automatically run within calls to `score()` for the user to review before proceeding with concept scoring.

#### summary
`l.summary(verbose=True)`

Displays a **cumulative** summary of the (1) Total time, (2) Total cost, and (3) Tokens for the entire LLooM instance. 
- Total time: Displays the total time required for each operator. Each tuple contains the operator name and the timestamp at which the operation completed. 
- Total cost: Displays the calculated cost incurred by each operator (in US Dollars).
- Tokens: Displays the overall number of tokens used (total, in, and out)

Sample output:
```
Total time: 25.31 sec (0.42 min)
	('distill_filter', '2024-03-08-02-45-20'): 3.13 sec
	('distill_summarize', '2024-03-08-02-45-21'): 1.80 sec
	('cluster', '2024-03-08-02-45-25'): 4.00 sec
	('synthesize', '2024-03-08-02-45-42'): 16.38 sec


Total cost: $0.14
	('distill_filter', '2024-03-08-02-45-20'): $0.02
	('distill_summarize', '2024-03-08-02-45-21'): $0.02
	('synthesize', '2024-03-08-02-45-42'): $0.10


Tokens: total=67045, in=55565, out=11480
```

### Rate limits
Depending on the volume of data you are analyzing and the details of your OpenAI account/organization, you may run into OpenAI API [rate limits](https://platform.openai.com/docs/guides/rate-limits) (with respect to tokens per minute (TPM) or requests per minute (RPM)). LLooM provides several avenues to address rate limits.

#### Modifying underlying models
By default, LLooM currently uses `gpt-4o-mini` for the Distill and Score operators, `gpt-4o` for the Synthesize operator, and `text-embedding-3-large` for the Cluster operator. These values are set in [`workbench.py`](https://github.com/michelle123lam/lloom/blob/main/text_lloom/src/text_lloom/workbench.py). However, users can specify different models for each of these operators within the LLooM instance. See the [Custom Models](./custom-models.md) page for examples with other OpenAI models, other LLM APIs, and open source models.

#### Customizing wait times
LLooM has built-in functionality for batching asynchronous requests to avoid rate limit issues. However, the necessary batch size and timing may vary across different users depending on details of their dataset and account. 

With the [Custom Models](./custom-models.html#different-rate-limits) option, users can override the **number of requests in a batch** and the **length of time to wait** between batches with the `rate_limit` parameter. 

The current defaults are defined using the `rate_limit` field in `MODEL_INFO` in [`llm_openai.py`](https://github.com/michelle123lam/lloom/blob/main/text_lloom/src/text_lloom/llm_openai.py). For OpenAI models, it may be helpful to refer to your organization's own [rate limits](https://platform.openai.com/account/limits) to set these values.

#### Batching score operations
The `Score` operator in particular may run into rate limits because it initiates a higher volume of concurrent requests to score all documents for all selected concepts. By default, scoring is applied _individually_ for each concept and each document (`batch_size=1`) to produce more reliable scores. 

However, users can opt to increase the batch size, which will score multiple documents at a time for a given concept. This will reduce the number of unique API calls, but may sacrifice scoring reliability.

```py
score_df = await l.score(
    batch_size=5,
)
```


### LLooM Operators
If you'd like to dive deeper and reconfigure the core operators used within LLooM (like the `Distill`, `Cluster`, and `Synthesize` operators), you can access the base functions from the `concept_induction` module:

```
import text_lloom.concept_induction as ci
```

Please refer to the [API Reference](../api/operators) for details on each of the core LLooM operators.

# Using the LLooM Workbench

The LLooM Workbench visualization consists of several components. Here, we'll walk through in a bit more detail on how to work with this interactive visualization.

![LLooM Workbench UI](/media/lloom_workbench_ui.png)

### A: Concept Overview
The Concept Overview chart is at the top of the LLooM Workbench visualization. This chart is intended to provide a high-level summary of concepts observed in the dataset. The x-axis displays all concepts (including the Outlier set), and the y-axis plots the number of documents that matched the concept. 

<img src="/media/ui/vis_guide_overview.png" width="70%" alt="LLooM Concept Overview chart">

### B: Concept Matrix
The Concept Matrix is below the Concept Overview and comprises the majority of the LLooM Workbench visualization. The left side is the Matrix view, which displays **concepts as rows** and **slices as columns**. The right side will display Detail views: clicking on a concept row header will open the corresponding **Concept Detail view**, and clicking on a slice column header will open the corresponding **Slice Detail view**.

#### Circle size
The circles at the intersection of each concept and slice indicate the _number of documents_ in that concept and slice: a larger circle indicates a higher number of docs, and a smaller circle indicates a lower number of docs. 

#### Circle normalization
Since there are different numbers of documents within each concept and slice, absolute document counts aren't always helpful. We can optionally _normalize_ the circle size either by concept or by slice.
- **`norm_by="concept"`**: (**norm by row**) The size of the circles in each _concept row_ represents the fraction of examples _in that concept_ that fall into each slice column. 
    ::: tip When to use CONCEPT normalization
    * Helpful if we want to see patterns _within_ a concept and _across_ slices. 
    * Example: If we wanted to see how a paper topic like "Artificial Intelligence" (concept) changes over decades (slices), concept normalization could let us see more clearly how the relative fraction of papers changes between each decade.
    :::

<div>
    <img class="img-center" src="/media/ui/vis_guide_matrix.png" width="70%" alt="LLooM Concept Matrix, Concept normalization">
    <p class="caption"><b>Concept normalization helps us see patterns within a concept row</b>: This matrix has slices based on a word-count field. For documents matching the "Robustness & Security" concept, most had 100-500 words (second column from the right). We see a similar pattern looking at each of the other concept rows.</p>
</div>

- **`norm_by="slice"`**: (**norm by column**) The size of the circles in each _slice column_ represents the fraction of examples _in that slice_ that match each concept row.
    ::: tip When to use SLICE normalization
    * Helpful if we want to see patterns _within_ a slice and _across_ concepts.
    * Example: If we wanted to see what attributes of social media posts (concepts) are correlated with the highest toxicity rating (slice), slice normalization could let us better see which concepts match the highest fraction of these highest-toxicity posts.
    :::
<div>
    <img class="img-center" src="/media/ui/vis_guide_matrix_sliceNorm.png" width="70%" alt="LLooM Concept Matrix, Slice normalization">
    <p class="caption"><b>Slice normalization helps us see patterns within a slice column</b>: For the slice of 500-1000-word statements (far right column), "Ethical Considerations" were far more prevalent than other concepts. For the 100-500-word bin, "Robustness & Security" and "Ethical Considerations" were most common.</p>
</div>

### C: Detail Views
#### Concept Detail view
Clicking on a concept row header opens its Concept Detail view. This view contains three cards: 
- **C1: Concept details**: This card provides key information about the concept including the inclusion criteria, summary, representative examples, and the number of matching documents.
- **C2: Potential concept matches**: This table displays a summary of documents that matched the concept, where each row represents one document. It includes the following columns:
    * `concept score`: The 0-1 score assigned to the document. By default, only documents with a score of 1 will appear as matches here.
    * `text`: The full document text. If the model has identified spans of relevant text for the concept, they will be highlighted in blue.
    * `text bullets`: Bulleted summaries of the document text.
    * `score rationale`: The LLM's rationale for providing the given concept score.
    * `<slice column>`: The slice column values if `slice_col` was specified.
    ::: tip
    Click on the header for a column in the table to sort by that column.
    :::
- **C2: Concept non-matches**: This table displays all documents that did _not_ match the concept, with the same columns as the concept match table above.

#### Slice Detail view
Similarly, clicking on a slice column header opens its Slice Detail view. This view contains two cards:
- **C1: Slice details**: This card provides key information about the slice including the name and the number of documents in the dataset matching the slice.
- **C2: Slice examples**: This table displays all documents in the slice, where each row again represents one document. The table includes the following columns:
    * `text`: The full document text.
    * `<concept name>`: The score for the concept with the indicated name. There will be a column for each concept.
    * `<slice column>`: The slice column values.

### Key terms
Here we provide a brief reference on terms used throughout the LLooM Workbench.

::: info CONCEPT GENERATION
- **Concept**: A natural language description of an emergent theme, trend, or pattern in text.
    - **Criteria**: The explicit inclusion criteria used to determine whether a given document matches a concept.
    - **Summary**: A summary of the documents that matched the concept.
    - **Representative examples**: A sample of quotes from input documents that were used to generate the concept.
- **Seed**: A word or phrase to steer the direction of concept generation. LLooM uses the provided seed term to condition the Distill and Synthesize operators to pay attention to a particular aspect of the data. Ex: "social issues" for a political dataset or "evaluation methods" for an academic papers dataset.
:::

::: info CONCEPT SCORING
- **Concept score**: The estimated likelihood that a document matches the given concept, from 0 (lowest likelihood) to 1 (highest likelihood).
- **Concept matches**: Documents that matched a concept, by default operationalized as those that received the highest concept score of 1.
:::

::: info VISUALIZATION
- **Slice**: A user-specified data grouping based on additional columns in the input dataframe. LLooM automatically creates groups for strings (as categorical variables) or numbers (as binned continuous variables).
- **Outlier**: Any input document that does not match _any_ of the active concepts.
:::


<style>
    .img-center {
        text-align: center;
        margin: auto;
    }

    .caption {
        font-size: 12px; 
        font-style: italic; 
        text-align: center;
        line-height: normal !important;
        margin-bottom: 30px !important;
    }
</style>

# Custom Models

LLooM supports custom models to serve the Distill, Cluster, Synthesize, and Score operators, including (1) [different OpenAI models](./custom-models#different-openai-models), (2) [alternative LLM APIs](./custom-models#alternative-llm-apis) (e.g., Gemini), and (3) [open source models](./custom-models#open-source-models) (e.g., Llama). 

In all of these cases, users provide their own model specification when **creating their LLooM instance** (optionally with a short API-specific function implementation). All other steps remain the same as shown on the [Getting Started](./get-started.md) page.

### Different OpenAI Models
See our example [Colab notebook](https://colab.research.google.com/drive/1GKk7my5QA8rs7V4pi-WP0vJIvBYEkPnZ?usp=sharing) or follow these steps to specify different OpenAI models for the LLooM operators. 

First, import our helper classes for the OpenAI models:
```py
from text_lloom.llm import OpenAIModel, OpenAIEmbedModel
```

Then, prep your OpenAI API key to provide in your model spec:
```py
openai_key = "sk-YOUR-KEY-HERE"
```

Then, specify the desired model name and API key for as many operators as you would like (among `distill_model`, `cluster_model`, `synth_model`, and `score_model`). If any of these are excluded, the system will use the default settings, as described on the Getting Started page.

```py {5-30}
l = wb.lloom(
    df=df,
    id_col="doc_id",
    text_col="text",
    # Example custom OpenAI model spec  
    distill_model=OpenAIModel(  
        name="gpt-4o-mini",  
        api_key=openai_key,  
    ),  
    cluster_model=OpenAIEmbedModel(  
        name="text-embedding-3-large",  
        api_key=openai_key,  
    ),  
    synth_model=OpenAIModel(  
        name="gpt-4o",  
        api_key=openai_key,  
    ),  
    score_model=OpenAIModel(  
        name="gpt-4o-mini",  
        api_key=openai_key,  
    ),  
)
```

### Different rate limits
Beyond specifying different model names, you can also modify your desired **rate limit** based on dataset size and API limits. This parameter is set to a tuple `(n_requests, wait_time_secs)`:
- `n_requests`: Number of requests allowed in one batch.
- `wait_time_secs`: Time period (in seconds) to wait after a batch before making more requests.

This means that RPM (requests per minute) = `n_requests * (60 / wait_time_secs)`. For example, a rate limit tuple of `(40, 10)` specifies 40 requests every 10 seconds, which means 240 requests per minute.

You may also modify information about the context window and cost if these parameters become out of date.

```py
l = wb.lloom(
    df=df,
    id_col="doc_id",
    text_col="text",
    # Example custom OpenAI model spec
    distill_model=OpenAIModel(
        name="gpt-4o-mini",
        api_key=openai_key,
        context_window=128_000, # <n_tokens>  # [!code ++]
        cost=(0.15 / 1_000_000, 0.6 / 1_000_000), # (input_cost, output_cost)  # [!code ++]
        rate_limit=(300, 10), # (n_requests, wait_time_secs)  # [!code ++]
    ),
    cluster_model=OpenAIEmbedModel(
        name="text-embedding-3-large",
        api_key=openai_key,
    ),
    synth_model=OpenAIModel(
        name="gpt-4o",
        api_key=openai_key,
        context_window=128_000, # <n_tokens>  # [!code ++]
        cost=(2.5 / 1_000_000, 10 / 1_000_000), # (input_cost, output_cost) # [!code ++]
        rate_limit=(20, 10), # (n_requests, wait_time_secs)  # [!code ++]
    ),
    score_model=OpenAIModel(
        name="gpt-4o-mini",
        api_key=openai_key,
        context_window=128_000, # <n_tokens>  # [!code ++]
        cost=(0.15/1_000_000, 0.6/1_000_000), # (input_cost, output_cost) # [!code ++]
        rate_limit=(300, 10), # (n_requests, wait_time_secs)  # [!code ++]
    ),
)
```

### Alternative LLM APIs
See our example [Colab notebook](https://colab.research.google.com/drive/1uY1JcLA_3Bu7C34Pb9S_qLtbADIDjc5j?usp=sharing) to follow along on how to incorporate different LLM APIs to serve LLooM operators.

First, import our helper classes for custom models:
```py
from text_lloom.llm import Model, EmbedModel
```

Then, the key difference for non-OpenAI APIs is that, for new models, you must implement two functions to (1) perform any necessary API **setup** operations and (2) to **call** the provided API and process its outputs. We will demonstrate these using the Gemini API.

#### Setup functions
A **setup** function takes an `api_key` as a parameter and is expected to return a `client` object, which is required for many LLM APIs and is used in the **call** functions. If the API does not use a client, this can be set as `None`. The function should perform any imports or initializations that are needed for the API to work properly.

###### Ex: Setup functions for Gemini
```py
# Setup for **LLM** API
# (relevant for Distill, Synthesize, Score operators)
def setup_llm_fn(api_key):
    import google.generativeai as genai  # Import package
    genai.configure(api_key=api_key)  # Set API key
    llm_client = None  # No client, so set to None
    return llm_client

# Setup for **Text Embedding** API
# (relevant for Cluster operator)
def setup_embed_fn(api_key):
    import google.generativeai as genai  # Import package
    genai.configure(api_key=api_key)  # Set API key
    embed_client = None  # No client, so set to None
    return embed_client
```

#### Call function (LLM API)
A **call** function for an **LLM API** is an `async` function that takes in two arguments: 
- `model`: An instance of LLooM's custom `Model` object, which stores the specified model name, the API client, and other necessary parameters.
- `prompt`: The LLM prompt.

The function is expected to return two things:
- `text`: The LLM text response to the provided prompt.
- `tokens`: A `(in_tokens, out_tokens)` tuple of the tokens used to respond to this request. If not provided by the API, this can be set to `(0, 0)`, but this will prevent the system from accurately accounting for the token usage in cost tracking functions.

###### Ex: Call function for Gemini LLM API
```py
async def call_llm_fn(model, prompt):
    # Retrieve model response
    from google.generativeai.types import HarmCategory, HarmBlockThreshold
    model = genai.GenerativeModel(model.name)
    response = model.generate_content(prompt)
    text_result = response.text

    # Retrieve token usage
    in_tokens = response.usage_metadata.prompt_token_count
    out_tokens = response.usage_metadata.total_token_count
    tokens = (in_tokens, out_tokens)

    return response.text, tokens
```

#### Call function (Text Embedding API)
Similarly, a **call** function for a **Text Embedding API** takes in two arguments: 
- `model`: An instance of LLooM's custom `EmbedModel` object, which stores the specified model name, the API client, and other necessary parameters.
- `text`: The text input for embedding retrieval.

The function is expected to return two things:
- `embedding`: The generated embedding for the provided text.
- `tokens`: A `(in_tokens, out_tokens)` tuple of the tokens used to respond to this request. Again, if not provided by the API, this can be set to `(0, 0)`.

###### Ex: Call function for Gemini Text Embedding API
```py
def call_embed_fn(model, text):
    task_type = "clustering"
    result = genai.embed_content(
        model=model.name,
        content=text,
        task_type=task_type,
    )
    tokens = [0, 0]
    return result['embedding'], tokens
```

#### Custom LLooM Instance
Putting these together, we can now write a model specification to create a LLooM instance. The setup and call functions can be written once and reused for *any* instance that uses the same LLM API.

###### Ex: Gemini LLooM instance
```py {5-25}
l = wb.lloom(
    df=df,
    id_col="doc_id",
    text_col="text",
    # Example custom LLM API model spec
    distill_model=Model(
        setup_fn=setup_llm_fn,
        fn=call_llm_fn,
        name="gemini-1.5-flash", cost=[0.0005/1000, 0.0015/1000], rate_limit=(300, 10), context_window=16385, api_key=api_key
    ),
    cluster_model=EmbedModel(
        setup_fn=setup_embed_fn,
        fn=call_embed_fn,
        name="models/embedding-001", cost=(0.00013/1000), batch_size=2048, api_key=api_key
    ),
    synth_model=Model(
        setup_fn=setup_llm_fn,
        fn=call_llm_fn,
        name="gemini-1.5-flash", cost=[0.01/1000, 0.03/1000], rate_limit=(20, 10), context_window=128000, api_key=api_key
    ),
    score_model=Model(
        setup_fn=setup_llm_fn,
        fn=call_llm_fn,
        name="gemini-1.5-flash", cost=[0.0005/1000, 0.0015/1000], rate_limit=(300, 10), context_window=16385, api_key=api_key
    ),
)
```

### Open Source Models 
We can use the same approach generated above in the **Alternative LLM APIs** section to support open source models with the help of [vLLM](https://github.com/vllm-project/vllm).

This setup requires a GPU to host the open source model. First, follow the steps to set up vLLM on this machine and start the local vLLM API server (see [vLLM documentation](https://docs.vllm.ai/en/latest/)). After this, you can implement the [setup functions](./custom-models#setup-functions) and [call functions](./custom-models#call-function-llm-api) for your models and create a custom LLooM instance using the same method shown in the last section.

#### Ex: Llama & Sentence Transformers
In this example, we will use `Meta-Llama-3-8B-Instruct` for our LLM. Start the local vLLM API server (for example, on `localhost:8000`):
```bash
python -m vllm.entrypoints.openai.api_server --model meta-llama/Meta-Llama-3-8B-Instruct --download-dir <path_to_your_hfcache_dir_here>
```

From a notebook, you can optionally test that this server is running:
```py
from openai import OpenAI  # Not using OpenAI API, but required for using vLLM's OpenAI-compatible API
openai_api_key = "EMPTY"
openai_api_base = "http://localhost:8000/v1"
client = OpenAI(
    api_key=openai_api_key,
    base_url=openai_api_base,
)
completion = client.completions.create(model="meta-llama/Meta-Llama-3-8B-Instruct",
                                      prompt="San Francisco is a")
print("Completion result:", completion)
```

Then, you can implement the setup and call functions for your model:
```py
import text_lloom.workbench as wb
from text_lloom.llm import Model, EmbedModel

# SETUP functions
# Meta-Llama-3-8B-Instruct for LLM
def setup_llm_fn(api_key):
    from openai import OpenAI  # Not using directly; just for vLLM's OpenAI-compatible API
    openai_api_base = "http://localhost:8000/v1"
    llm_client = OpenAI(
        api_key=api_key,
        base_url=openai_api_base,
    )
    return llm_client

# all-MiniLM-L6-v2 Sentence Transformers model for text embeddings
def setup_embed_fn(api_key):
    from sentence_transformers import SentenceTransformer
    model = SentenceTransformer("all-MiniLM-L6-v2")
    return model

# CALL functions
async def call_llm_fn(model, prompt):
    if "system_prompt" not in model.args:
        model.args["system_prompt"] = "You are a helpful assistant who helps with identifying patterns in text examples."
    if "temperature" not in model.args:
        model.args["temperature"] = 0
        
    res = model.client.chat.completions.create(
        model=model.name,
        temperature=model.args["temperature"],
        messages=[
            {"role": "system", "content": model.args["system_prompt"]},
            {"role": "user", "content": prompt},
        ]
    )
    res_parsed = res.choices[0].message.content if res else None
    tokens = [0, 0]
    return res_parsed, tokens

def call_embed_fn(model, text_arr):
    embed_model = model.client
    embeddings = embed_model.encode(text_arr)
    embeddings = embeddings.tolist()
    tokens = [0, 0]
    return embeddings, tokens

api_key = "EMPTY"
```

Finally, you can create your LLooM instance using the open-source models:
```py {5-25}
l = wb.lloom(
    df=df,
    id_col="doc_id",
    text_col="text",
    # Open source model spec
    distill_model=Model(
        setup_fn=setup_llm_fn, 
        fn=call_llm_fn, 
        name="meta-llama/Meta-Llama-3-8B-Instruct", cost=[0,0], rate_limit=(300, 10), context_window=16385, api_key=api_key
    ),
    cluster_model=EmbedModel(
        setup_fn=setup_embed_fn, 
        fn=call_embed_fn, 
        name="", cost=(0), batch_size=2048, api_key=api_key
    ),
    synth_model=Model(
        setup_fn=setup_llm_fn, 
        fn=call_llm_fn, 
        name="meta-llama/Meta-Llama-3-8B-Instruct", cost=[0,0], rate_limit=(20, 10), context_window=128000, api_key=api_key
    ),
    score_model=Model(
        setup_fn=setup_llm_fn, 
        fn=call_llm_fn, 
        name="meta-llama/Meta-Llama-3-8B-Instruct", cost=[0,0], rate_limit=(300, 10), context_window=16385, api_key=api_key
    ),
)
```

# LLooM Operators

The LLooM Operators are a lower-level API for the operators that underlie the LLooM algorithm. The operators are defined as the `concept_induction` module within the `text_lloom` Python package. The LLooM Workbench module calls these functions internally to carry out concept induction.

```py
import text_lloom.concept_induction as ci
```

**Core operators**:
- `Distill`: Shards out and scales down data to the context window while preserving salient details.
    - `Distill-filter`: Performs extractive summarization that selects exact quotes from the original text.
    - `Distill-summarize`: Performs abstractive summarization in the form of bullet point text summaries.

- `Cluster`: Recombines shards from the Distill step into groupings that share enough meaningful overlap to induce meaningful rather than surface-level concepts

- `Synthesize`: Prompts the model to generalize from provided examples to generate concept descriptions and criteria in natural language.

- `Score`:  Labels all text documents by applying concept criteria expressed as zero- shot prompts.

**Additional operators**:
- `Seed`: Allows the user to steer concept induction. Accepts a user-provided seed term to condition the Distill or Synthesize operators, which can improve the quality and alignment of the output concepts.

- `Loop`: Further iterates on concepts by looping back to concept generation after scoring.

::: info 🚧 Under construction
Detailed documentation coming soon!
:::

### distill_filter
`distill_filter(text_df, doc_col, doc_id_col, model_name, n_quotes=3, seed=None, sess=None)`

### distill_summarize
`distill_summarize(text_df, doc_col, doc_id_col, model_name, n_bullets="2-4", n_words_per_bullet="5-8", seed=None, sess=None):`

### cluster
`cluster(text_df, doc_col, doc_id_col, cluster_id_col="cluster_id", min_cluster_size=None, embed_model_name="text-embedding-ada-002", batch_size=20, randomize=False, sess=None)`

### synthesize
`synthesize(cluster_df, doc_col, doc_id_col, model_name, cluster_id_col="cluster_id", concept_col_prefix="concept", n_concepts=None, batch_size=None, verbose=False, pattern_phrase="unifying pattern", dedupe=True, seed=None, sess=None, return_logs=False)`

### score_concepts
`score_concepts(text_df, text_col, doc_id_col, concepts, model_name="gpt-3.5-turbo", batch_size=5, get_highlights=False, sess=None, threshold=1.0)`

### loop
`loop(score_df, doc_col, doc_id_col, debug=False)`

### review
`review(concepts, concept_df, concept_col_prefix, model_name, debug=False, sess=None, return_logs=False)`

# LLooM Workbench

The LLooM Workbench is a higher-level API for computational notebooks that surfaces interactive notebook widgets to inspect data by induced concepts. It is defined as the `workbench` module within the `text_lloom` Python package and consists of the `lloom` class.

```py
import text_lloom.workbench as wb
```

# lloom
`lloom(df, text_col, id_col=None, distill_model_name="gpt-3.5-turbo", embed_model_name="text-embedding-3-large", synth_model_name="gpt-4-turbo", score_model_name="gpt-3.5-turbo", rate_limits={})`

A `lloom` instance manages a working session with a provided dataset. It allows the user to load their dataset and perform rounds of concept induction, concept scoring, and visualization.

**Parameters**:
- `df` _(pd.DataFrame)_: Text dataset that will be analyzed with LLooM. This dataframe must include a column that contains the input text documents. LLooM expects a dataframe where each row represents a distinct document (or unit of analysis). This is the primary text that will be analyzed with LLooM. The dataframe may also have other columns with additional metadata, which can be used for analysis with LLooM visualizations.
- `text_col` _(str)_: Name of the primary text column in the provided `df`.
- `id_col` _(str, optional, default: None)_: Name of a column with unique IDs for each row. If not provided, the system will assign an ID to each row.
- `distill_model_name` _(str, optional, default: "gpt-3.5-turbo")_: Name of the OpenAI model to use for the Distill operators (filter and summarize).
- `embed_model_name` _(str, optional, default: "text-embedding-3-large")_: Name of the OpenAI embedding model to use for the Cluster operator.
- `synth_model_name` _(str, optional, default: "gpt-4-turbo")_: Name of the OpenAI model to use for the Synthesize operator.
- `score_model_name` _(str, optional, default: "gpt-3.5-turbo")_: Name of the OpenAI model to use for the Score operator.
- `rate_limits` _(Dict, optional, default: {})_: An optional dictionary specifying a mapping from an OpenAI model to its associated rate-limit parameters, a tuple of the form (n_requests, wait_time_secs), where n_requests indicates the number of requests allowed in one batch and wait_time_secs indicates the length of time (in seconds) to wait between batches. Example: `{ "gpt-4-turbo": (40, 10) }`. If not specified, defaults to the values defined as `RATE_LIMITS` in [`llm.py`](https://github.com/michelle123lam/lloom/blob/24a7f5b1335311b90b4788608a3784a5d87e4482/text_lloom/src/text_lloom/llm.py#L34-L41).

**Example**:
```py
# Creating a LLooM instance
l = wb.lloom(
    df=df,
    text_col="your_doc_text_col",
    id_col="your_doc_id_col",  # Optional
)
```

### gen
`gen(seed=None, params=None, n_synth=1, auto_review=True)`

Runs concept generation, which includes the `Distill`-`Cluster`-`Synthesize` operator pipeline.

**Parameters**:
- `seed` _(str, optional, default: None)_: The optional seed term can steer concept induction towards more specific areas of interest (e.g., social issues" for political discussion or "evaluation methods" for academic papers). 
- `params` _(Dict, optional, default: None)_: The specific parameters to use within the Distill, Cluster, and Synthesize operators. By default, the system auto-suggests parameters based on the length and number of documents. If specified, the parameters should include the following:
    ```py
    {
        "filter_n_quotes": filter_n_quotes,  # Number of quotes per document
        "summ_n_bullets": summ_n_bullets,  # Number of bullet points per document
        "synth_n_concepts": synth_n_concepts,  # Number of concepts per cluster/batch
    }
    ```
- `n_synth` _(int, optional, default: 1)_: The number of times to run the Synthesize operator.
- `auto_review` _(bool, optional, default: True)_: Whether to run a step after the Synthesize operator for the system to review the set of concepts to remove low-quality concepts and merge overlapping concepts.

**Examples**:
```py
# Default version (no seed)
await l.gen()

# Or: Seed version
await l.gen(
    seed="your_optional_seed_term",
)
```

### gen_auto
`gen_auto(max_concepts=8, seed=None, params=None, n_synth=1)`

Runs concept generation, selection, and scoring as a single automated step. In `gen_auto`, the system makes a call to the LLM to automatically select which concepts to score. By contrast, `gen` only generates the concepts and allows the user to run the `select` function to review and select concepts, followed by the `score` function to perform that scoring. Returns a dataframe with the score results.

**Parameters**:
- `max_concepts` _(int, optional, default: 8)_: The maximum number of concepts for the system to select out of the set of generated concepts. All of these concepts will be scored. After concept generation, the user is prompted to confirm the set of concepts before scoring proceeds, so there is still an opportunity to review the automatic selection.
- `seed` _(str, optional, default: None)_: (Same as `gen`) The optional seed term can steer concept induction towards more specific areas of interest (e.g., social issues" for political discussion or "evaluation methods" for academic papers). 
- `params` _(Dict, optional, default: None)_: (Same as `gen`) The specific parameters to use within the Distill, Cluster, and Synthesize operators. Refer to [`gen`](#gen) for details.
- `n_synth` _(int, optional, default: 1)_: (Same as `gen`) The number of times to run the Synthesize operator.

**Example**:
```py
score_df = await l.gen_auto(
    max_concepts=5,
    seed="your_optional_seed_term", 
)
```

### select
`select()`

Allows the user to review and select concepts for scoring. Displays an interactive widget in the notebook.

**Example**:
```py
l.select()
```

In the output, each box contains the concept name, concept inclusion criteria, and representative example(s).
![LLooM select() function output](/media/ui/select_output.png)

### select_auto
`select_auto(max_concepts)`

Automatically selects up to the specified number of concepts via an LLM call.

**Parameters**:
- `max_concepts` _(int)_: The maximum number of concepts for the system to select out of the set of generated concepts. All of these concepts will be scored when the user calls the `score()` function.

**Example**:
```py
 await self.select_auto(max_concepts=8)
```

### show_selected
`show_selected()`

Prints out a summary of the concepts that have been currently selected. The user can make changes via the `select()` widget and re-run this function to check the current state.

**Example**:
```py
l.show_selected()
```

### score
`score(c_ids=None, batch_size=1, get_highlights=True, ignore_existing=True)`

Score all documents with respect to each concept to indicate the extent to which the document matches the concept inclusion criteria. Returns a dataframe with the score results.

**Parameters**:
- `c_ids` _(List[str], optional, default: None)_: A list of IDs (UUID strings) for the concepts that should be scored.
- `batch_size` _(int, optional, default: 1)_: Number of documents to score at once in each LLM call. By default, LLooM scores each (concept, document) combination individually to improve scoring reliability. Increasing this number will batch together multiple documents to be scored at once for a given concept.
- `get_highlights` _(bool, optional, default: True)_: Whether to retrieve highlighted quotes indicating where the document illustrates the concept.
- `ignore_existing` _(bool, optional, default: True)_: Whether to ignore concepts that have previously been scored.

**Returns**:
- `score_df` _(pd.DataFrame)_: Dataframe summarizing scoring results. Contains the following columns:
    - doc_id: Unique document ID
    - text: Text of the document
    - concept_id: Unique ID for the concept (assigned internally)
    - concept_name: Name of the concept
    - concept_prompt: Prompt conveying the concept inclusion criteria
    - score: Concept score (range: [0, 0.25, 0.5, 0.75, 1.0], where 0 indicates no concept match and 1 indicates the highest concept match)
    - rationale: LLM-provided rationale for the score
    - highlight: LLM-extracted quote from the document that illustrates the concept (if applicable) 
    - concept_seed: The seed used to generate the concept (if provided)

**Example**:
```py
score_df = await l.score()
```

### get_score_df
`get_score_df()`

Retrieves the `score_df` for the current set of active concepts.

**Returns**:
- `score_df` _(pd.DataFrame)_: Dataframe summarizing scoring results. Refer to [`score`](#score) for details.

**Example**:
```py
score_df = l.get_score_df()
```

### summary
`summary(verbose=True)`

Displays a **cumulative** summary of the (1) Total time, (2) Total cost, and (3) Tokens for the entire LLooM instance. 
- Total time: Displays the total time required for each operator. Each tuple contains the operator name and the timestamp at which the operation completed. 
- Total cost: Displays the calculated cost incurred by each operator (in US Dollars).
- Tokens: Displays the overall number of tokens used (total, in, and out)

**Parameters**:
- `verbose` _(bool, optional, default: True)_: Whether to print out verbose output (per-operator breakdowns of time and cost).

**Example**:
```py
l.summary()
```

Sample output:
```
Total time: 25.31 sec (0.42 min)
	('distill_filter', '2024-03-08-02-45-20'): 3.13 sec
	('distill_summarize', '2024-03-08-02-45-21'): 1.80 sec
	('cluster', '2024-03-08-02-45-25'): 4.00 sec
	('synthesize', '2024-03-08-02-45-42'): 16.38 sec


Total cost: $0.14
	('distill_filter', '2024-03-08-02-45-20'): $0.02
	('distill_summarize', '2024-03-08-02-45-21'): $0.02
	('synthesize', '2024-03-08-02-45-42'): $0.10


Tokens: total=67045, in=55565, out=11480
```

### vis
`vis(cols_to_show=[], slice_col=None, max_slice_bins=5, slice_bounds=None, show_highlights=True, norm_by=None, export_df=False, include_outliers=False)`

Visualizes the concept results in the main LLooM Workbench view. An interactive widget will appear when you run this function.

**Parameters**:
- `cols_to_show` _(List[str], optional, default: [])_: Additional column names to show in the tables
- `slice_col` _(str, optional, default: None)_: Name of a column with which to slice the data. This should be a pre-existing metadata column in the dataframe. Numeric or string columns are supported. Currently, numeric columns are automatically binned into quantiles, and string columns are treated as categorical variables.
- `max_slice_bins` _(int, optional, default: 5)_: For numeric columns, the maximum number of bins to create
- `slice_bounds` _(List[float], optional, default: None)_: For numeric columns, manual bin boundaries to use. Example: `[0, 0.2, 0.4, 0.6, 0.8, 1.0]`
- `show_highlights` _(bool, optional, default: True)_: Whether to show text highlights in the table.
- `norm_by` _(str, optional, default: None)_: How to normalize scores for the matrix visualization. Options: `"concept"` or `"slice"`. If not provided, the scores will not be normalized and the matrix will reflect absolute counts.
- `export_df` _(bool, optional, default: False)_: Whether to return a dataframe for export. This dataframe contains the following columns:
    - concept: Concept name
    - criteria: Concept inclusion criteria
    - summary: Written summary of the documents that matched the concept
    - rep_examples: Representative text examples of the concept
    - prevalence: Proportion of total documents that matched this concept
    - n_matches: Absolute number of documents that matched this concept
    - highlights: Sample of highlighted text from documents that matched the concept
- `include_outliers` _(bool, optional, default: False)_: Whether to include outliers in the export_df (if requested).

**Examples**:
```py
l.vis()

# With slice column
l.vis(slice_col="n_likes")

# With normalization by concept
l.vis(slice_col="n_likes", norm_by="concept")

# With normalization by slice
l.vis(slice_col="n_likes", norm_by="slice")
```
Check out [Using the LLooM Workbench](../about/vis-guide.md) for a more detailed guide on the visualization components.
![LLooM vis() function output](/media/ui/vis_output.png)

### add
`add(name, prompt, ex_ids=[], get_highlights=True)`

Adds a new custom concepts by providing a name and prompt. This function will automatically score the data by that concept.

**Parameters**:
- `name` _(str)_: The new concept name
- `prompt` _(str)_: The new concept prompt, which conveys its inclusion criteria. 
- `ex_ids` _(List[str], optional, default: [])_: IDs of the documents that exemplify this concept.
- `get_highlights` _(bool, optional, default: True)_: Whether to retrieve highlighted quotes indicating where the document illustrates the concept.

**Example**:
```py
await l.add(
    # Your new concept name
    name="Government Critique",
    # Your new concept prompt
    prompt="Does this text criticize government actions or policies?", 
)
```

### save
`save(folder, file_name=None)`

Save the LLooM instance to a pickle file to reload at a later point.

**Parameters**:
- `folder` _(str)_: File path of the folder in which to store the pickle file.
- `file_name` _(str, optional, default: None)_: Name of the pickle file. If not specified, the system will generate a name based on the current local time.

**Example**:
```py
l.save(folder="your/path/here", file_name="your_file_name")

# Reloading later
import pickle
with open("your/path/here/your_file_name.pkl", "rb") as f:
    l = pickle.load(f)
```

### export_df
`export_df(include_outliers=False)`

Export a summary of the results in Pandas Dataframe form.

**Parameters**:
- `include_outliers` _(bool, optional, default: False)_: Whether to include the category of outliers (documents that did not match _any_ concepts) in the table.

**Returns**:
- `export_df` _(pd.DataFrame)_: Dataframe summarizing the concepts. Contains the following columns:
    - concept: Concept name
    - criteria: Concept inclusion criteria
    - summary: Written summary of the documents that matched the concept
    - rep_examples: Representative text examples of the concept
    - prevalence: Proportion of total documents that matched this concept
    - n_matches: Absolute number of documents that matched this concept
    - highlights: Sample of highlighted text from documents that matched the concept

**Example**:
```py
export_df = l.export_df()
```

### submit
`submit()`

Allows users to submit their LLooM instance to share their work, which may be selected to be featured in a gallery of results.

**Example**:
```py
l.submit()
```
You will be prompted to provide a few more details: 
- **Email address**: Please provide an email address so that we can contact you if your work is selected.
- **Analysis goal**: Share as much detail as you'd like about your analysis: What data were you using? What questions were you trying to answer? What did you find?

### estimate_gen_cost
`estimate_gen_cost(params=None, verbose=False)`

Estimates the cost of running `gen()` with the given parameters. The function is automatically run within calls to `gen()` for the user to review before proceeding with concept generation.

**Parameters**:
- `params` _(Dict, optional, default: None)_: The specific parameters to use within the Distill, Cluster, and Synthesize operators (see [`gen`](#gen) for details). If no parameters are provided, the function uses [auto-suggested parameters](#auto-suggest-parameters).
- `verbose` _(bool, optional, default: False)_: Whether to print a full per-operator cost breakdown

**Example**:
```py
l.estimate_gen_cost()
```

### estimate_score_cost
`estimate_score_cost(n_concepts=None, verbose=False)`

Estimates the cost of running `score()` on the provided number of concepts. The function is automatically run within calls to `score()` for the user to review before proceeding with concept scoring.

**Parameters**:
- `n_concepts` _(int, optional, default: None)_: Number of concepts to score. If not specified, the function uses the current number of active (selected) concepts.
- `verbose` _(bool, optional, default: False)_: Whether to print a full per-operator cost breakdown

**Example**:
```py
l.estimate_score_cost()
```

### auto_suggest_parameters
`auto_suggest_parameters(sample_size=None, target_n_concepts=20)`

Suggests concept generation parameters based on heuristics related to the number and length of documents in the dataset. Called automatically in `gen()` and `estimate_gen_cost()` if no parameters are provided.

**Parameters**:
- `sample_size` _(int, optional, default: None)_: Number of documents to sample from `df` to determine the parameters. If not provided, all documents will be used.
- `target_n_concepts` _(int, optional, default: 20)_: The estimated total number of concepts that the user would like to generate.

**Returns**:
- `params` _(Dict)_: The parameters to use within the Distill, Cluster, and Synthesize operators. Refer to [`gen`](#gen) for details.

**Example**:
```py
params = l.auto_suggest_parameters()
```
