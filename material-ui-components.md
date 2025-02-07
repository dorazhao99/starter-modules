# Material UI Components
## Accordion

<p class="description">The Accordion component lets users show and hide sections of related content on a page.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

The Material UI Accordion component includes several complementary utility components to handle various use cases:

- Accordion: the wrapper for grouping related components.
- Accordion Summary: the wrapper for the Accordion header, which expands or collapses the content when clicked.
- Accordion Details: the wrapper for the Accordion content.
- Accordion Actions: an optional wrapper that groups a set of buttons.

{{"demo": "AccordionUsage.js", "bg": true}}

:::info
This component is no longer documented in the [Material Design guidelines](https://m2.material.io/), but Material UI will continue to support it.
:::

 Basics

```jsx
import Accordion from '@mui/material/Accordion';
import AccordionDetails from '@mui/material/AccordionDetails';
import AccordionSummary from '@mui/material/AccordionSummary';
```

 Expand icon

Use the `expandIcon` prop on the Accordion Summary component to change the expand indicator icon.
The component handles the turning upside-down transition automatically.

{{"demo": "AccordionExpandIcon.js", "bg": true}}

 Expanded by default

Use the `defaultExpanded` prop on the Accordion component to have it opened by default.

{{"demo": "AccordionExpandDefault.js", "bg": true}}

 Transition

Use the `slots.transition` and `slotProps.transition` props to change the Accordion's default transition.

{{"demo": "AccordionTransition.js", "bg": true}}

 Disabled item

Use the `disabled` prop on the Accordion component to disable interaction and focus.

{{"demo": "DisabledAccordion.js", "bg": true}}

 Controlled Accordion

The Accordion component can be controlled or uncontrolled.

{{"demo": "ControlledAccordions.js", "bg": true}}

:::info

- A component is **controlled** when it's managed by its parent using props.
- A component is **uncontrolled** when it's managed by its own local state.

Learn more about controlled and uncontrolled components in the [React documentation](https://react.dev/learn/sharing-state-between-components##controlled-and-uncontrolled-components).
:::

 Customization

 Only one expanded at a time

Use the `expanded` prop with React's `useState` hook to allow only one Accordion item to be expanded at a time.
The demo below also shows a bit of visual customization.

{{"demo": "CustomizedAccordions.js", "bg": true}}

 Changing heading level

By default, the Accordion uses an `h3` element for the heading. You can change the heading element using the `slotProps.heading.component` prop to ensure the correct heading hierarchy in your document.

```jsx
<Accordion slotProps={{ heading: { component: 'h4' } }}>
  <AccordionSummary
    expandIcon={<ExpandMoreIcon />}
    aria-controls="panel1-content"
    id="panel1-header"
  >
    Accordion
  </AccordionSummary>
  <AccordionDetails>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada
    lacus ex, sit amet blandit leo lobortis eget.
  </AccordionDetails>
</Accordion>
```

 Performance

The Accordion content is mounted by default even if it's not expanded.
This default behavior has server-side rendering and SEO in mind.

If you render the Accordion Details with a big component tree nested inside, or if you have many Accordions, you may want to change this behavior by setting `unmountOnExit` to `true` inside the `slotProps.transition` prop to improve performance:

```jsx
<Accordion slotProps={{ transition: { unmountOnExit: true } }} />
```

 Accessibility

The [WAI-ARIA guidelines for accordions](https://www.w3.org/WAI/ARIA/apg/patterns/accordion/) recommend setting an `id` and `aria-controls`, which in this case would apply to the Accordion Summary component.
The Accordion component then derives the necessary `aria-labelledby` and `id` from its content.

```jsx
<Accordion>
  <AccordionSummary id="panel-header" aria-controls="panel-content">
    Header
  </AccordionSummary>
  <AccordionDetails>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </AccordionDetails>
</Accordion>
```

 Anatomy

The Accordion component consists of a root `<div>` that contains the Accordion Summary, Accordion Details, and optional Accordion Actions for action buttons.

```jsx
<div class="MuiAccordion-root">
  <h3 class="MuiAccordion-heading">
    <button class="MuiButtonBase-root MuiAccordionSummary-root" aria-expanded="">
      <!-- Accordion summary goes here -->
    </button>
  </h3>
  <div class="MuiAccordion-region" role="region">
    <div class="MuiAccordionDetails-root">
      <!-- Accordion content goes here -->
    </div>
  </div>
</div>
```

## Alert

<p class="description">Alerts display brief messages for the user without interrupting their use of the app.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Alerts give users brief and potentially time-sensitive information in an unobtrusive manner.

The Material UI Alert component includes several props for quickly customizing its styles to provide immediate visual cues about its contents.

{{"demo": "SimpleAlert.js"}}

:::info
This component is no longer documented in the [Material Design guidelines](https://m2.material.io/), but Material UI will continue to support it.
:::

 Usage

A key trait of the alert pattern is that [it should not interrupt the user's experience](https://www.w3.org/WAI/ARIA/apg/patterns/alert/) of the app.
Alerts should not be confused with alert _dialogs_ ([ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/alertdialog/)), which _are_ intended to interrupt the user to obtain a response.
Use the Material UI [Dialog](/material-ui/react-dialog/) component if you need this behavior.

 Basics

```jsx
import Alert from '@mui/material/Alert';
```

The Alert component wraps around its content, and stretches to fill its enclosing container.

 Severity

The `severity` prop accepts four values representing different states—`success` (the default), `info`, `warning`, and `error`–with corresponding icon and color combinations for each:

{{"demo": "BasicAlerts.js"}}

 Variants

The Alert component comes with two alternative style options—`filled` and `outlined`—which you can set using the `variant` prop.

 Filled

{{"demo": "FilledAlerts.js"}}

 Outlined

{{"demo": "OutlinedAlerts.js"}}

:::warning
When using an outlined Alert with the [Snackbar](/material-ui/react-snackbar/) component, background content will be visible and bleed through the Alert by default.
You can prevent this by adding `bgcolor: 'background.paper'` to [the `sx` prop](/material-ui/customization/how-to-customize/##the-sx-prop) on the Alert component:

```jsx
<Alert sx={{ bgcolor: 'background.paper' }} />
```

Check out the [Snackbar—customization](/material-ui/react-snackbar/##customization) doc for an example of how to use these two components together.
:::

 Color

Use the `color` prop to override the default color for the specified [`severity`](##severity)—for instance, to apply `warning` colors to a `success` Alert:

{{"demo": "ColorAlerts.js"}}

 Actions

Add an action to your Alert with the `action` prop.
This lets you insert any element—an HTML tag, an SVG icon, or a React component such as a Material UI Button—after the Alert's message, justified to the right.

If you provide an `onClose` callback to the Alert without setting the `action` prop, the component will display a close icon (&##x2715;) by default.

{{"demo": "ActionAlerts.js"}}

 Icons

Use the `icon` prop to override an Alert's icon.
As with the [`action`](##actions) prop, your `icon` can be an HTML element, an SVG icon, or a React component.
Set this prop to `false` to remove the icon altogether.

If you need to override all instances of an icon for a given [`severity`](##severity), you can use the `iconMapping` prop instead.
You can define this prop globally by customizing your app's theme. See [Theme components—Default props](/material-ui/customization/theme-components/##theme-default-props) for details.

{{"demo": "IconAlerts.js"}}

 Customization

 Titles

To add a title to an Alert, import the Alert Title component:

```jsx
import AlertTitle from '@mui/material/AlertTitle';
```

You can nest this component above the message in your Alert for a neatly styled and properly aligned title, as shown below:

{{"demo": "DescriptionAlerts.js"}}

 Transitions

You can use [Transition components](/material-ui/transitions/) like [Collapse](/material-ui/transitions/##collapse) to add motion to an Alert's entrance and exit.

{{"demo": "TransitionAlerts.js"}}

 Accessibility

Here are some factors to consider to ensure that your Alert is accessible:

- Because alerts are not intended to interfere with the use of the app, your Alert component should _never_ affect the keyboard focus.
- If an alert contains an action, that action must have a `tabindex` of `0` so it can be reached by keyboard-only users.
- Essential alerts should not disappear automatically—[timed interactions](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) can make your app inaccessible to users who need extra time to understand or locate the alert.
- Alerts that occur too frequently can [inhibit the usability](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) of your app.
- Dynamically rendered alerts are announced by screen readers; alerts that are already present on the page when it loads are _not_ announced.
- Color does not add meaning to the UI for users who require assistive technology. You must ensure that any information conveyed through color is also denoted in other ways, such as within the text of the alert itself, or with additional hidden text that's read by screen readers.

 Anatomy

The Alert component is composed of a root [Paper](/material-ui/react-paper/) component (which renders as a `<div>`) that houses an icon, a message, and an optional [action](##actions):

```html
<div class="MuiPaper-root MuiAlert-root" role="alert">
  <div class="MuiAlert-icon">
    <!-- svg icon here -->
  </div>
  <div class="MuiAlert-message">This is how an Alert renders in the DOM.</div>
  <div class="MuiAlert-action">
    <!-- optional action element here -->
  </div>
</div>
```

## App Bar

<p class="description">The App Bar displays information and actions relating to the current screen.</p>

The top App bar provides content and actions related to the current screen. It's used for branding, screen titles, navigation, and actions.

It can transform into a contextual action bar or be used as a navbar.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic App bar

{{"demo": "ButtonAppBar.js", "bg": true}}

 App bar with menu

{{"demo": "MenuAppBar.js", "bg": true}}

 App bar with responsive menu

{{"demo": "ResponsiveAppBar.js", "bg": true}}

 App bar with search field

A side searchbar.

{{"demo": "SearchAppBar.js", "bg": true}}

 Responsive App bar with Drawer

{{"demo": "DrawerAppBar.js", "bg": true,"iframe": true}}

 App bar with a primary search field

A primary searchbar.

{{"demo": "PrimarySearchAppBar.js", "bg": true}}

 Dense (desktop only)

{{"demo": "DenseAppBar.js", "bg": true}}

 Prominent

A prominent app bar.

{{"demo": "ProminentAppBar.js", "bg": true}}

 Bottom App bar

{{"demo": "BottomAppBar.js", "iframe": true, "maxWidth": 400}}

 Fixed placement

When you render the app bar position fixed, the dimension of the element doesn't impact the rest of the page. This can cause some part of your content to be invisible, behind the app bar. Here are 3 possible solutions:

1. You can use `position="sticky"` instead of fixed.
2. You can render a second `<Toolbar />` component:

```jsx
function App() {
  return (
    <React.Fragment>
      <AppBar position="fixed">
        <Toolbar>{/* content */}</Toolbar>
      </AppBar>
      <Toolbar />
    </React.Fragment>
  );
}
```

3. You can use `theme.mixins.toolbar` CSS:

```jsx
const Offset = styled('div')(({ theme }) => theme.mixins.toolbar);

function App() {
  return (
    <React.Fragment>
      <AppBar position="fixed">
        <Toolbar>{/* content */}</Toolbar>
      </AppBar>
      <Offset />
    </React.Fragment>
  );
}
```

 Scrolling

You can use the `useScrollTrigger()` hook to respond to user scroll actions.

 Hide App bar

The app bar hides on scroll down to leave more space for reading.

{{"demo": "HideAppBar.js", "iframe": true, "disableLiveEdit": true}}

 Elevate App bar

The app bar elevates on scroll to communicate that the user is not at the top of the page.

{{"demo": "ElevateAppBar.js", "iframe": true, "disableLiveEdit": true}}

 Back to top

A floating action button appears on scroll to make it easy to get back to the top of the page.

{{"demo": "BackToTop.js", "iframe": true, "disableLiveEdit": true}}

 `useScrollTrigger([options]) => trigger`

 Arguments

1. `options` (_object_ [optional]):

   - `options.disableHysteresis` (_bool_ [optional]): Defaults to `false`. Disable the hysteresis. Ignore the scroll direction when determining the `trigger` value.
   - `options.target` (_Node_ [optional]): Defaults to `window`.
   - `options.threshold` (_number_ [optional]): Defaults to `100`. Change the `trigger` value when the vertical scroll strictly crosses this threshold (exclusive).

 Returns

`trigger`: Does the scroll position match the criteria?

 Examples

```jsx
import useScrollTrigger from '@mui/material/useScrollTrigger';

function HideOnScroll(props) {
  const trigger = useScrollTrigger();
  return (
    <Slide in={!trigger}>
      <div>Hello</div>
    </Slide>
  );
}
```

 Enable color on dark

Following the [Material Design guidelines](https://m2.material.io/design/color/dark-theme.html), the `color` prop has no effect on the appearance of the app bar in dark mode.
You can override this behavior by setting the `enableColorOnDark` prop to `true`.

{{"demo": "EnableColorOnDarkAppBar.js", "bg": true}}

 Toolpad (Beta)

 Dashboard Layout

The [DashboardLayout](https://mui.com/toolpad/core/react-dashboard-layout/) component from `@toolpad/core` is the starting point for dashboarding applications. It takes care of application layout, theming, navigation, and more. An example usage of this component:

{{"demo": "DashboardLayoutBasic.js", "height": 400, "iframe": true, "defaultExpanded": false}}

## Autocomplete

<p class="description">The autocomplete is a normal text input enhanced by a panel of suggested options.</p>

The widget is useful for setting the value of a single-line textbox in one of two types of scenarios:

1. The value for the textbox must be chosen from a predefined set of allowed values, for example a location field must contain a valid location name: [combo box](##combo-box).
2. The textbox may contain any arbitrary value, but it is advantageous to suggest possible values to the user, for example a search field may suggest similar or previous searches to save the user time: [free solo](##free-solo).

It's meant to be an improved version of the "react-select" and "downshift" packages.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Combo box

The value must be chosen from a predefined set of allowed values.

{{"demo": "ComboBox.js"}}

 Options structure

By default, the component accepts the following options structures:

```ts
interface AutocompleteOption {
  label: string;
}
// or
type AutocompleteOption = string;
```

for instance:

```js
const options = [
  { label: 'The Godfather', id: 1 },
  { label: 'Pulp Fiction', id: 2 },
];
// or
const options = ['The Godfather', 'Pulp Fiction'];
```

However, you can use different structures by providing a `getOptionLabel` prop.

If your options are objects, you must provide the `isOptionEqualToValue` prop to ensure correct selection and highlighting. By default, it uses strict equality to compare options with the current value.

 Playground

Each of the following examples demonstrates one feature of the Autocomplete component.

{{"demo": "Playground.js"}}

 Country select

Choose one of the 248 countries.

{{"demo": "CountrySelect.js"}}

 Controlled states

The component has two states that can be controlled:

1. the "value" state with the `value`/`onChange` props combination. This state represents the value selected by the user, for instance when pressing <kbd class="key">Enter</kbd>.
2. the "input value" state with the `inputValue`/`onInputChange` props combination. This state represents the value displayed in the textbox.

These two states are isolated, and should be controlled independently.

:::info

- A component is **controlled** when it's managed by its parent using props.
- A component is **uncontrolled** when it's managed by its own local state.

Learn more about controlled and uncontrolled components in the [React documentation](https://react.dev/learn/sharing-state-between-components##controlled-and-uncontrolled-components).
:::

{{"demo": "ControllableStates.js"}}

:::warning

If you control the `value`, make sure it's referentially stable between renders.
In other words, the reference to the value shouldn't change if the value itself doesn't change.

```tsx
// ⚠️ BAD
return <Autocomplete multiple value={allValues.filter((v) => v.selected)} />;

// 👍 GOOD
const selectedValues = React.useMemo(
  () => allValues.filter((v) => v.selected),
  [allValues],
);
return <Autocomplete multiple value={selectedValues} />;
```

In the first example, `allValues.filter` is called and returns **a new array** every render.
The fix includes memoizing the value, so it changes only when needed.
:::

 Free solo

Set `freeSolo` to true so the textbox can contain any arbitrary value.

 Search input

The prop is designed to cover the primary use case of a **search input** with suggestions, for example Google search or react-autowhatever.

{{"demo": "FreeSolo.js"}}

:::warning
Be careful when using the free solo mode with non-string options, as it may cause type mismatch.

The value created by typing into the textbox is always a string, regardless of the type of the options.
:::

 Creatable

If you intend to use this mode for a [combo box](##combo-box) like experience (an enhanced version of a select element) we recommend setting:

- `selectOnFocus` to help the user clear the selected value.
- `clearOnBlur` to help the user enter a new value.
- `handleHomeEndKeys` to move focus inside the popup with the <kbd class="key">Home</kbd> and <kbd class="key">End</kbd> keys.
- A last option, for instance: `Add "YOUR SEARCH"`.

{{"demo": "FreeSoloCreateOption.js"}}

You could also display a dialog when the user wants to add a new value.

{{"demo": "FreeSoloCreateOptionDialog.js"}}

 Grouped

You can group the options with the `groupBy` prop.
If you do so, make sure that the options are also sorted with the same dimension that they are grouped by,
otherwise, you will notice duplicate headers.

{{"demo": "Grouped.js"}}

To control how the groups are rendered, provide a custom `renderGroup` prop.
This is a function that accepts an object with two fields:

- `group`—a string representing a group name
- `children`—a collection of list items that belong to the group

The following demo shows how to use this prop to define custom markup and override the styles of the default groups:

{{"demo": "RenderGroup.js"}}

 Disabled options

{{"demo": "DisabledOptions.js"}}

 `useAutocomplete`

For advanced customization use cases, a headless `useAutocomplete()` hook is exposed.
It accepts almost the same options as the Autocomplete component minus all the props
related to the rendering of JSX.
The Autocomplete component is built on this hook.

```tsx
import { useAutocomplete } from '@mui/base/useAutocomplete';
```

The `useAutocomplete` hook is also reexported from @mui/material for convenience and backward compatibility.

```tsx
import useAutocomplete from '@mui/material/useAutocomplete';
```

- 📦 [4.6 kB gzipped](https://bundlephobia.com/package/@mui/material).

{{"demo": "UseAutocomplete.js", "defaultCodeOpen": false}}

 Customized hook

{{"demo": "CustomizedHook.js"}}

Head to the [customization](##customization) section for an example with the `Autocomplete` component instead of the hook.

 Asynchronous requests

The component supports two different asynchronous use-cases:

- [Load on open](##load-on-open): it waits for the component to be interacted with to load the options.
- [Search as you type](##search-as-you-type): a new request is made for each keystroke.

 Load on open

It displays a progress state as long as the network request is pending.

{{"demo": "Asynchronous.js"}}

 Search as you type

If your logic is fetching new options on each keystroke and using the current value of the textbox
to filter on the server, you may want to consider throttling requests.

Additionally, you will need to disable the built-in filtering of the `Autocomplete` component by
overriding the `filterOptions` prop:

```jsx
<Autocomplete filterOptions={(x) => x} />
```

 Google Maps place

A customized UI for Google Maps Places Autocomplete.
For this demo, we need to load the [Google Maps JavaScript](https://developers.google.com/maps/documentation/javascript/overview) and [Google Places](https://developers.google.com/maps/documentation/places/web-service/overview) API.

{{"demo": "GoogleMaps.js"}}

The demo relies on [autosuggest-highlight](https://github.com/moroshko/autosuggest-highlight), a small (1 kB) utility for highlighting text in autosuggest and autocomplete components.

:::error
Before you can start using the Google Maps JavaScript API and Places API, you need to get your own [API key](https://developers.google.com/maps/documentation/javascript/get-api-key).

This demo has limited quotas to make API requests. When your quota exceeds, you will see the response for "Paris".
:::

 Multiple values

Also known as tags, the user is allowed to enter more than one value.

{{"demo": "Tags.js"}}

 Fixed options

In the event that you need to lock certain tags so that they can't be removed, you can set the chips disabled.

{{"demo": "FixedTags.js"}}

 Checkboxes

{{"demo": "CheckboxesTags.js"}}

 Limit tags

You can use the `limitTags` prop to limit the number of displayed options when not focused.

{{"demo": "LimitTags.js"}}

 Sizes

Fancy smaller inputs? Use the `size` prop.

{{"demo": "Sizes.js"}}

 Customization

 Custom input

The `renderInput` prop allows you to customize the rendered input.
The first argument of this render prop contains props that you need to forward.
Pay specific attention to the `ref` and `inputProps` keys.

:::warning
If you're using a custom input component inside the Autocomplete, make sure that you forward the ref to the underlying DOM element.
:::

{{"demo": "CustomInputAutocomplete.js"}}

 Globally Customized Options

To globally customize the Autocomplete options for all components in your app,
you can use the [theme default props](/material-ui/customization/theme-components/##theme-default-props) and set the `renderOption` property in the `defaultProps` key.
The `renderOption` property takes the `ownerState` as the fourth parameter, which includes props and internal component state.
To display the label, you can use the `getOptionLabel` prop from the `ownerState`.
This approach enables different options for each Autocomplete component while keeping the options styling consistent.

{{"demo": "GloballyCustomizedOptions.js"}}

 GitHub's picker

This demo reproduces GitHub's label picker:

{{"demo": "GitHubLabel.js"}}

Head to the [Customized hook](##customized-hook) section for a customization example with the `useAutocomplete` hook instead of the component.

 Hint

The following demo shows how to add a hint feature to the Autocomplete:

{{"demo": "AutocompleteHint.js"}}

 Highlights

The following demo relies on [autosuggest-highlight](https://github.com/moroshko/autosuggest-highlight), a small (1 kB) utility for highlighting text in autosuggest and autocomplete components.

{{"demo": "Highlights.js"}}

 Custom filter

The component exposes a factory to create a filter method that can be provided to the `filterOptions` prop.
You can use it to change the default option filter behavior.

```js
import { createFilterOptions } from '@mui/material/Autocomplete';
```

 `createFilterOptions(config) => filterOptions`

 Arguments

1. `config` (_object_ [optional]):

- `config.ignoreAccents` (_bool_ [optional]): Defaults to `true`. Remove diacritics.
- `config.ignoreCase` (_bool_ [optional]): Defaults to `true`. Lowercase everything.
- `config.limit` (_number_ [optional]): Default to null. Limit the number of suggested options to be shown. For example, if `config.limit` is `100`, only the first `100` matching options are shown. It can be useful if a lot of options match and virtualization wasn't set up.
- `config.matchFrom` (_'any' | 'start'_ [optional]): Defaults to `'any'`.
- `config.stringify` (_func_ [optional]): Controls how an option is converted into a string so that it can be matched against the input text fragment.
- `config.trim` (_bool_ [optional]): Defaults to `false`. Remove trailing spaces.

 Returns

`filterOptions`: the returned filter method can be provided directly to the `filterOptions` prop of the `Autocomplete` component, or the parameter of the same name for the hook.

In the following demo, the options need to start with the query prefix:

```jsx
const filterOptions = createFilterOptions({
  matchFrom: 'start',
  stringify: (option) => option.title,
});

<Autocomplete filterOptions={filterOptions} />;
```

{{"demo": "Filter.js", "defaultCodeOpen": false}}

 Advanced

For richer filtering mechanisms, like fuzzy matching, it's recommended to look at [match-sorter](https://github.com/kentcdodds/match-sorter). For instance:

```jsx
import { matchSorter } from 'match-sorter';

const filterOptions = (options, { inputValue }) => matchSorter(options, inputValue);

<Autocomplete filterOptions={filterOptions} />;
```

 Virtualization

Search within 10,000 randomly generated options. The list is virtualized thanks to [react-window](https://github.com/bvaughn/react-window).

{{"demo": "Virtualize.js"}}

 Events

If you would like to prevent the default key handler behavior, you can set the event's `defaultMuiPrevented` property to `true`:

```jsx
<Autocomplete
  onKeyDown={(event) => {
    if (event.key === 'Enter') {
      // Prevent's default 'Enter' behavior.
      event.defaultMuiPrevented = true;
      // your handler code
    }
  }}
/>
```

 Limitations

 autocomplete/autofill

Browsers have heuristics to help the user fill in form inputs.
However, this can harm the UX of the component.

By default, the component disables the input **autocomplete** feature (remembering what the user has typed for a given field in a previous session) with the `autoComplete="off"` attribute.
Google Chrome does not currently support this attribute setting ([Issue 41239842](https://issues.chromium.org/issues/41239842)).
A possible workaround is to remove the `id` to have the component generate a random one.

In addition to remembering past entered values, the browser might also propose **autofill** suggestions (saved login, address, or payment details).
In the event you want the avoid autofill, you can try the following:

- Name the input without leaking any information the browser can use. For example `id="field1"` instead of `id="country"`. If you leave the id empty, the component uses a random id.
- Set `autoComplete="new-password"` (some browsers will suggest a strong password for inputs with this attribute setting):

  ```jsx
  <TextField
    {...params}
    inputProps={{
      ...params.inputProps,
      autoComplete: 'new-password',
    }}
  />
  ```

Read [the guide on MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/Turning_off_form_autocompletion) for more details.

 iOS VoiceOver

VoiceOver on iOS Safari doesn't support the `aria-owns` attribute very well.
You can work around the issue with the `disablePortal` prop.

 ListboxComponent

If you provide a custom `ListboxComponent` prop, you need to make sure that the intended scroll container has the `role` attribute set to `listbox`. This ensures the correct behavior of the scroll, for example when using the keyboard to navigate.

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/)

We encourage the usage of a label for the textbox.
The component implements the WAI-ARIA authoring practices.

## Avatar

<p class="description">Avatars are found throughout material design with uses in everything from tables to dialog menus.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Image avatars

Image avatars can be created by passing standard `img` props `src` or `srcSet` to the component.

{{"demo": "ImageAvatars.js"}}

 Letter avatars

Avatars containing simple characters can be created by passing a string as `children`.

{{"demo": "LetterAvatars.js"}}

You can use different background colors for the avatar.
The following demo generates the color based on the name of the person.

{{"demo": "BackgroundLetterAvatars.js"}}

 Sizes

You can change the size of the avatar with the `height` and `width` CSS properties.

{{"demo": "SizeAvatars.js"}}

 Icon avatars

Icon avatars are created by passing an icon as `children`.

{{"demo": "IconAvatars.js"}}

 Variants

If you need square or rounded avatars, use the `variant` prop.

{{"demo": "VariantAvatars.js"}}

 Fallbacks

If there is an error loading the avatar image, the component falls back to an alternative in the following order:

- the provided children
- the first letter of the `alt` text
- a generic avatar icon

{{"demo": "FallbackAvatars.js"}}

 Grouped

`AvatarGroup` renders its children as a stack. Use the `max` prop to limit the number of avatars.

{{"demo": "GroupAvatars.js"}}

 Total avatars

If you need to control the total number of avatars not shown, you can use the `total` prop.

{{"demo": "TotalAvatars.js"}}

 Custom surplus

Set the `renderSurplus` prop as a callback to customize the surplus avatar. The callback will receive the surplus number as an argument based on the children and the `max` prop, and should return a `React.ReactNode`.

The `renderSurplus` prop is useful when you need to render the surplus based on the data sent from the server.

{{"demo": "CustomSurplusAvatars.js"}}

 Spacing

You can change the spacing between avatars using the `spacing` prop. You can use one of the presets (`"medium"`, the default, or `"small"`) or set a custom numeric value.

{{"demo": "Spacing.js"}}

 With badge

{{"demo": "BadgeAvatars.js"}}

## Backdrop

<p class="description">The Backdrop component narrows the user's focus to a particular element on the screen.</p>

The Backdrop signals a state change within the application and can be used for creating loaders, dialogs, and more.
In its simplest form, the Backdrop component will add a dimmed layer over your application.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Example

The demo below shows a basic Backdrop with a Circular Progress component in the foreground to indicate a loading state.
After clicking **Show Backdrop**, you can click anywhere on the page to close it.

{{"demo": "SimpleBackdrop.js"}}

## Badge

<p class="description">Badge generates a small badge to the top-right of its child(ren).</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic badge

Examples of badges containing text, using primary and secondary colors. The badge is applied to its children.

{{"demo": "SimpleBadge.js"}}

 Color

Use `color` prop to apply theme palette to component.

{{"demo": "ColorBadge.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedBadges.js"}}

 Badge visibility

The visibility of badges can be controlled using the `invisible` prop.

{{"demo": "BadgeVisibility.js"}}

The badge hides automatically when `badgeContent` is zero. You can override this with the `showZero` prop.

{{"demo": "ShowZeroBadge.js"}}

 Maximum value

You can use the `max` prop to cap the value of the badge content.

{{"demo": "BadgeMax.js"}}

 Dot badge

The `dot` prop changes a badge into a small dot. This can be used as a notification that something has changed without giving a count.

{{"demo": "DotBadge.js"}}

 Badge overlap

You can use the `overlap` prop to place the badge relative to the corner of the wrapped element.

{{"demo": "BadgeOverlap.js"}}

 Badge alignment

You can use the `anchorOrigin` prop to move the badge to any corner of the wrapped element.

{{"demo": "BadgeAlignment.js", "hideToolbar": true}}

 Accessibility

You can't rely on the content of the badge to be announced correctly.
You should provide a full description, for instance, with `aria-label`:

{{"demo": "AccessibleBadges.js"}}

## Bottom Navigation

<p class="description">The Bottom Navigation bar allows movement between primary destinations in an app.</p>

Bottom navigation bars display three to five destinations at the bottom of a screen. Each destination is represented by an icon and an optional text label. When a bottom navigation icon is tapped, the user is taken to the top-level navigation destination associated with that icon.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Bottom navigation

When there are only **three** actions, display both icons and text labels at all times.

{{"demo": "SimpleBottomNavigation.js", "bg": true}}

 Bottom navigation with no label

If there are **four** or **five** actions, display inactive views as icons only.

{{"demo": "LabelBottomNavigation.js", "bg": true}}

 Fixed positioning

This demo keeps bottom navigation fixed to the bottom, no matter the amount of content on-screen.

{{"demo": "FixedBottomNavigation.js", "bg": true, "iframe": true, "maxWidth": 600}}

 Third-party routing library

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server.
The `BottomNavigationAction` component provides the `component` prop to handle this use case.
Here is a [more detailed guide](/material-ui/integrations/routing/).

## Box

<p class="description">The Box component is a generic, theme-aware container with access to CSS utilities from MUI System.</p>

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Introduction

The Box component is a generic container for grouping other components.
It's a fundamental building block when working with Material UI—you can think of it as a `<div>` with extra built-in features, like access to your app's theme and the [`sx` prop](/system/getting-started/the-sx-prop/).

 Usage

The Box component differs from other containers available in Material UI in that its usage is intended to be multipurpose and open-ended, just like a `<div>`.
Components like [Container](/material-ui/react-container/), [Stack](/material-ui/react-stack/) and [Paper](/material-ui/react-paper/), by contrast, feature usage-specific props that make them ideal for certain use cases: Container for main layout orientation, Stack for one-dimensional layouts, and Paper for elevated surfaces.

 Basics

```jsx
import Box from '@mui/material/Box';
```

The Box component renders as a `<div>` by default, but you can swap in any other valid HTML tag or React component using the `component` prop.
The demo below replaces the `<div>` with a `<section>` element:

{{"demo": "BoxBasic.js", "defaultCodeOpen": true }}

 Customization

 With the sx prop

Use the [`sx` prop](/system/getting-started/the-sx-prop/) to quickly customize any Box instance using a superset of CSS that has access to all the style functions and theme-aware properties exposed in the MUI System package.
The demo below shows how to apply colors from the theme using this prop:

{{"demo": "BoxSx.js", "defaultCodeOpen": true }}

 With MUI System props

:::info
System props are deprecated and will be removed in the next major release. Please use the `sx` prop instead.

```diff
- <Box mt={2} />
+ <Box sx={{ mt: 2 }} />
```

:::

 Anatomy

The Box component is composed of a single root `<div>` element:

```html
<div className="MuiBox-root">
  <!-- contents of the Box -->
</div>
```

## Breadcrumbs

<p class="description">A breadcrumbs is a list of links that help visualize a page's location within a site's hierarchical structure, it allows navigation up to any of the ancestors.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic breadcrumbs

{{"demo": "BasicBreadcrumbs.js"}}

 Active last breadcrumb

Keep the last breadcrumb interactive.

{{"demo": "ActiveLastBreadcrumb.js"}}

 Custom separator

In the following examples, we are using two string separators and an SVG icon.

{{"demo": "CustomSeparator.js"}}

 Breadcrumbs with icons

{{"demo": "IconBreadcrumbs.js"}}

 Collapsed breadcrumbs

{{"demo": "CollapsedBreadcrumbs.js"}}

 Condensed with menu

As an alternative, consider adding a Menu component to display the condensed links in a dropdown list:

{{"demo": "CondensedWithMenu.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedBreadcrumbs.js"}}

 Integration with react-router

{{"demo": "RouterBreadcrumbs.js", "bg": true}}

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)

Be sure to add a `aria-label` description on the `Breadcrumbs` component.

The accessibility of this component relies on:

- The set of links is structured using an ordered list (`<ol>` element).
- To prevent screen reader announcement of the visual separators between links, they are hidden with `aria-hidden`.
- A nav element labeled with `aria-label` identifies the structure as a breadcrumb trail and makes it a navigation landmark so that it is easy to locate.

 Toolpad (Beta)

 Page Container

The [PageContainer](https://mui.com/toolpad/core/react-page-container/) component in `@toolpad/core` is the ideal wrapper for the content of your dashboard. It makes the Material UI Container navigation-aware and extends it with page title, breadcrumbs, actions, and more.

{{"demo": "PageContainerBasic.js", "height": 400, "bg": "inline", "defaultExpanded": false}}

## Button Group

<p class="description">The ButtonGroup component can be used to group related buttons.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic button group

The buttons can be grouped by wrapping them with the `ButtonGroup` component.
They need to be immediate children.

{{"demo": "BasicButtonGroup.js"}}

 Button variants

All the standard button variants are supported.

{{"demo": "VariantButtonGroup.js"}}

 Sizes and colors

The `size` and `color` props can be used to control the appearance of the button group.

{{"demo": "GroupSizesColors.js"}}

 Vertical group

The button group can be displayed vertically using the `orientation` prop.

{{"demo": "GroupOrientation.js"}}

 Split button

`ButtonGroup` can also be used to create a split button. The dropdown can change the button action (as in this example) or be used to immediately trigger a related action.

{{"demo": "SplitButton.js"}}

 Disabled elevation

You can remove the elevation with the `disableElevation` prop.

{{"demo": "DisableElevation.js"}}

 Loading

Use the `loading` prop from `Button` to set buttons in a loading state and disable interactions.

{{"demo": "LoadingButtonGroup.js"}}

## Button

<p class="description">Buttons allow users to take actions, and make choices, with a single tap.</p>

Buttons communicate actions that users can take. They are typically placed throughout your UI, in places like:

- Modal windows
- Forms
- Cards
- Toolbars

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic button

The `Button` comes with three variants: text (default), contained, and outlined.

{{"demo": "BasicButtons.js"}}

 Text button

[Text buttons](https://m2.material.io/components/buttons##text-button)
are typically used for less-pronounced actions, including those located: in dialogs, in cards.
In cards, text buttons help maintain an emphasis on card content.

{{"demo": "TextButtons.js"}}

 Contained button

[Contained buttons](https://m2.material.io/components/buttons##contained-button)
are high-emphasis, distinguished by their use of elevation and fill.
They contain actions that are primary to your app.

{{"demo": "ContainedButtons.js"}}

You can remove the elevation with the `disableElevation` prop.

{{"demo": "DisableElevation.js"}}

 Outlined button

[Outlined buttons](https://m2.material.io/components/buttons##outlined-button) are medium-emphasis buttons.
They contain actions that are important but aren't the primary action in an app.

Outlined buttons are also a lower emphasis alternative to contained buttons,
or a higher emphasis alternative to text buttons.

{{"demo": "OutlinedButtons.js"}}

 Handling clicks

All components accept an `onClick` handler that is applied to the root DOM element.

```jsx
<Button
  onClick={() => {
    alert('clicked');
  }}
>
  Click me
</Button>
```

Note that the documentation [avoids](/material-ui/guides/api/##native-properties) mentioning native props (there are a lot) in the API section of the components.

 Color

{{"demo": "ColorButtons.js"}}

In addition to using the default button colors, you can add custom ones, or disable any you don't need. See the [Adding new colors](/material-ui/customization/palette/##custom-colors) examples for more info.

 Sizes

For larger or smaller buttons, use the `size` prop.

{{"demo": "ButtonSizes.js"}}

 Buttons with icons and label

Sometimes you might want to have icons for certain buttons to enhance the UX of the application as we recognize logos more easily than plain text. For example, if you have a delete button you can label it with a dustbin icon.

{{"demo": "IconLabelButtons.js"}}

 Icon button

Icon buttons are commonly found in app bars and toolbars.

Icons are also appropriate for toggle buttons that allow a single choice to be selected or
deselected, such as adding or removing a star to an item.

{{"demo": "IconButtons.js"}}

 Sizes

For larger or smaller icon buttons, use the `size` prop.

{{"demo": "IconButtonSizes.js"}}

 Colors

Use `color` prop to apply theme color palette to component.

{{"demo": "IconButtonColors.js"}}

 Loading

Starting from v6.4.0, use `loading` prop to set icon buttons in a loading state and disable interactions.

{{"demo": "LoadingIconButton.js"}}

 Badge

You can use the [`Badge`](/material-ui/react-badge/) component to add a badge to an `IconButton`.

{{"demo": "IconButtonWithBadge.js"}}

 File upload

To create a file upload button, turn the button into a label using `component="label"` and then create a visually-hidden input with type `file`.

{{"demo": "InputFileUpload.js"}}

 Loading

Starting from v6.4.0, use the `loading` prop to set buttons in a loading state and disable interactions.

{{"demo": "LoadingButtons.js"}}

Toggle the loading switch to see the transition between the different states.

{{"demo": "LoadingButtonsTransition.js"}}

:::warning
When the `loading` prop is set to `boolean`, the loading wrapper is always present in the DOM to prevent a [Google Translation Crash](https://github.com/mui/material-ui/issues/27853).

The `loading` value should always be `null` or `boolean`. The pattern below is not recommended as it can cause the Google Translation crash:

```jsx
<Button {...(isFetching && { loading: true })}> // ❌ Don't do this
```

:::

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedButtons.js", "defaultCodeOpen": false}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/button-introduction--docs).

 Complex button

The Text Buttons, Contained Buttons, Floating Action Buttons and Icon Buttons are built on top of the same component: the `ButtonBase`.
You can take advantage of this lower-level component to build custom interactions.

{{"demo": "ButtonBaseDemo.js"}}

 Third-party routing library

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server.
The `ButtonBase` component provides the `component` prop to handle this use case.
Here is a [more detailed guide](/material-ui/integrations/routing/##button).

 Limitations

 Cursor not-allowed

The ButtonBase component sets `pointer-events: none;` on disabled buttons, which prevents the appearance of a disabled cursor.

If you wish to use `not-allowed`, you have two options:

1. **CSS only**. You can remove the pointer-events style on the disabled state of the `<button>` element:

```css
.MuiButtonBase-root:disabled {
  cursor: not-allowed;
  pointer-events: auto;
}
```

However:

- You should add `pointer-events: none;` back when you need to display [tooltips on disabled elements](/material-ui/react-tooltip/##disabled-elements).
- The cursor won't change if you render something other than a button element, for instance, a link `<a>` element.

2. **DOM change**. You can wrap the button:

```jsx
<span style={{ cursor: 'not-allowed' }}>
  <Button component={Link} disabled>
    disabled
  </Button>
</span>
```

This has the advantage of supporting any element, for instance, a link `<a>` element.

## Card

<p class="description">Cards contain content and actions about a single subject.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Cards are surfaces that display content and actions on a single topic.
The Material UI Card component includes several complementary utility components to handle various use cases:

- Card: a surface-level container for grouping related components.
- Card Content: the wrapper for the Card content.
- Card Header: an optional wrapper for the Card header.
- Card Media: an optional container for displaying images, videos, etc.
- Card Actions: an optional wrapper that groups a set of buttons.
- Card Action Area: an optional wrapper that allows users to interact with the specified area of the Card.

{{"demo": "BasicCard.js", "bg": true}}

 Basics

```jsx
import Card from '@mui/material/Card';
import CardContent from '@mui/material/CardContent';
```

:::success
Although cards can support multiple actions, UI controls, and an overflow menu, use restraint and remember that cards are meant to be entry points to more complex and detailed information.
:::

 Outlined Card

Set `variant="outlined"` to render an outlined card.

{{"demo": "OutlinedCard.js", "bg": true}}

 Complex Interaction

On desktop, card content can expand. (Click the downward chevron to view the recipe.)

{{"demo": "RecipeReviewCard.js", "bg": true}}

 Media

Example of a card using an image to reinforce the content.

{{"demo": "MediaCard.js", "bg": true}}

By default, we use the combination of a `<div>` element and a _background image_ to display the media. It can be problematic in some situations, for example, you might want to display a video or a responsive image. Use the `component` prop for these use cases:

{{"demo": "ImgMediaCard.js", "bg": true}}

 Primary action

Often a card allow users to interact with the entirety of its surface to trigger its main action, be it an expansion, a link to another screen or some other behavior. The action area of the card can be specified by wrapping its contents in a `CardActionArea` component.

{{"demo": "ActionAreaCard.js", "bg": true}}

A card can also offer supplemental actions which should stand detached from the main action area in order to avoid event overlap.

{{"demo": "MultiActionAreaCard.js", "bg": true}}

 UI Controls

Supplemental actions within the card are explicitly called out using icons, text, and UI controls, typically placed at the bottom of the card.

Here's an example of a media control card.

{{"demo": "MediaControlCard.js", "bg": true}}

 Active state styles

To customize a Card's styles when it's in an active state, you can attach a `data-active` attribute to the Card Action Area component and apply styles with the `&[data-active]` selector, as shown below:

{{"demo": "SelectActionCard.js", "bg": true}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/card-introduction--docs).

##checkboxes
githubLabel: 'component: checkbox'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/
githubSource: packages/mui-material/src/Checkbox
---

## Checkbox

<p class="description">Checkboxes allow the user to select one or more items from a set.</p>

Checkboxes can be used to turn an option on or off.

If you have multiple options appearing in a list,
you can preserve space by using checkboxes instead of on/off switches.
If you have a single option, avoid using a checkbox and use an on/off switch instead.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic checkboxes

{{"demo": "Checkboxes.js"}}

 Label

You can provide a label to the `Checkbox` thanks to the `FormControlLabel` component.

{{"demo": "CheckboxLabels.js"}}

 Size

Use the `size` prop or customize the font size of the svg icons to change the size of the checkboxes.

{{"demo": "SizeCheckboxes.js"}}

 Color

{{"demo": "ColorCheckboxes.js"}}

 Icon

{{"demo": "IconCheckboxes.js"}}

 Controlled

You can control the checkbox with the `checked` and `onChange` props:

{{"demo": "ControlledCheckbox.js"}}

 Indeterminate

A checkbox input can only have two states in a form: checked or unchecked.
It either submits its value or doesn't.
Visually, there are **three** states a checkbox can be in: checked, unchecked, or indeterminate.

You can change the indeterminate icon using the `indeterminateIcon` prop.

{{"demo": "IndeterminateCheckbox.js"}}

:::warning
When indeterminate is set, the value of the `checked` prop only impacts the form submitted values.
It has no accessibility or UX implications.
:::

 FormGroup

`FormGroup` is a helpful wrapper used to group selection control components.

{{"demo": "CheckboxesGroup.js"}}

 Label placement

You can change the placement of the label:

{{"demo": "FormControlLabelPosition.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedCheckbox.js"}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/checkbox-introduction--docs).

 When to use

- [Checkboxes vs. Radio Buttons](https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/)
- [Checkboxes vs. Switches](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/)

- All form controls should have labels, and this includes radio buttons, checkboxes, and switches. In most cases, this is done by using the `<label>` element ([FormControlLabel](/material-ui/api/form-control-label/)).
- When a label can't be used, it's necessary to add an attribute directly to the input component.
  In this case, you can apply the additional attribute (for example `aria-label`, `aria-labelledby`, `title`) via the `inputProps` prop.

```jsx
<Checkbox
  value="checkedA"
  inputProps={{
    'aria-label': 'Checkbox A',
  }}
/>
```

## Chip

<p class="description">Chips are compact elements that represent an input, attribute, or action.</p>

Chips allow users to enter information, make selections, filter content, or trigger actions.

While included here as a standalone component, the most common use will
be in some form of input, so some of the behavior demonstrated here is
not shown in context.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic chip

The `Chip` component supports outlined and filled styling.

{{"demo": "BasicChips.js"}}

 Chip actions

You can use the following actions.

- Chips with the `onClick` prop defined change appearance on focus, hover, and click.
- Chips with the `onDelete` prop defined will display a delete icon which changes appearance on hover.

 Clickable

{{"demo": "ClickableChips.js"}}

 Deletable

{{"demo": "DeletableChips.js"}}

 Clickable and deletable

{{"demo": "ClickableAndDeletableChips.js"}}

 Clickable link

{{"demo": "ClickableLinkChips.js"}}

 Custom delete icon

{{"demo": "CustomDeleteIconChips.js"}}

 Chip adornments

You can add ornaments to the beginning of the component.

Use the `avatar` prop to add an avatar or use the `icon` prop to add an icon.

 Avatar chip

{{"demo": "AvatarChips.js"}}

 Icon chip

{{"demo": "IconChips.js"}}

 Color chip

You can use the `color` prop to define a color from theme palette.

{{"demo": "ColorChips.js"}}

 Sizes chip

You can use the `size` prop to define a small Chip.

{{"demo": "SizesChips.js"}}

 Multiline chip

By default, Chips displays labels only in a single line.
To have them support multiline content, use the `sx` prop to add `height:auto` to the Chip component, and `whiteSpace: normal` to the `label` styles.

{{"demo": "MultilineChips.js"}}

 Chip array

An example of rendering multiple chips from an array of values.
Deleting a chip removes it from the array. Note that since no
`onClick` prop is defined, the `Chip` can be focused, but does not
gain depth while clicked or touched.

{{"demo": "ChipsArray.js"}}

 Chip playground

{{"demo": "ChipsPlayground.js", "hideToolbar": true}}

 Accessibility

If the Chip is deletable or clickable then it is a button in tab order. When the Chip is focused (for example when tabbing) releasing (`keyup` event) `Backspace` or `Delete` will call the `onDelete` handler while releasing `Escape` will blur the Chip.

## Click-Away Listener

<p class="description">The Click-Away Listener component detects when a click event happens outside of its child element.</p>

 This document has moved

:::warning
Please refer to the [Click-Away Listener](/base-ui/react-click-away-listener/) component page in the MUI Base docs for demos and details on usage.

Click-Away Listener is a part of the standalone MUI Base component library.
It is currently re-exported from `@mui/material` for your convenience, but it will be removed from this package in a future major version after MUI Base gets a stable release.
:::

## Container

<p class="description">The container centers your content horizontally. It's the most basic layout element.</p>

While containers can be nested, most layouts do not require a nested container.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Fluid

A fluid container width is bounded by the `maxWidth` prop value.

{{"demo": "SimpleContainer.js", "iframe": true, "defaultCodeOpen": false}}

```jsx
<Container maxWidth="sm">
```

 Fixed

If you prefer to design for a fixed set of sizes instead of trying to accommodate a fully fluid viewport, you can set the `fixed` prop.
The max-width matches the min-width of the current breakpoint.

{{"demo": "FixedContainer.js", "iframe": true, "defaultCodeOpen": false}}

```jsx
<Container fixed>
```

 Toolpad (Beta)

 Page Container

The [PageContainer](https://mui.com/toolpad/core/react-page-container/) component in `@toolpad/core` is the ideal wrapper for the content of your dashboard. It makes the Material UI Container navigation-aware and extends it with page title, breadcrumbs, actions, and more.

{{"demo": "../breadcrumbs/PageContainerBasic.js", "height": 400, "bg": "inline", "defaultExpanded": false}}

## CSS Baseline

<p class="description">The CssBaseline component helps to kickstart an elegant, consistent, and simple baseline to build upon.</p>

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Global reset

You might be familiar with [normalize.css](https://github.com/necolas/normalize.css), a collection of HTML element and attribute style-normalizations.

```jsx
import * as React from 'react';
import CssBaseline from '@mui/material/CssBaseline';

export default function MyApp() {
  return (
    <React.Fragment>
      <CssBaseline />
      {/* The rest of your application */}
    </React.Fragment>
  );
}
```

 Scoping on children

However, you might be progressively migrating a website to Material UI, using a global reset might not be an option.
It's possible to apply the baseline only to the children by using the `ScopedCssBaseline` component.

```jsx
import * as React from 'react';
import ScopedCssBaseline from '@mui/material/ScopedCssBaseline';
import MyApp from './MyApp';

export default function MyApp() {
  return (
    <ScopedCssBaseline>
      {/* The rest of your application */}
      <MyApp />
    </ScopedCssBaseline>
  );
}
```

⚠️ Make sure you import `ScopedCssBaseline` first to avoid box-sizing conflicts as in the above example.

 Approach

 Page

The `<html>` and `<body>` elements are updated to provide better page-wide defaults. More specifically:

- The margin in all browsers is removed.
- The default Material Design background color is applied.
  It's using [`theme.palette.background.default`](/material-ui/customization/default-theme/?expand-path=$.palette.background) for standard devices and a white background for print devices.
- If `enableColorScheme` is provided to `CssBaseline`, native components color will be set by applying [`color-scheme`](https://web.dev/articles/color-scheme) on `<html>`.
  The value used is provided by the theme property `theme.palette.mode`.

 Layout

- `box-sizing` is set globally on the `<html>` element to `border-box`.
  Every element—including `*::before` and `*::after` are declared to inherit this property,
  which ensures that the declared width of the element is never exceeded due to padding or border.

 Scrollbars

:::error
This API is deprecated.
Consider using [color-scheme](##color-scheme) instead.
:::

The colors of the scrollbars can be customized to improve the contrast (especially on Windows). Add this code to your theme (for dark mode).

```jsx
import darkScrollbar from '@mui/material/darkScrollbar';

const theme = createTheme({
  components: {
    MuiCssBaseline: {
      styleOverrides: (themeParam) => ({
        body: themeParam.palette.mode === 'dark' ? darkScrollbar() : null,
      }),
    },
  },
});
```

Be aware, however, that using this utility (and customizing `-webkit-scrollbar`) forces macOS to always show the scrollbar.

 Color scheme

This API is introduced in @mui/material (v5.1.0) for switching between `"light"` and `"dark"` modes of native components such as scrollbar, using the `color-scheme` CSS property.
To enable it, you can set `enableColorScheme=true` as follows:

```jsx
<CssBaseline enableColorScheme />

// or

<ScopedCssBaseline enableColorScheme >
  {/* The rest of your application using color-scheme*/}
</ScopedCssBaseline>
```

 Typography

- No base font-size is declared on the `<html>`, but 16px is assumed (the browser default).
  You can learn more about the implications of changing the `<html>` default font size in [the theme documentation](/material-ui/customization/typography/##html-font-size) page.
- Set the `theme.typography.body1` style on the `<body>` element.
- Set the font-weight to `theme.typography.fontWeightBold` for the `<b>` and `<strong>` elements.
- Custom font-smoothing is enabled for better display of the Roboto font.

 Customization

Head to the [global customization](/material-ui/customization/how-to-customize/##4-global-css-override) section of the documentation to change the output of these components.

## Dialog

<p class="description">Dialogs inform users about a task and can contain critical information, require decisions, or involve multiple tasks.</p>

A Dialog is a type of [modal](/material-ui/react-modal/) window that appears in front of app content to provide critical information or ask for a decision. Dialogs disable all app functionality when they appear, and remain on screen until confirmed, dismissed, or a required action has been taken.

Dialogs are purposefully interruptive, so they should be used sparingly.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Dialogs are implemented using a collection of related components:

- Dialog: the parent component that renders the modal.
- Dialog Title: a wrapper used for the title of a Dialog.
- Dialog Actions: an optional container for a Dialog's Buttons.
- Dialog Content: an optional container for displaying the Dialog's content.
- Dialog Content Text: a wrapper for text inside of `<DialogContent />`.
- Slide: optional [Transition](/material-ui/transitions/##slide) used to slide the Dialog in from the edge of the screen.

{{"demo": "SimpleDialogDemo.js"}}

 Basics

```jsx
import Dialog from '@mui/material/Dialog';
import DialogTitle from '@mui/material/DialogTitle';
```

 Alerts

Alerts are urgent interruptions, requiring acknowledgement, that inform the user about a situation.

Most alerts don't need titles.
They summarize a decision in a sentence or two by either:

- Asking a question (for example "Delete this conversation?")
- Making a statement related to the action buttons

Use title bar alerts only for high-risk situations, such as the potential loss of connectivity.
Users should be able to understand the choices based on the title and button text alone.

If a title is required:

- Use a clear question or statement with an explanation in the content area, such as "Erase USB storage?".
- Avoid apologies, ambiguity, or questions, such as "Warning!" or "Are you sure?"

{{"demo": "AlertDialog.js"}}

 Transitions

You can also swap out the transition, the next example uses `Slide`.

{{"demo": "AlertDialogSlide.js"}}

 Form dialogs

Form dialogs allow users to fill out form fields within a dialog.
For example, if your site prompts for potential subscribers to fill in their email address, they can fill out the email field and touch 'Submit'.

{{"demo": "FormDialog.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

The dialog has a close button added to aid usability.

{{"demo": "CustomizedDialogs.js"}}

 Full-screen dialogs

{{"demo": "FullScreenDialog.js"}}

 Optional sizes

You can set a dialog maximum width by using the `maxWidth` enumerable in combination with the `fullWidth` boolean.
When the `fullWidth` prop is true, the dialog will adapt based on the `maxWidth` value.

{{"demo": "MaxWidthDialog.js"}}

 Responsive full-screen

You may make a dialog responsively full screen using [`useMediaQuery`](/material-ui/react-use-media-query/).

```jsx
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const theme = useTheme();
  const fullScreen = useMediaQuery(theme.breakpoints.down('md'));

  return <Dialog fullScreen={fullScreen} />;
}
```

{{"demo": "ResponsiveDialog.js"}}

 Confirmation dialogs

Confirmation dialogs require users to explicitly confirm their choice before an option is committed.
For example, users can listen to multiple ringtones but only make a final selection upon touching "OK".

Touching "Cancel" in a confirmation dialog, cancels the action, discards any changes, and closes the dialog.

{{"demo": "ConfirmationDialog.js"}}

 Non-modal dialog

Dialogs can also be non-modal, meaning they don't interrupt user interaction behind it.
Visit [the Nielsen Norman Group article](https://www.nngroup.com/articles/modal-nonmodal-dialog/) for more in-depth guidance about modal vs. non-modal dialog usage.

The demo below shows a persistent cookie banner, a common non-modal dialog use case.

{{"demo": "CookiesBanner.js", "iframe": true}}

 Draggable dialog

You can create a draggable dialog by using [react-draggable](https://github.com/react-grid-layout/react-draggable).
To do so, you can pass the imported `Draggable` component as the `PaperComponent` of the `Dialog` component.
This will make the entire dialog draggable.

{{"demo": "DraggableDialog.js"}}

 Scrolling long content

When dialogs become too long for the user's viewport or device, they scroll.

- `scroll=paper` the content of the dialog scrolls within the paper element.
- `scroll=body` the content of the dialog scrolls within the body element.

Try the demo below to see what we mean:

{{"demo": "ScrollDialog.js"}}

 Performance

Follow the [Modal performance section](/material-ui/react-modal/##performance).

 Limitations

Follow the [Modal limitations section](/material-ui/react-modal/##limitations).

 Supplementary projects

For more advanced use cases you might be able to take advantage of:

 material-ui-confirm

![stars](https://img.shields.io/github/stars/jonatanklosko/material-ui-confirm?style=social&label=Star)
![npm downloads](https://img.shields.io/npm/dm/material-ui-confirm.svg)

The package [`material-ui-confirm`](https://github.com/jonatanklosko/material-ui-confirm/) provides dialogs for confirming user actions without writing boilerplate code.

 Accessibility

Follow the [Modal accessibility section](/material-ui/react-modal/##accessibility).

 Toolpad (Beta)

 useDialogs

You can create and manipulate dialogs imperatively with the [`useDialogs()`](https://mui.com/toolpad/core/react-use-dialogs/) API in `@toolpad/core`. This hook handles

- state management for opening and closing dialogs
- passing data to dialogs and receiving results back from them
- stacking multiple dialogs
- themed, asynchronous versions of `window.alert()`, `window.confirm()` and `window.prompt()`

The following example demonstrates some of these features:

{{"demo": "ToolpadDialogsNoSnap.js", "defaultCodeOpen": false}}

```tsx
const handleDelete = async () => {
  const id = await dialogs.prompt('Enter the ID to delete', {
    okText: 'Delete',
    cancelText: 'Cancel',
  });

  if (id) {
    const deleteConfirmed = await dialogs.confirm(
      `Are you sure you want to delete "${id}"?`,
    );
    if (deleteConfirmed) {
      try {
        setIsDeleting(true);
        await mockApiDelete(id);
        dialogs.alert('Deleted!');
      } catch (error) {
        const message = error instanceof Error ? error.message : 'Unknown error';
        await dialogs.open(MyCustomDialog, { id, error: message });
      } finally {
        setIsDeleting(false);
      }
    }
  }
};
```

## Divider

<p class="description">The Divider component provides a thin, unobtrusive line for grouping elements to reinforce visual hierarchy.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

The Material UI Divider component renders as a dark gray `<hr>` by default, and features several useful props for quick style adjustments.

{{"demo": "IntroDivider.js", "bg": true}}

 Basics

```jsx
import Divider from '@mui/material/Divider';
```

 Variants

The Divider component supports three variants: `fullWidth` (default), `inset`, and `middle`.

{{"demo": "DividerVariants.js", "bg": true}}

 Orientation

Use the `orientation` prop to change the Divider from horizontal to vertical. When using vertical orientation, the Divider renders a `<div>` with the corresponding accessibility attributes instead of `<hr>` to adhere to the WAI-ARIA [spec](https://www.w3.org/TR/wai-aria-1.2/##separator).

{{"demo": "VerticalDividers.js", "bg": true}}

 Flex item

Use the `flexItem` prop to display the Divider when it's being used in a flex container.

{{"demo": "FlexDivider.js", "bg": true}}

 With children

Use the `textAlign` prop to align elements that are wrapped by the Divider.

{{"demo": "DividerText.js", "bg": true}}

 Customization

 Use with a List

When using the Divider to separate items in a List, use the `component` prop to render it as an `<li>`—otherwise it won't be a valid HTML element.

{{"demo": "ListDividers.js", "bg": true}}

 Icon grouping

The demo below shows how to combine the props `variant="middle"` and `orientation="vertical"`.

{{"demo": "VerticalDividerMiddle.js", "bg": true}}

 Accessibility

Due to its implicit role of `separator`, the Divider, which is a `<hr>` element, will be announced by screen readers as a "Horziontal Splitter" (or vertical, if you're using the `orientation` prop).

If you're using it as a purely stylistic element, we recommend setting `aria-hidden="true"` which will make screen readers bypass it.

```js
<Divider aria-hidden="true" />
```

If you're using the Divider to wrap other elements, such as text or chips, we recommend changing its rendered element to a plain `<div>` using the `component` prop, and setting `role="presentation"`.
This ensures that it's not announced by screen readers while still preserving the semantics of the elements inside it.

```js
<Divider component="div" role="presentation">
  <Typography>Text element</Typography>
</Divider>
```

 Anatomy

The Divider component is composed of a root `<hr>`.

```html
<hr class="MuiDivider-root">
  <!-- Divider children goes here -->
</hr>
```

## Drawer

<p class="description">The navigation drawers (or "sidebars") provide ergonomic access to destinations in a site or app functionality such as switching accounts.</p>

A navigation drawer can either be permanently on-screen or controlled by a navigation menu icon.

[Side sheets](https://m2.material.io/components/sheets-side) are supplementary surfaces primarily used on tablet and desktop.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Temporary drawer

Temporary navigation drawers can toggle open or closed. Closed by default, the drawer opens temporarily above all other content until a section is selected.

The Drawer can be cancelled by clicking the overlay or pressing the Esc key.
It closes when an item is selected, handled by controlling the `open` prop.

{{"demo": "TemporaryDrawer.js"}}

 Anchor

Use the `anchor` prop to specify which side of the screen the Drawer should originate from.

The default value is `left`.

{{"demo": "AnchorTemporaryDrawer.js"}}

 Swipeable

You can make the drawer swipeable with the `SwipeableDrawer` component.

This component comes with a 2 kB gzipped payload overhead.
Some low-end mobile devices won't be able to follow the fingers at 60 FPS.
You can use the `disableBackdropTransition` prop to help.

{{"demo": "SwipeableTemporaryDrawer.js"}}

The following properties are used in this documentation website for optimal usability of the component:

- iOS is hosted on high-end devices.
  The backdrop transition can be enabled without dropping frames.
  The performance will be good enough.
- iOS has a "swipe to go back" feature that interferes
  with the discovery feature, so discovery has to be disabled.

```jsx
const iOS =
  typeof navigator !== 'undefined' && /iPad|iPhone|iPod/.test(navigator.userAgent);

<SwipeableDrawer disableBackdropTransition={!iOS} disableDiscovery={iOS} />;
```

 Swipeable edge

You can configure the `SwipeableDrawer` to have a visible edge when closed.

If you are on a desktop, you can toggle the drawer with the "OPEN" button.
If you are on mobile, you can open the demo in CodeSandbox ("edit" icon) and swipe.

{{"demo": "SwipeableEdgeDrawer.js", "iframe": true, "disableLiveEdit": true, "height": 400, "maxWidth": 300}}

 Keep mounted

The Modal used internally by the Swipeable Drawer has the `keepMounted` prop set by default.
This means that the contents of the drawer are always present in the DOM.

You can change this default behavior with the `ModalProps` prop, but you may encounter issues with `keepMounted: false` in React 18.

```jsx
<Drawer
  variant="temporary"
  ModalProps={{
    keepMounted: false,
  }}
/>
```

 Responsive drawer

You can use the `temporary` variant to display a drawer for small screens and `permanent` for a drawer for wider screens.

{{"demo": "ResponsiveDrawer.js", "iframe": true, "disableLiveEdit": true}}

 Persistent drawer

Persistent navigation drawers can toggle open or closed.
The drawer sits on the same surface elevation as the content.
It is closed by default and opens by selecting the menu icon, and stays open until closed by the user.
The state of the drawer is remembered from action to action and session to session.

When the drawer is outside of the page grid and opens, the drawer forces other content to change size and adapt to the smaller viewport.

Persistent navigation drawers are acceptable for all sizes larger than mobile.
They are not recommended for apps with multiple levels of hierarchy that require using an up arrow for navigation.

{{"demo": "PersistentDrawerLeft.js", "iframe": true}}

{{"demo": "PersistentDrawerRight.js", "iframe": true}}

 Mini variant drawer

In this variation, the persistent navigation drawer changes its width.
Its resting state is as a mini-drawer at the same elevation as the content, clipped by the app bar.
When expanded, it appears as the standard persistent navigation drawer.

The mini variant is recommended for apps sections that need quick selection access alongside content.

{{"demo": "MiniDrawer.js", "iframe": true}}

 Permanent drawer

Permanent navigation drawers are always visible and pinned to the left edge, at the same elevation as the content or background. They cannot be closed.

Permanent navigation drawers are the **recommended default for desktop**.

 Full-height navigation

Apps focused on information consumption that use a left-to-right hierarchy.

{{"demo": "PermanentDrawerLeft.js", "iframe": true}}

{{"demo": "PermanentDrawerRight.js", "iframe": true}}

 Clipped under the app bar

Apps focused on productivity that require balance across the screen.

{{"demo": "ClippedDrawer.js", "iframe": true}}

 Toolpad (Beta)

 Dashboard Layout

The [DashboardLayout](https://mui.com/toolpad/core/react-dashboard-layout/) component from `@toolpad/core` is the starting point for dashboarding applications. It takes care of application layout, theming, navigation, and more. An example usage of this component:

{{"demo": "../app-bar/DashboardLayoutBasic.js", "height": 400, "iframe": true, "bg": "inline", "defaultExpanded": false}}

## Floating Action Button

<p class="description">A Floating Action Button (FAB) performs the primary, or most common, action on a screen.</p>

A floating action button appears in front of all screen content, typically as a circular shape with an icon in its center.
FABs come in two types: regular, and extended.

Only use a FAB if it is the most suitable way to present a screen's primary action.
Only one component is recommended per screen to represent the most common action.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic FAB

{{"demo": "FloatingActionButtons.js"}}

 Size

By default, the size is `large`. Use the `size` prop for smaller floating action buttons.

{{"demo": "FloatingActionButtonSize.js"}}

{{"demo": "FloatingActionButtonExtendedSize.js"}}

 Animation

The floating action button animates onto the screen as an expanding piece of material, by default.

A floating action button that spans multiple lateral screens (such as tabbed screens) should briefly disappear,
then reappear if its action changes.

The Zoom transition can be used to achieve this. Note that since both the exiting and entering
animations are triggered at the same time, we use `enterDelay` to allow the outgoing Floating Action Button's
animation to finish before the new one enters.

{{"demo": "FloatingActionButtonZoom.js", "bg": true}}

## Grid

<p class="description">The Material Design responsive layout grid adapts to screen size and orientation, ensuring consistency across layouts.</p>

The [grid](https://m2.material.io/design/layout/responsive-layout-grid.html) creates visual consistency between layouts while allowing flexibility across a wide variety of designs.
Material Design's responsive UI is based on a 12-column grid layout.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

:::warning
The `Grid` component shouldn't be confused with a data grid; it is closer to a layout grid. For a data grid head to [the `DataGrid` component](/x/react-data-grid/).
:::

:::warning
The `Grid` component has been deprecated. Please use [Grid v2](/material-ui/react-grid2/) instead. See how to migrate in the [Grid v2 migration guide](/material-ui/migration/migration-grid-v2/) and [Material UI v6 upgrade guide](/material-ui/migration/upgrade-to-v6/).
:::

 How it works

The grid system is implemented with the `Grid` component:

- It uses [CSS's Flexible Box module](https://www.w3.org/TR/css-flexbox-1/) for high flexibility.
- There are two types of layout: _containers_ and _items_.
- Item widths are set in percentages, so they're always fluid and sized relative to their parent element.
- Items have padding to create the spacing between individual items.
- There are five grid breakpoints: xs, sm, md, lg, and xl.
- Integer values can be given to each breakpoint, indicating how many of the 12 available columns are occupied by the component when the viewport width satisfies the [breakpoint constraints](/material-ui/customization/breakpoints/##default-breakpoints).

If you are **new to or unfamiliar with flexbox**, we encourage you to read this [CSS-Tricks flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) guide.

 Fluid grids

Fluid grids use columns that scale and resize content. A fluid grid's layout can use breakpoints to determine if the layout needs to change dramatically.

 Basic grid

Column widths are integer values between 1 and 12; they apply at any breakpoint and indicate how many columns are occupied by the component.

A value passed to any given breakpoint also applies to all wider breakpoints (if they have no values explicitly defined).
For example, `xs={12}` sizes a component to occupy the full width of its parent container, regardless of the viewport size.

{{"demo": "BasicGrid.js", "bg": true}}

 Grid with multiple breakpoints

Components may have multiple widths defined, causing the layout to change at the defined breakpoint. Width values given to larger breakpoints override those given to smaller breakpoints.

For example, `xs={12} sm={6}` sizes a component to occupy half of the viewport width (6 columns) when viewport width is [600 or more pixels](/material-ui/customization/breakpoints/##default-breakpoints). For smaller viewports, the component fills all 12 available columns.

{{"demo": "FullWidthGrid.js", "bg": true}}

 Spacing

To control space between children, use the `spacing` prop.
The spacing value can be any positive number, including decimals and any string.
The prop is converted into a CSS property using the [`theme.spacing()`](/material-ui/customization/spacing/) helper.

{{"demo": "SpacingGrid.js", "bg": true}}

 Row & column spacing

The `rowSpacing` and `columnSpacing` props allow for specifying the row and column gaps independently.
It's similar to the `row-gap` and `column-gap` properties of [CSS Grid](/system/grid/##row-gap-amp-column-gap).

{{"demo": "RowAndColumnSpacing.js", "bg": true}}

 Responsive values

You can switch the props' value based on the active breakpoint.
For instance, we can implement the ["recommended"](https://m2.material.io/design/layout/responsive-layout-grid.html) responsive layout grid of Material Design.

{{"demo": "ResponsiveGrid.js", "bg": true}}

Responsive values is supported by:

- `columns`
- `columnSpacing`
- `direction`
- `rowSpacing`
- `spacing`
- all the [other props](##system-props) of MUI System

:::warning
When using a responsive `columns` prop, each grid item needs its corresponding breakpoint.
For instance, this is not working. The grid item misses the value for `md`:

```jsx
<Grid container columns={{ xs: 4, md: 12 }}>
  <Grid item xs={2} />
</Grid>
```

:::

 Interactive

Below is an interactive demo that lets you explore the visual results of the different settings:

{{"demo": "InteractiveGrid.js", "hideToolbar": true, "bg": true}}

 Auto-layout

The Auto-layout makes the _items_ equitably share the available space.
That also means you can set the width of one _item_ and the others will automatically resize around it.

{{"demo": "AutoGrid.js", "bg": true}}

 Variable width content

Set one of the size breakpoint props to `"auto"` instead of `true` / a `number` to size
a column based on the natural width of its content.

{{"demo": "VariableWidthGrid.js", "bg": true}}

 Complex Grid

The following demo doesn't follow the Material Design guidelines, but illustrates how the grid can be used to build complex layouts.

{{"demo": "ComplexGrid.js", "bg": true}}

 Nested Grid

The `container` and `item` props are two independent booleans; they can be combined to allow a Grid component to be both a flex container and child.

:::info
A flex **container** is the box generated by an element with a computed display of `flex` or `inline-flex`. In-flow children of a flex container are called flex **items** and are laid out using the flex layout model.
:::

https://www.w3.org/TR/css-flexbox-1/##box-model

{{"demo": "NestedGrid.js", "bg": true}}

⚠️ Defining an explicit width to a Grid element that is flex container, flex item, and has spacing at the same time leads to unexpected behavior, avoid doing it:

```jsx
<Grid spacing={1} container item xs={12}>
```

If you need to do such, remove one of the props.

 Columns

You can change the default number of columns (12) with the `columns` prop.

{{"demo": "ColumnsGrid.js", "bg": true}}

 Limitations

 Negative margin

The spacing between items is implemented with a negative margin. This might lead to unexpected behaviors. For instance, to apply a background color, you need to apply `display: flex;` to the parent.

 white-space: nowrap

The initial setting on flex items is `min-width: auto`.
This causes a positioning conflict when children use `white-space: nowrap;`.
You can reproduce the issue with:

```jsx
<Grid item xs>
  <Typography noWrap>
```

In order for the item to stay within the container you need to set `min-width: 0`.
In practice, you can set the `zeroMinWidth` prop:

```jsx
<Grid item xs zeroMinWidth>
  <Typography noWrap>
```

{{"demo": "AutoGridNoWrap.js", "bg": true}}

 direction: column | column-reverse

The `xs`, `sm`, `md`, `lg`, and `xl` props are **not supported** within `direction="column"` and `direction="column-reverse"` containers.

They define the number of grids the component will use for a given breakpoint. They are intended to control **width** using `flex-basis` in `row` containers but they will impact height in `column` containers.
If used, these props may have undesirable effects on the height of the `Grid` item elements.

 CSS Grid Layout

The `Grid` component is using CSS flexbox internally.
But as seen below, you can easily use [MUI System](/system/grid/) and CSS Grid to layout your pages.

{{"demo": "CSSGrid.js", "bg": true}}

 System props

:::info
System props are deprecated and will be removed in the next major release. Please use the `sx` prop instead.

```diff
- <Grid item p={2} />
+ <Grid item sx={{ p: 2 }} />
```

:::

## Grid version 2

<p class="description">The responsive layout grid adapts to screen size and orientation, ensuring consistency across layouts.</p>

The `Grid` component works well for a layout with a known number of columns.
The columns can be configured with multiple breakpoints to specify the column span of each child.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 How it works

The grid system is implemented with the `Grid` component:

- It uses [CSS Flexbox](https://www.w3.org/TR/css-flexbox-1/) (rather than CSS Grid) for high flexibility.
- The grid is always a flex item. Use the `container` prop to add a flex container.
- Item widths are set in percentages, so they're always fluid and sized relative to their parent element.
- There are five default grid breakpoints: xs, sm, md, lg, and xl. If you need custom breakpoints, check out [custom breakpoints grid](##custom-breakpoints).
- You can give integer values for each breakpoint, to indicate how many of the 12 available columns are occupied by the component when the viewport width satisfies the [breakpoint constraints](/material-ui/customization/breakpoints/##default-breakpoints).
- It uses [the `gap` CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/gap) to add spacing between items.
- It does _not_ support row spanning. Children elements cannot span multiple rows. We recommend using [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout) if you need this functionality.
- It does _not_ automatically place children. It will try to fit the children one by one, and if there is not enough space, the rest of the children will start on the next line, and so on. If you need auto-placement, we recommend using [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Auto-placement_in_grid_layout) instead.

:::warning
The `Grid` component is a _layout_ grid, not a _data_ grid.
If you need a data grid, check out [the MUI X `DataGrid` component](/x/react-data-grid/).
:::

 Fluid grids

Fluid grids use columns that scale and resize content. A fluid grid's layout can use breakpoints to determine if the layout needs to change dramatically.

 Basic grid

In order to create a grid layout, you need a container.
Use the `container` prop to create a grid container that wraps the grid items (the `Grid` is always an item).

Column widths are integer values between 1 and 12.
For example, an item with `size={6}` occupies half of the grid container's width.

{{"demo": "BasicGrid.js", "bg": true}}

 Multiple breakpoints

Items may have multiple widths defined, causing the layout to change at the defined breakpoint.
Width values apply to all wider breakpoints, and larger breakpoints override those given to smaller breakpoints.

For example, a component with `size={{ xs: 12, sm: 6 }}` occupies the entire viewport width when the viewport is [less than 600 pixels wide](/material-ui/customization/breakpoints/##default-breakpoints).
When the viewport grows beyond this size, the component occupies half of the total width—six columns rather than 12.

{{"demo": "FullWidthGrid.js", "bg": true}}

 Spacing

Use the `spacing` prop to control the space between children.
The spacing value can be any positive number (including decimals) or a string.
The prop is converted into a CSS property using the [`theme.spacing()`](/material-ui/customization/spacing/) helper.

The following demo illustrates the use of the `spacing` prop:

{{"demo": "SpacingGrid.js", "bg": true, "hideToolbar": true}}

 Row and column spacing

The `rowSpacing` and `columnSpacing` props let you specify row and column gaps independently of one another.
They behave similarly to the `row-gap` and `column-gap` properties of [CSS Grid](/system/grid/##row-gap-amp-column-gap).

{{"demo": "RowAndColumnSpacing.js", "bg": true}}

 Responsive values

You can set prop values to change when a given breakpoint is active.
For instance, we can implement Material Design's [recommended](https://m2.material.io/design/layout/responsive-layout-grid.html) responsive layout grid, as seen in the following demo:

{{"demo": "ResponsiveGrid.js", "bg": true}}

Responsive values are supported by:

- `size`
- `columns`
- `columnSpacing`
- `direction`
- `rowSpacing`
- `spacing`
- `offset`

 Interactive

Below is an interactive demo that lets you explore the visual results of the different settings:

{{"demo": "InteractiveGrid.js", "hideToolbar": true, "bg": true}}

 Auto-layout

The auto-layout feature gives equal space to all items present.
When you set the width of one item, the others will automatically resize to match it.

{{"demo": "AutoGrid.js", "bg": true}}

 Variable width content

When a breakpoint's value is given as `"auto"`, then a column's size will automatically adjust to match the width of its content.
The demo below shows how this works:

{{"demo": "VariableWidthGrid.js", "bg": true}}

 Nested grid

The grid container that renders as a **direct child** inside another grid container is a nested grid that inherits its [`columns`](##columns) and [`spacing`](##spacing) from the top level.
It will also inherit the props of the top-level grid if it receives those props.

:::success

Note that a nested grid container should be a direct child of another grid container. If there are non-grid elements in between, the grid container will start as the new root container.

```js
<Grid container>
  <Grid container> // A nested grid container that inherits columns and spacing from above.
    <div>
      <Grid container> // A new root grid container with its own variables scope.
```

:::

 Inheriting spacing

A nested grid container inherits the row and column spacing from its parent unless the `spacing` prop is specified to the instance.

{{"demo": "NestedGrid.js", "bg": true}}

 Inheriting columns

A nested grid container inherits the columns from its parent unless the `columns` prop is specified to the instance.

{{"demo": "NestedGridColumns.js", "bg": true}}

 Columns

Use the `columns` prop to change the default number of columns (12) in the grid, as shown below:

{{"demo": "ColumnsGrid.js", "bg": true}}

 Offset

The `offset` prop pushes an item to the right side of the grid.
This props accepts:

- numbers—for example, `offset={{ md: 2 }}` pushes an item two columns to the right when the viewport size is equal to or greater than the `md` breakpoint.
- `"auto"`—this pushes the item to the far right side of the grid container.

The demo below illustrates how to use the offset props:

{{"demo": "OffsetGrid.js", "bg": true}}

 Custom breakpoints

If you specify custom breakpoints in the theme, you can use those names as grid item props in responsive values:

```js
import { ThemeProvider, createTheme } from '@mui/material/styles';

function Demo() {
  return (
    <ThemeProvider
      theme={createTheme({
        breakpoints: {
          values: {
            laptop: 1024,
            tablet: 640,
            mobile: 0,
            desktop: 1280,
          },
        },
      })}
    >
      <Grid container spacing={{ mobile: 1, tablet: 2, laptop: 3 }}>
        {Array.from(Array(4)).map((_, index) => (
          <Grid key={index} size={{ mobile: 6, tablet: 4, laptop: 3 }}>
            <div>{index + 1}</div>
          </Grid>
        ))}
      </Grid>
    </ThemeProvider>
  );
}
```

:::info
Custom breakpoints affect all [responsive values](##responsive-values).
:::

 TypeScript

You have to set module augmentation on the theme breakpoints interface.

```ts
declare module '@mui/system' {
  interface BreakpointOverrides {
    // Your custom breakpoints
    laptop: true;
    tablet: true;
    mobile: true;
    desktop: true;
    // Remove default breakpoints
    xs: false;
    sm: false;
    md: false;
    lg: false;
    xl: false;
  }
}
```

 Customization

 Centered elements

To center a grid item's content, specify `display="flex"` directly on the item.
Then use `justifyContent` and/or `alignItems` to adjust the position of the content, as shown below:

{{"demo": "CenteredElementGrid.js", "bg": true}}

:::warning
Using the `container` prop does not work in this situation because the grid container is designed exclusively to wrap grid items.
It cannot wrap other elements.
:::

 Full border

{{"demo": "FullBorderedGrid.js"}}

 Half border

{{"demo": "HalfBorderedGrid.js"}}

 Limitations

 Column direction and reversing

The `size` and `offset` props are _not_ supported within containers that use `direction="column"` or `direction="column-reverse"`.

Size and offset props define the number of columns the component will use for a given breakpoint.
They are intended to control the width using `flex-basis` in `row` containers, but they will impact the height in `column` containers.
If used, these props may have undesirable effects on the height of the `Grid` item elements.

## Hidden

:::error
The Hidden component was deprecated in Material UI v5.
To learn more, see [the Hidden section](/material-ui/migration/v5-component-changes/##hidden) of the migration docs.
:::

<p class="description"></p>

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

## Icons

<p class="description">Guidance and suggestions for using icons with Material UI.</p>

Material UI provides icon support in three ways:

1. With [Material Icons](##material-svg-icons) exported as React components (SVG icons).
1. With the [SvgIcon](##svgicon) component, a React wrapper for custom SVG icons.
1. With the [Icon](##icon-font-icons) component, a React wrapper for custom font icons.

 Material SVG icons

Google has created over 2,100 official [Material icons](https://fonts.google.com/icons?icon.set=Material+Icons), each in five different "themes" (see below).
For each SVG icon, we export the respective React component from the `@mui/icons-material` package.
You can [search the full list of these icons](/material-ui/material-icons/).

 Installation

Run one of the following commands to install it and save it to your `package.json` dependencies:

<!-- ##default-branch-switch -->

<codeblock storageKey="package-manager">
```bash npm
npm install @mui/icons-material
```

```bash pnpm
pnpm add @mui/icons-material
```

```bash yarn
yarn add @mui/icons-material
```

</codeblock>

These components use the Material UI `SvgIcon` component to render the SVG path for each icon, and so have a peer-dependency on `@mui/material`.

If you aren't already using Material UI in your project, you can add it following the [installation guide](/material-ui/getting-started/installation/).

 Usage

Import icons using one of these two options:

- Option 1:

  ```jsx
  import AccessAlarmIcon from '@mui/icons-material/AccessAlarm';
  import ThreeDRotation from '@mui/icons-material/ThreeDRotation';
  ```

- Option 2:

  ```jsx
  import { AccessAlarm, ThreeDRotation } from '@mui/icons-material';
  ```

The safest for bundle size is Option 1, but some developers prefer Option 2.
Make sure you follow the [minimizing bundle size guide](/material-ui/guides/minimizing-bundle-size/##option-two-use-a-babel-plugin) before using the second approach.

Each Material icon also has a "theme": Filled (default), Outlined, Rounded, Two-tone, and Sharp. To import the icon component with a theme other than the default, append the theme name to the icon name. For example `@mui/icons-material/Delete` icon with:

- Filled theme (default) is exported as `@mui/icons-material/Delete`,
- Outlined theme is exported as `@mui/icons-material/DeleteOutlined`,
- Rounded theme is exported as `@mui/icons-material/DeleteRounded`,
- Twotone theme is exported as `@mui/icons-material/DeleteTwoTone`,
- Sharp theme is exported as `@mui/icons-material/DeleteSharp`.

:::warning
The Material Design guidelines name the icons using "snake_case" naming (for example `delete_forever`, `add_a_photo`), while `@mui/icons-material` exports the respective icons using "PascalCase" naming (for example `DeleteForever`, `AddAPhoto`). There are three exceptions to this naming rule: `3d_rotation` exported as `ThreeDRotation`, `4k` exported as `FourK`, and `360` exported as `ThreeSixty`.
:::

{{"demo": "SvgMaterialIcons.js"}}

 Testing

For testing purposes, each icon exposed from `@mui/icons-material` has a `data-testid` attribute with the name of the icon. For instance:

```jsx
import DeleteIcon from '@mui/icons-material/Delete';
```

has the following attribute once mounted:

```html
<svg data-testid="DeleteIcon"></svg>
```

 SvgIcon

If you need a custom SVG icon (not available in the [Material Icons](/material-ui/material-icons/)) you can use the `SvgIcon` wrapper.
This component extends the native `<svg>` element:

- It comes with built-in accessibility.
- SVG elements should be scaled for a 24x24px viewport so that the resulting icon can be used as is, or included as a child for other Material UI components that use icons.
  This can be customized with the `viewBox` attribute.
  To inherit the `viewBox` value from the original image, the `inheritViewBox` prop can be used.
- By default, the component inherits the current color. Optionally, you can apply one of the theme colors using the `color` prop.
- It supports `<svg>` element as a child so you can copy and paste your SVG directly to `SvgIcon` component.

{{"demo": "SvgIconChildren.js"}}

 Color

{{"demo": "SvgIconsColor.js"}}

 Size

{{"demo": "SvgIconsSize.js"}}

 Component prop

You can use the `SvgIcon` wrapper even if your icons are saved in the `.svg` format.
[svgr](https://github.com/gregberge/svgr) has loaders to import SVG files and use them as React components. For example, with webpack:

```jsx
// webpack.config.js
{
  test: /\.svg$/,
  use: ['@svgr/webpack'],
}

// ---
import StarIcon from './star.svg';

<SvgIcon component={StarIcon} inheritViewBox />
```

It's also possible to use it with "url-loader" or "file-loader". This is the approach used by Create React App.

```jsx
// webpack.config.js
{
  test: /\.svg$/,
  use: ['@svgr/webpack', 'url-loader'],
}

// ---
import { ReactComponent as StarIcon } from './star.svg';

<SvgIcon component={StarIcon} inheritViewBox />
```

 createSvgIcon

The `createSvgIcon` utility component is used to create the [Material Icons](##material-icons). It can be used to wrap an `<svg>` element or an SVG path which is passed as a child to the [`SvgIcon`](##svgicon) component.

```jsx
const HomeIcon = createSvgIcon(
  <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />,
  'Home',
);

// or with custom SVG
const PlusIcon = createSvgIcon(
  <svg
    xmlns="http://www.w3.org/2000/svg"
    fill="none"
    viewBox="0 0 24 24"
    strokeWidth={1.5}
    stroke="currentColor"
    className="h-6 w-6"
  >
    <path strokeLinecap="round" strokeLinejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
  </svg>,
  'Plus',
);
```

{{"demo": "CreateSvgIcon.js"}}

 Font Awesome

If you find that there are layout issues when using FontAwesomeIcon from `@fortawesome/react-fontawesome`, you can try passing the Font Awesome SVG data directly to SvgIcon.

Below is a comparison of the `FontAwesomeIcon` component and a wrapped `SvgIcon` component.

{{"demo": "FontAwesomeSvgIconDemo.js"}}

FontAwesomeIcon's `fullWidth` prop can also be used to approximate the correct dimensions, but it isn't perfect.

 Other libraries

 MDI

[materialdesignicons.com](https://pictogrammers.com/library/mdi/) provides over 2,000 icons.
For the wanted icon, copy the SVG `path` they provide, and use it as the child of the `SvgIcon` component, or with `createSvgIcon()`.

Note: [mdi-material-ui](https://github.com/TeamWertarbyte/mdi-material-ui) has already wrapped each of these SVG icons with the `SvgIcon` component, so you don't have to do it yourself.

 Icon (Font icons)

The `Icon` component will display an icon from any icon font that supports ligatures.
As a prerequisite, you must include one, such as the
[Material Icons font](https://google.github.io/material-design-icons/##icon-font-for-the-web) in your project.
To use an icon simply wrap the icon name (font ligature) with the `Icon` component,
for example:

```jsx
import Icon from '@mui/material/Icon';

<Icon>star</Icon>;
```

By default, an Icon will inherit the current text color.
Optionally, you can set the icon color using one of the theme color properties: `primary`, `secondary`, `action`, `error` & `disabled`.

 Font Material Icons

`Icon` will by default set the correct base class name for the Material Icons font (filled variant).
All you need to do is load the font, for instance, via Google Web Fonts:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/icon?family=Material+Icons"
/>
```

{{"demo": "Icons.js"}}

 Custom font

For other fonts, you can customize the baseline class name using the `baseClassName` prop.
For instance, you can display two-tone icons with Material Design:

```jsx
import Icon from '@mui/material/Icon';

<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css?family=Material+Icons+Two+Tone"
  // Import the two tones MD variant                           ^^^^^^^^
/>;
```

{{"demo": "TwoToneIcons.js"}}

 Global base class name

Modifying the `baseClassName` prop for each component usage is repetitive.
You can change the default prop globally with the theme

```js
const theme = createTheme({
  components: {
    MuiIcon: {
      defaultProps: {
        // Replace the `material-icons` default value.
        baseClassName: 'material-icons-two-tone',
      },
    },
  },
});
```

Then, you can use the two-tone font directly:

```jsx
<Icon>add_circle</Icon>
```

 Font Awesome

[Font Awesome](https://fontawesome.com/icons) can be used with the `Icon` component as follows:

{{"demo": "FontAwesomeIcon.js"}}

Note that the Font Awesome icons weren't designed like the Material Icons (compare the two previous demos).
The fa icons are cropped to use all the space available. You can adjust for this with a global override:

```js
const theme = createTheme({
  components: {
    MuiIcon: {
      styleOverrides: {
        root: {
          // Match 24px = 3 * 2 + 1.125 * 16
          boxSizing: 'content-box',
          padding: 3,
          fontSize: '1.125rem',
        },
      },
    },
  },
});
```

{{"demo": "FontAwesomeIconSize.js"}}

 Font vs. SVGs: Which approach to use?

Both approaches work fine, however, there are some subtle differences, especially in terms of performance and rendering quality.
Whenever possible SVG is preferred as it allows code splitting, supports more icons, and renders faster and better.

For more details, take a look at [why GitHub migrated from font icons to SVG icons](https://github.blog/engineering/delivering-octicons-with-svg/).

 Accessibility

Icons can convey all sorts of meaningful information, so it's important to ensure they are accessible where appropriate.
There are two use cases you'll want to consider:

- **Decorative icons** that are only being used for visual or branding reinforcement.
  If they were removed from the page, users would still understand and be able to use your page.
- **Semantic icons** are ones that you're using to convey meaning, rather than just pure decoration.
  This includes icons without text next to them that are used as interactive controls — buttons, form elements, toggles, etc.

 Decorative icons

If your icons are purely decorative, you're already done!
The `aria-hidden=true` attribute is added so that your icons are properly accessible (invisible).

 Semantic icons

 Semantic SVG icons

You should include the `titleAccess` prop with a meaningful value.
The `role="img"` attribute and the `<title>` element are added so that your icons are correctly accessible.

In the case of focusable interactive elements, for example when used with an icon button, you can use the `aria-label` prop:

```jsx
import IconButton from '@mui/material/IconButton';
import SvgIcon from '@mui/material/SvgIcon';

// ...

<IconButton aria-label="delete">
  <SvgIcon>
    <path d="M20 12l-1.41-1.41L13 16.17V4h-2v12.17l-5.58-5.59L4 12l8 8 8-8z" />
  </SvgIcon>
</IconButton>;
```

 Semantic font icons

You need to provide a text alternative that is only visible to assistive technologies.

```jsx
import Box from '@mui/material/Box';
import Icon from '@mui/material/Icon';
import { visuallyHidden } from '@mui/utils';

// ...

<Icon>add_circle</Icon>
<Box component="span" sx={visuallyHidden}>Create a user</Box>
```

 Reference

- https://www.tpgi.com/using-aria-enhance-svg-accessibility/

## Image List

<p class="description">The Image List displays a collection of images in an organized grid.</p>

Image lists represent a collection of items in a repeated pattern. They help improve the visual comprehension of the content they hold.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Standard image list

Standard image lists are best for items of equal importance. They have a uniform container size, ratio, and spacing.

{{"demo": "StandardImageList.js"}}

 Quilted image list

Quilted image lists emphasize certain items over others in a collection. They create hierarchy using varied container sizes and ratios.

{{"demo": "QuiltedImageList.js"}}

 Woven image list

Woven image lists use alternating container ratios to create a rhythmic layout. A woven image list is best for browsing peer content.

{{"demo": "WovenImageList.js"}}

 Masonry image list

Masonry image lists use dynamically sized container heights that reflect the aspect ratio of each image. This image list is best used for browsing uncropped peer content.

{{"demo": "MasonryImageList.js"}}

 Image list with title bars

This example demonstrates the use of the `ImageListItemBar` to add an overlay to each item.
The overlay can accommodate a `title`, `subtitle` and secondary action - in this example an `IconButton`.

{{"demo": "TitlebarImageList.js"}}

 Title bar below image (standard)

The title bar can be placed below the image.

{{"demo": "TitlebarBelowImageList.js"}}

 Title bar below image (masonry)

{{"demo": "TitlebarBelowMasonryImageList.js"}}

 Custom image list

In this example the items have a customized titlebar, positioned at the top and with a custom gradient `titleBackground`.
The secondary action `IconButton` is positioned on the left. The `gap` prop is used to adjust the gap between items.

{{"demo": "CustomImageList.js", "defaultCodeOpen": false}}

## Links

<p class="description">The Link component allows you to easily customize anchor elements with your theme colors and typography styles.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic links

The Link component is built on top of the [Typography](/material-ui/api/typography/) component, meaning that you can use its props.

{{"demo": "Links.js"}}

However, the Link component has some different default props than the Typography component:

- `color="primary"` as the link needs to stand out.
- `variant="inherit"` as the link will, most of the time, be used as a child of a Typography component.

 Underline

The `underline` prop can be used to set the underline behavior. The default is `always`.

{{"demo": "UnderlineLink.js"}}

 Security

When you use `target="_blank"` with Links, it is [recommended](https://developers.google.com/web/tools/lighthouse/audits/noopener) to always set `rel="noopener"` or `rel="noreferrer"` when linking to third party content.

- `rel="noopener"` prevents the new page from being able to access the `window.opener` property and ensures it runs in a separate process.
  Without this, the target page can potentially redirect your page to a malicious URL.
- `rel="noreferrer"` has the same effect, but also prevents the _Referer_ header from being sent to the new page.
  ⚠️ Removing the referrer header will affect analytics.

 Third-party routing library

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server.
The `Link` component provides the `component` prop to handle this use case.
Here is a [more detailed guide](/material-ui/integrations/routing/##link).

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/link/)

- When providing the content for the link, avoid generic descriptions like "click here" or "go to".
  Instead, use [specific descriptions](https://developers.google.com/web/tools/lighthouse/audits/descriptive-link-text).
- For the best user experience, links should stand out from the text on the page. For instance, you can keep the default `underline="always"` behavior.
- If a link doesn't have a meaningful href, [it should be rendered using a `<button>` element](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/HEAD/docs/rules/anchor-is-valid.md).
  The demo below illustrates how to properly link with a `<button>`:

{{"demo": "ButtonLink.js"}}

 Keyboard accessibility

- Interactive elements should receive focus in a coherent order when the user presses the <kbd class="key">Tab</kbd> key.
- Users should be able to open a link by pressing <kbd class="key">Enter</kbd>.

 Screen reader accessibility

- When a link receives focus, screen readers should announce a descriptive link name.
  If the link opens in a new window or browser tab, add an [`aria-label`](https://www.w3.org/WAI/WCAG22/Techniques/aria/ARIA8) to inform screen reader users—for example, _"To learn more, visit the About page which opens in a new window."_

## Lists

<p class="description">Lists are continuous, vertical indexes of text or images.</p>

Lists are a continuous group of text or images. They are composed of items containing primary and supplemental actions, which are represented by icons and text.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Lists present information in a concise, easy-to-follow format through a continuous, vertical index of text or images.

Material UI Lists are implemented using a collection of related components:

- List: a wrapper for list items. Renders as a `<ul>` by default.
- List Item: a common list item. Renders as an `<li>` by default.
- List Item Button: an action element to be used inside a list item.
- List Item Icon: an icon to be used inside of a list item.
- List Item Avatar: an avatar to be used inside of a list item.
- List Item Text: a container inside a list item, used to display text content.
- List Divider: a separator between list items.
- List Subheader: a label for a nested list.

{{"demo": "BasicList.js", "bg": true}}

The last item of the previous demo shows how you can render a link:

```jsx
<ListItemButton component="a" href="##simple-list">
  <ListItemText primary="Spam" />
</ListItemButton>
```

You can find a [demo with React Router following this section](/material-ui/integrations/routing/##list) of the documentation.

 Basics

```jsx
import List from '@mui/material/List';
import ListItem from '@mui/material/ListItem';
```

 Nested List

{{"demo": "NestedList.js", "bg": true}}

 Folder List

{{"demo": "FolderList.js", "bg": true}}

 Interactive

Below is an interactive demo that lets you explore the visual results of the different settings:

{{"demo": "InteractiveList.js", "bg": true}}

 Selected ListItem

{{"demo": "SelectedListItem.js", "bg": true}}

 Align list items

When displaying three lines or more, the avatar is not aligned at the top.
You should set the `alignItems="flex-start"` prop to align the avatar at the top, following the Material Design guidelines:

{{"demo": "AlignItemsList.js", "bg": true}}

 List Controls

 Checkbox

A checkbox can either be a primary action or a secondary action.

The checkbox is the primary action and the state indicator for the list item. The comment button is a secondary action and a separate target.

{{"demo": "CheckboxList.js", "bg": true}}

The checkbox is the secondary action for the list item and a separate target.

{{"demo": "CheckboxListSecondary.js", "bg": true}}

 Switch

The switch is the secondary action and a separate target.

{{"demo": "SwitchListSecondary.js", "bg": true}}

 Sticky subheader

Upon scrolling, subheaders remain pinned to the top of the screen until pushed off screen by the next subheader.
This feature relies on CSS sticky positioning.

{{"demo": "PinnedSubheaderList.js", "bg": true}}

 Inset List Item

The `inset` prop enables a list item that does not have a leading icon or avatar to align correctly with items that do.

{{"demo": "InsetList.js", "bg": true}}

 Gutterless list

When rendering a list within a component that defines its own gutters, `ListItem` gutters can be disabled with `disableGutters`.

{{"demo": "GutterlessList.js", "bg": true}}

 Virtualized List

In the following example, we demonstrate how to use [react-window](https://github.com/bvaughn/react-window) with the `List` component.
It renders 200 rows and can easily handle more.
Virtualization helps with performance issues.

{{"demo": "VirtualizedList.js", "bg": true}}

The use of [react-window](https://github.com/bvaughn/react-window) when possible is encouraged.
If this library doesn't cover your use case, you should consider using alternatives like [react-virtuoso](https://github.com/petyosi/react-virtuoso).

 Customization

Here are some examples of customizing the component.
You can learn more about this in the
[overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedList.js"}}

## Masonry

<p class="description">Masonry lays out contents of varying dimensions as blocks of the same width and different height with configurable gaps.</p>

Masonry maintains a list of content blocks with a consistent width but different height.
The contents are ordered by row.
If a row is already filled with the specified number of columns, the next item starts another row, and it is added to the shortest column in order to optimize the use of space.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Basic masonry

A simple example of a `Masonry`. `Masonry` is a container for one or more items. It can receive any element including `<div />` and `<img />`.

{{"demo": "BasicMasonry.js", "bg": true}}

 Image masonry

This example demonstrates the use of `Masonry` for images. `Masonry` orders its children by row.
If you'd like to order images by column, check out [ImageList](/material-ui/react-image-list/##masonry-image-list).

{{"demo": "ImageMasonry.js", "bg": true}}

 Items with variable height

This example demonstrates the use of `Masonry` for items with variable height.
Items can move to other columns in order to abide by the rule that items are always added to the shortest column and hence optimize the use of space.

{{"demo": "MasonryWithVariableHeightItems.js", "bg": true}}

 Columns

This example demonstrates the use of the `columns` to configure the number of columns of a `Masonry`.

{{"demo": "FixedColumns.js", "bg": true}}

`columns` accepts responsive values:

{{"demo": "ResponsiveColumns.js", "bg": true}}

 Spacing

This example demonstrates the use of the `spacing` to configure the spacing between items.
It is important to note that the value provided to the `spacing` prop is multiplied by the theme's spacing field.

{{"demo": "FixedSpacing.js", "bg": true}}

`spacing` accepts responsive values:

{{"demo": "ResponsiveSpacing.js", "bg": true}}

 Sequential

This example demonstrates the use of the `sequential` to configure the sequential order.
With `sequential` enabled, items are added in order from left to right rather than adding to the shortest column.

{{"demo": "Sequential.js", "bg": true}}

 Server-side rendering

This example demonstrates the use of the `defaultHeight`, `defaultColumns` and `defaultSpacing`, which are used to
support server-side rendering.

:::info
`defaultHeight` should be large enough to render all rows. Also, it is worth mentioning that items are not added to the shortest column in case of server-side rendering.
:::

{{"demo": "SSRMasonry.js", "bg": true}}

## Material Icons

<p class="description">2,100+ ready-to-use React Material Icons from the official website.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}
<br/>

[@mui/icons-material](https://www.npmjs.com/package/@mui/icons-material)
includes the 2,100+ official [Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons) converted to [`SvgIcon`](/material-ui/api/svg-icon/) components.
It depends on `@mui/material`, which requires Emotion packages.
Use one of the following commands to install it:

<!-- ##default-branch-switch -->

<codeblock storageKey="package-manager">

```bash npm
npm install @mui/icons-material @mui/material @emotion/styled @emotion/react
```

```bash pnpm
pnpm add @mui/icons-material @mui/material @emotion/styled @emotion/react
```

```bash yarn
yarn add @mui/icons-material @mui/material @emotion/styled @emotion/react
```

</codeblock>

See the [Installation](/material-ui/getting-started/installation/) page for additional docs about how to make sure everything is set up correctly.

:::info
Google also offers [Material Symbols](https://fonts.google.com/icons?icon.set=Material+Symbols) as the successor of Material Icons. `@mui/icons-material` only covers Icons at this time, there are no support for Symbols yet.
:::

<hr/>

 Search Material Icons

Browse through the icons below to find the one you need.
The search field supports synonyms—for example, try searching for "hamburger" or "logout."

{{"demo": "SearchIcons.js", "hideToolbar": true, "bg": true}}

## Menu

<p class="description">Menus display a list of choices on temporary surfaces.</p>

A menu displays a list of choices on a temporary surface. It appears when the user interacts with a button, or other control.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Menus are implemented using a collection of related components:

- Menu: The container/surface of the menu.
- Menu Item: An option for users to select from the menu.
- Menu List (optional): Alternative composable container for Menu Items—see [Composition with Menu List](##composition-with-menu-list) for details.

 Basic menu

A basic menu opens over the anchor element by default (this option can be [changed](##menu-positioning) via props). When close to a screen edge, a basic menu vertically realigns to make sure that all menu items are completely visible.

You should configure the component so that selecting an option immediately confirms it and closes the menu, as shown in the demo below.

{{"demo": "BasicMenu.js"}}

 Icon menu

In desktop viewport, padding is increased to give more space to the menu.

{{"demo": "IconMenu.js", "bg": true}}

 Dense menu

For the menu that has long list and long text, you can use the `dense` prop to reduce the padding and text size.

{{"demo": "DenseMenu.js", "bg": true}}

 Selected menu

If used for item selection, when opened, simple menus places the initial focus on the selected menu item.
The currently selected menu item is set using the `selected` prop (from [ListItem](/material-ui/api/list-item/)).
To use a selected menu item without impacting the initial focus, set the `variant` prop to "menu".

{{"demo": "SimpleListMenu.js"}}

 Positioned menu

Because the `Menu` component uses the `Popover` component to position itself, you can use the same [positioning props](/material-ui/react-popover/##anchor-playground) to position it.
For instance, you can display the menu on top of the anchor:

{{"demo": "PositionedMenu.js"}}

 Composition with Menu List

The Menu component uses the Popover component internally.
But you might want to use a different positioning strategy, or prefer not to block scrolling, for example.

The Menu List component lets you compose your own menu for these kinds of use cases—its primary purpose is to handle focus.
See the demo below for an example of composition that uses Menu List and replaces the Menu's default Popover with a Popper component instead:

{{"demo": "MenuListComposition.js", "bg": true}}

 Account menu

`Menu` content can be mixed with other components like `Avatar`.

{{"demo": "AccountMenu.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedMenus.js"}}

The `MenuItem` is a wrapper around `ListItem` with some additional styles.
You can use the same list composition features with the `MenuItem` component:

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/menu-introduction--docs).

 Max height menu

If the height of a menu prevents all menu items from being displayed, the menu can scroll internally.

{{"demo": "LongMenu.js"}}

 Limitations

There is [a flexbox bug](https://issues.chromium.org/issues/40344463) that prevents `text-overflow: ellipsis` from working in a flexbox layout.
You can use the `Typography` component with `noWrap` to workaround this issue:

{{"demo": "TypographyMenu.js", "bg": true}}

 Change transition

Use a different transition.

{{"demo": "FadeMenu.js"}}

 Context menu

Here is an example of a context menu. (Right click to open.)

{{"demo": "ContextMenu.js"}}

 Supplementary projects

For more advanced use cases you might be able to take advantage of:

 material-ui-popup-state

![stars](https://img.shields.io/github/stars/jcoreio/material-ui-popup-state?style=social&label=Star)
![npm downloads](https://img.shields.io/npm/dm/material-ui-popup-state.svg)

The package [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) that takes care of menu state for you in most cases.

{{"demo": "MenuPopupState.js"}}

## Modal

<p class="description">The modal component provides a solid foundation for creating dialogs, popovers, lightboxes, or whatever else.</p>

The component renders its `children` node in front of a backdrop component.
The `Modal` offers important features:

- 💄 Manages modal stacking when one-at-a-time just isn't enough.
- 🔐 Creates a backdrop, for disabling interaction below the modal.
- 🔐 It disables scrolling of the page content while open.
- ♿️ It properly manages focus; moving to the modal content,
  and keeping it there until the modal is closed.
- ♿️ Adds the appropriate ARIA roles automatically.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

:::info
The term "modal" is sometimes used to mean "dialog", but this is a misnomer.
A modal window describes parts of a UI.
An element is considered modal if [it blocks interaction with the rest of the application](https://en.wikipedia.org/wiki/Modal_window).
:::

If you are creating a modal dialog, you probably want to use the [Dialog](/material-ui/react-dialog/) component rather than directly using Modal.
Modal is a lower-level construct that is leveraged by the following components:

- [Dialog](/material-ui/react-dialog/)
- [Drawer](/material-ui/react-drawer/)
- [Menu](/material-ui/react-menu/)
- [Popover](/material-ui/react-popover/)

 Basic modal

{{"demo": "BasicModal.js"}}

Notice that you can disable the outline (often blue or gold) with the `outline: 0` CSS property.

 Nested modal

Modals can be nested, for example a select within a dialog, but stacking of more than two modals, or any two modals with a backdrop is discouraged.

{{"demo": "NestedModal.js"}}

 Transitions

The open/close state of the modal can be animated with a transition component.
This component should respect the following conditions:

- Be a direct child descendent of the modal.
- Have an `in` prop. This corresponds to the open/close state.
- Call the `onEnter` callback prop when the enter transition starts.
- Call the `onExited` callback prop when the exit transition is completed.
  These two callbacks allow the modal to unmount the child content when closed and fully transitioned.

Modal has built-in support for [react-transition-group](https://github.com/reactjs/react-transition-group).

{{"demo": "TransitionsModal.js"}}

Alternatively, you can use [react-spring](https://github.com/pmndrs/react-spring).

{{"demo": "SpringModal.js"}}

 Performance

The content of modal is unmounted when closed.
If you need to make the content available to search engines or render expensive component trees inside your modal while optimizing for interaction responsiveness
it might be a good idea to change this default behavior by enabling the `keepMounted` prop:

```jsx
<Modal keepMounted />
```

{{"demo": "KeepMountedModal.js", "defaultCodeOpen": false}}

As with any performance optimization, this is not a silver bullet.
Be sure to identify bottlenecks first, and then try out these optimization strategies.

 Server-side modal

React [doesn't support](https://github.com/facebook/react/issues/13097) the [`createPortal()`](https://react.dev/reference/react-dom/createPortal) API on the server.
In order to display the modal, you need to disable the portal feature with the `disablePortal` prop:

{{"demo": "ServerModal.js"}}

 Limitations

 Focus trap

The modal moves the focus back to the body of the component if the focus tries to escape it.

This is done for accessibility purposes. However, it might create issues.
In the event the users need to interact with another part of the page, for example with a chatbot window, you can disable the behavior:

```jsx
<Modal disableEnforceFocus />
```

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)

- Be sure to add `aria-labelledby="id..."`, referencing the modal title, to the `Modal`.
  Additionally, you may give a description of your modal with the `aria-describedby="id..."` prop on the `Modal`.

  ```jsx
  <Modal aria-labelledby="modal-title" aria-describedby="modal-description">
    <h2 id="modal-title">My Title</h2>
    <p id="modal-description">My Description</p>
  </Modal>
  ```

- The [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/examples/dialog/) can help you set the initial focus on the most relevant element, based on your modal content.
- Keep in mind that a "modal window" overlays on either the primary window or another modal window. Windows under a modal are **inert**. That is, users cannot interact with content outside an active modal window. This might create [conflicting behaviors](##focus-trap).

## No SSR

<p class="description">The No-SSR component defers the rendering of children components from the server to the client.</p>

 This document has moved

:::warning
Please refer to the [No-SSR](/base-ui/react-no-ssr/) component page in the MUI Base docs for demos and details on usage.

No-SSR is a part of the standalone MUI Base component library.
It is currently re-exported from `@mui/material` for your convenience, but it will be removed from this package in a future major version after MUI Base gets a stable release.
:::

## Pagination

<p class="description">The Pagination component enables the user to select a specific page from a range of pages.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic pagination

{{"demo": "BasicPagination.js"}}

 Outlined pagination

{{"demo": "PaginationOutlined.js"}}

 Rounded pagination

{{"demo": "PaginationRounded.js"}}

 Pagination size

{{"demo": "PaginationSize.js"}}

 Buttons

You can optionally enable first-page and last-page buttons, or disable the previous-page and next-page buttons.

{{"demo": "PaginationButtons.js"}}

 Custom icons

It's possible to customize the control icons.

{{"demo": "CustomIcons.js"}}

 Pagination ranges

You can specify how many digits to display either side of current page with the `siblingCount` prop, and adjacent to the start and end page number with the `boundaryCount` prop.

{{"demo": "PaginationRanges.js"}}

 Controlled pagination

{{"demo": "PaginationControlled.js"}}

 Router integration

{{"demo": "PaginationLink.js"}}

 `usePagination`

For advanced customization use cases, a headless `usePagination()` hook is exposed.
It accepts almost the same options as the Pagination component minus all the props
related to the rendering of JSX.
The Pagination component is built on this hook.

```jsx
import usePagination from '@mui/material/usePagination';
```

{{"demo": "UsePagination.js"}}

 Table pagination

The `Pagination` component was designed to paginate a list of arbitrary items when infinite loading isn't used.
It's preferred in contexts where SEO is important, for instance, a blog.

For the pagination of a large set of tabular data, you should use the `TablePagination` component.

{{"demo": "TablePaginationDemo.js"}}

:::warning
Note that the `Pagination` page prop starts at 1 to match the requirement of including the value in the URL, while the `TablePagination` page prop starts at 0 to match the requirement of zero-based JavaScript arrays that come with rendering a lot of tabular data.
:::

You can learn more about this use case in the [table section](/material-ui/react-table/##custom-pagination-options) of the documentation.

 Accessibility

 ARIA

The root node has a role of "navigation" and aria-label "pagination navigation" by default. The page items have an aria-label that identifies the purpose of the item ("go to first page", "go to previous page", "go to page 1" etc.).
You can override these using the `getItemAriaLabel` prop.

 Keyboard

The pagination items are in tab order, with a tabindex of "0".

## Paper

<p class="description">The Paper component is a container for displaying content on an elevated surface.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

In Material Design, surface components and shadow styles are heavily influenced by their real-world physical counterparts.

Material UI implements this concept with the Paper component, a container-like surface that features the [`elevation`](##elevation) prop for pulling box-shadow values from the theme.

:::success
The Paper component is ideally suited for designs that follow [Material Design's elevation system](https://m2.material.io/design/environment/elevation.html##elevation-in-material-design), which is meant to replicate how light casts shadows in the physical world.

If you just need a generic container, you may prefer to use the [Box](/material-ui/react-box/) or [Container](/material-ui/react-container/) components.
:::

{{"demo": "SimplePaper.js", "bg": true}}

 Component

```jsx
import Paper from '@mui/material/Paper';
```

 Customization

 Elevation

Use the `elevation` prop to establish hierarchy through the use of shadows.
The Paper component's default elevation level is `1`.
The prop accepts values from `0` to `24`.
The higher the number, the further away the Paper appears to be from its background.

In dark mode, increasing the elevation also makes the background color lighter.
This is done by applying a semi-transparent gradient with the `background-image` CSS property.

:::warning
The aforementioned dark mode behavior can lead to confusion when overriding the Paper component, because changing the `background-color` property won't affect the lighter shading.
To override it, you must either use a new background value, or customize the values for both `background-color` and `background-image`.
:::

{{"demo": "Elevation.js", "bg": "outlined"}}

 Variants

Set the `variant` prop to `"outlined"` for a flat, outlined Paper with no shadows:

{{"demo": "Variants.js", "bg": true}}

 Corners

The Paper component features rounded corners by default.
Add the `square` prop for square corners:

{{"demo": "SquareCorners.js", "bg": true}}

 Anatomy

The Paper component is composed of a single root `<div>` that wraps around its contents:

```html
<div class="MuiPaper-root">
  <!-- Paper contents -->
</div>
```

## Popover

<p class="description">A Popover can be used to display some content on top of another.</p>

Things to know when using the `Popover` component:

- The component is built on top of the [`Modal`](/material-ui/react-modal/) component.
- The scroll and click away are blocked unlike with the [`Popper`](/material-ui/react-popper/) component.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Basic Popover

{{"demo": "BasicPopover.js"}}

 Anchor playground

Use the radio buttons to adjust the `anchorOrigin` and `transformOrigin` positions.
You can also set the `anchorReference` to `anchorPosition` or `anchorEl`.
When it is `anchorPosition`, the component will, instead of `anchorEl`,
refer to the `anchorPosition` prop which you can adjust to set
the position of the popover.

{{"demo": "AnchorPlayground.js", "hideToolbar": true}}

 Mouse hover interaction

This demo demonstrates how to use the `Popover` component with `mouseenter` and `mouseleave` events to achieve popover behavior.

{{"demo": "MouseHoverPopover.js"}}

 Virtual element

The value of the `anchorEl` prop can be a reference to a fake DOM element.
You need to provide an object with the following interface:

```ts
interface PopoverVirtualElement {
  nodeType: 1;
  getBoundingClientRect: () => DOMRect;
}
```

Highlight part of the text to see the popover:

{{"demo": "VirtualElementPopover.js"}}

For more information on the virtual element's properties, see the following resources:

- [getBoundingClientRect](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)
- [DOMRect](https://drafts.fxtf.org/geometry-1/##domrectreadonly)
- [Node types](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)

:::warning
The usage of a virtual element for the Popover component requires the `nodeType` property.
This is different from virtual elements used for the [`Popper`](/material-ui/react-popper/##virtual-element) or [`Tooltip`](/material-ui/react-tooltip/##virtual-element) components, both of which don't require the property.
:::

 Supplementary projects

For more advanced use cases, you might be able to take advantage of:

 material-ui-popup-state

![stars](https://img.shields.io/github/stars/jcoreio/material-ui-popup-state?style=social&label=Star)
![npm downloads](https://img.shields.io/npm/dm/material-ui-popup-state.svg)

The package [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) that takes care of popover state for you in most cases.

{{"demo": "PopoverPopupState.js"}}

## Popper

<p class="description">A Popper can be used to display some content on top of another. It's an alternative to react-popper.</p>

Some important features of the Popper component:

- 🕷 Popper relies on the 3rd party library ([Popper.js](https://popper.js.org/)) for perfect positioning.
- 💄 It's an alternative API to react-popper. It aims for simplicity.
- Its child element is a [MUI Base Portal](/base-ui/react-portal/) on the body of the document to avoid rendering problems.
  You can disable this behavior with `disablePortal`.
- The scroll isn't blocked like with the [Popover](/material-ui/react-popover/) component.
  The placement of the popper updates with the available area in the viewport.
- Clicking away does not hide the Popper component.
  If you need this behavior, you can use the [MUI Base Click-Away Listener](/base-ui/react-click-away-listener/) - see the example in the [menu documentation section](/material-ui/react-menu/##composition-with-menu-list).
- The `anchorEl` is passed as the reference object to create a new `Popper.js` instance.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Basic Popper

{{"demo": "SimplePopper.js"}}

 Transitions

The open/close state of the popper can be animated with a render prop child and a transition component.
This component should respect the following conditions:

- Be a direct child descendent of the popper.
- Call the `onEnter` callback prop when the enter transition starts.
- Call the `onExited` callback prop when the exit transition is completed.
  These two callbacks allow the popper to unmount the child content when closed and fully transitioned.

Popper has built-in support for [react-transition-group](https://github.com/reactjs/react-transition-group).

{{"demo": "TransitionsPopper.js"}}

Alternatively, you can use [react-spring](https://github.com/pmndrs/react-spring).

{{"demo": "SpringPopper.js"}}

 Positioned popper

{{"demo": "PositionedPopper.js"}}

 Scroll playground

{{"demo": "ScrollPlayground.js", "hideToolbar": true, "bg": true}}

 Virtual element

The value of the `anchorEl` prop can be a reference to a fake DOM element.
You need to create an object shaped like the [`VirtualElement`](https://popper.js.org/docs/v2/virtual-elements/).

Highlight part of the text to see the popper:

{{"demo": "VirtualElementPopper.js"}}

 Supplementary projects

For more advanced use cases you might be able to take advantage of:

 material-ui-popup-state

![stars](https://img.shields.io/github/stars/jcoreio/material-ui-popup-state?style=social&label=Star)
![npm downloads](https://img.shields.io/npm/dm/material-ui-popup-state.svg)

The package [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) that takes care of popper state for you in most cases.

{{"demo": "PopperPopupState.js"}}

## Portal

<p class="description">The Portal component lets you render its children into a DOM node that exists outside of the Portal's own DOM hierarchy.</p>

 This document has moved

:::warning
Please refer to the [Portal](/base-ui/react-portal/) component page in the MUI Base docs for demos and details on usage.

Portal is a part of the standalone MUI Base component library.
It is currently re-exported from `@mui/material` for your convenience, but it will be removed from this package in a future major version after MUI Base gets a stable release.
:::

## Progress

<p class="description">Progress indicators commonly known as spinners, express an unspecified wait time or display the length of a process.</p>

Progress indicators inform users about the status of ongoing processes, such as loading an app, submitting a form, or saving updates.

- **Determinate** indicators display how long an operation will take.
- **Indeterminate** indicators visualize an unspecified wait time.

The animations of the components rely on CSS as much as possible to work even before the JavaScript is loaded.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Circular

 Circular indeterminate

{{"demo": "CircularIndeterminate.js"}}

 Circular color

{{"demo": "CircularColor.js"}}

 Circular size

{{"demo": "CircularSize.js"}}

 Circular determinate

{{"demo": "CircularDeterminate.js"}}

 Interactive integration

{{"demo": "CircularIntegration.js"}}

 Circular with label

{{"demo": "CircularWithValueLabel.js"}}

 Linear

 Linear indeterminate

{{"demo": "LinearIndeterminate.js"}}

 Linear color

{{"demo": "LinearColor.js"}}

 Linear determinate

{{"demo": "LinearDeterminate.js"}}

 Linear buffer

{{"demo": "LinearBuffer.js"}}

 Linear with label

{{"demo": "LinearWithValueLabel.js"}}

 Non-standard ranges

The progress components accept a value in the range 0 - 100. This simplifies things for screen-reader users, where these are the default min / max values. Sometimes, however, you might be working with a data source where the values fall outside this range. Here's how you can easily transform a value in any range to a scale of 0 - 100:

```jsx
// MIN = Minimum expected value
// MAX = Maximum expected value
// Function to normalise the values (MIN / MAX could be integrated)
const normalise = (value) => ((value - MIN) * 100) / (MAX - MIN);

// Example component that utilizes the `normalise` function at the point of render.
function Progress(props) {
  return (
    <React.Fragment>
      <CircularProgress variant="determinate" value={normalise(props.value)} />
      <LinearProgress variant="determinate" value={normalise(props.value)} />
    </React.Fragment>
  );
}
```

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedProgressBars.js", "defaultCodeOpen": false}}

 Delaying appearance

There are [3 important limits](https://www.nngroup.com/articles/response-times-3-important-limits/) to know around response time.
The ripple effect of the `ButtonBase` component ensures that the user feels that the UI is reacting instantaneously.
Normally, no special feedback is necessary during delays of more than 0.1 but less than 1.0 second.
After 1.0 second, you can display a loader to keep user's flow of thought uninterrupted.

{{"demo": "DelayingAppearance.js"}}

 Limitations

 High CPU load

Under heavy load, you might lose the stroke dash animation or see random `CircularProgress` ring widths.
You should run processor intensive operations in a web worker or by batch in order not to block the main rendering thread.

<video autoplay muted loop playsinline width="1082" height="158" style="width: 541px;">
  <source src="/static/material-ui/react-components/progress-heavy-load.mp4" type="video/mp4" />
</video>

When it's not possible, you can leverage the `disableShrink` prop to mitigate the issue.
See [this issue](https://github.com/mui/material-ui/issues/10327).

{{"demo": "CircularUnderLoad.js"}}

 High frequency updates

The `LinearProgress` uses a transition on the CSS transform property to provide a smooth update between different values.
The default transition duration is 200ms.
In the event a parent component updates the `value` prop too quickly, you will at least experience a 200ms delay between the re-render and the progress bar fully updated.

If you need to perform 30 re-renders per second or more, we recommend disabling the transition:

```css
.MuiLinearProgress-bar {
  transition: none;
}
```

##radio-buttons
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/radio/
githubSource: packages/mui-material/src/RadioGroup
---

## Radio Group

<p class="description">The Radio Group allows the user to select one option from a set.</p>

Use radio buttons when the user needs to see all available options.
If available options can be collapsed, consider using a [Select component](/material-ui/react-select/) because it uses less space.

Radio buttons should have the most commonly used option selected by default.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Radio group

`RadioGroup` is a helpful wrapper used to group `Radio` components that provides an easier API, and proper keyboard accessibility to the group.

{{"demo": "RadioButtonsGroup.js"}}

 Direction

To lay out the buttons horizontally, set the `row` prop:

{{"demo": "RowRadioButtonsGroup.js"}}

 Controlled

You can control the radio with the `value` and `onChange` props:

{{"demo": "ControlledRadioButtonsGroup.js"}}

 Standalone radio buttons

`Radio` can also be used standalone, without the RadioGroup wrapper.

{{"demo": "RadioButtons.js"}}

 Size

Use the `size` prop or customize the font size of the svg icons to change the size of the radios.

{{"demo": "SizeRadioButtons.js"}}

 Color

{{"demo": "ColorRadioButtons.js"}}

 Label placement

You can change the placement of the label with the `FormControlLabel` component's `labelPlacement` prop:

{{"demo": "FormControlLabelPlacement.js"}}

 Show error

In general, radio buttons should have a value selected by default. If this is not the case, you can display an error if no value is selected when the form is submitted:

{{"demo": "ErrorRadios.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedRadios.js"}}

 `useRadioGroup`

For advanced customization use cases, a `useRadioGroup()` hook is exposed.
It returns the context value of the parent radio group.
The Radio component uses this hook internally.

 API

```jsx
import { useRadioGroup } from '@mui/material/RadioGroup';
```

 Returns

`value` (_object_):

- `value.name` (_string_ [optional]): The name used to reference the value of the control.
- `value.onChange` (_func_ [optional]): Callback fired when a radio button is selected.
- `value.value` (_any_ [optional]): Value of the selected radio button.

 Example

{{"demo": "UseRadioGroup.js"}}

 When to use

- [Checkboxes vs. Radio Buttons](https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/)

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/radio/)

- All form controls should have labels, and this includes radio buttons, checkboxes, and switches. In most cases, this is done by using the `<label>` element ([FormControlLabel](/material-ui/api/form-control-label/)).

- When a label can't be used, it's necessary to add an attribute directly to the input component.
  In this case, you can apply the additional attribute (for example `aria-label`, `aria-labelledby`, `title`) via the `inputProps` property.

```jsx
<Radio
  value="radioA"
  inputProps={{
    'aria-label': 'Radio A',
  }}
/>
```

##a-star-rating
githubSource: packages/mui-material/src/Rating
---

## Rating

<p class="description">Ratings provide insight regarding others' opinions and experiences, and can allow the user to submit a rating of their own.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic rating

{{"demo": "BasicRating.js"}}

 Rating precision

The rating can display any float number with the `value` prop.
Use the `precision` prop to define the minimum increment value change allowed.

{{"demo": "HalfRating.js"}}

 Hover feedback

You can display a label on hover to help the user pick the correct rating value.
The demo uses the `onChangeActive` prop.

{{"demo": "HoverRating.js"}}

 Sizes

For larger or smaller ratings use the `size` prop.

{{"demo": "RatingSize.js"}}

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedRating.js"}}

 Radio group

The rating is implemented with a radio group, set `highlightSelectedOnly` to restore the natural behavior.

{{"demo": "RadioGroupRating.js"}}

 Accessibility

([WAI tutorial](https://www.w3.org/WAI/tutorials/forms/custom-controls/##a-star-rating))

The accessibility of this component relies on:

- A radio group with its fields visually hidden.
  It contains six radio buttons, one for each star, and another for 0 stars that is checked by default. Be sure to provide a value for the `name` prop that is unique to the parent form.
- Labels for the radio buttons containing actual text ("1 Star", "2 Stars", …).
  Be sure to provide a suitable function to the `getLabelText` prop when the page is in a language other than English. You can use the [included locales](/material-ui/guides/localization/), or provide your own.
- A visually distinct appearance for the rating icons.
  By default, the rating component uses both a difference of color and shape (filled and empty icons) to indicate the value. In the event that you are using color as the only means to indicate the value, the information should also be also displayed as text, as in this demo. This is important to match [success Criterion 1.4.1](https://www.w3.org/TR/WCAG21/##use-of-color) of WCAG2.1.

{{"demo": "TextRating.js"}}

 ARIA

The read only rating has a role of "img", and an aria-label that describes the displayed rating.

 Keyboard

Because the rating component uses radio buttons, keyboard interaction follows the native browser behavior. Tab will focus the current rating, and cursor keys control the selected rating.

The read only rating is not focusable.

##exposed-dropdown-menu
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/examples/combobox-select-only/
unstyled: /base-ui/react-select/
githubSource: packages/mui-material/src/Select
---

## Select

<p class="description">Select components are used for collecting user provided information from a list of options.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic select

Menus are positioned under their emitting elements, unless they are close to the bottom of the viewport.

{{"demo": "BasicSelect.js"}}

 Advanced features

The Select component is meant to be interchangeable with a native `<select>` element.

If you are looking for more advanced features, like combobox, multiselect, autocomplete, async or creatable support, head to the [`Autocomplete` component](/material-ui/react-autocomplete/).
It's meant to be an improved version of the "react-select" and "downshift" packages.

 Props

The Select component is implemented as a custom `<input>` element of the [InputBase](/material-ui/api/input-base/).
It extends the [text field components](/material-ui/react-text-field/) subcomponents, either the [OutlinedInput](/material-ui/api/outlined-input/), [Input](/material-ui/api/input/), or [FilledInput](/material-ui/api/filled-input/), depending on the variant selected.
It shares the same styles and many of the same props. Refer to the respective component's API page for details.

:::warning
Unlike input components, the `placeholder` prop is not available in Select. To add a placeholder, refer to the [placeholder](##placeholder) section below.
:::

 Filled and standard variants

{{"demo": "SelectVariants.js"}}

 Labels and helper text

{{"demo": "SelectLabels.js"}}

:::warning
Note that when using FormControl with the outlined variant of the Select, you need to provide a label in two places: in the InputLabel component and in the `label` prop of the Select component (see the above demo).
:::

 Auto width

{{"demo": "SelectAutoWidth.js"}}

 Small Size

{{"demo": "SelectSmall.js"}}

 Other props

{{"demo": "SelectOtherProps.js"}}

 Native select

As the user experience can be improved on mobile using the native select of the platform,
we allow such pattern.

{{"demo": "NativeSelectDemo.js"}}

 TextField

The `TextField` wrapper component is a complete form control including a label, input and help text.
You can find an example with the select mode [in this section](/material-ui/react-text-field/##select).

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

The first step is to style the `InputBase` component.
Once it's styled, you can either use it directly as a text field or provide it to the select `input` prop to have a `select` field.
Notice that the `"standard"` variant is easier to customize, since it does not wrap the contents in a `fieldset`/`legend` markup.

{{"demo": "CustomizedSelects.js"}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/select-introduction--docs).

 Multiple select

The `Select` component can handle multiple selections.
It's enabled with the `multiple` prop.

Like with the single selection, you can pull out the new value by accessing `event.target.value` in the `onChange` callback. It's always an array.

 Default

{{"demo": "MultipleSelect.js"}}

 Checkmarks

{{"demo": "MultipleSelectCheckmarks.js"}}

 Chip

{{"demo": "MultipleSelectChip.js"}}

 Placeholder

{{"demo": "MultipleSelectPlaceholder.js"}}

 Native

{{"demo": "MultipleSelectNative.js"}}

 Controlling the open state

You can control the open state of the select with the `open` prop. Alternatively, it is also possible to set the initial (uncontrolled) open state of the component with the `defaultOpen` prop.

:::info

- A component is **controlled** when it's managed by its parent using props.
- A component is **uncontrolled** when it's managed by its own local state.

Learn more about controlled and uncontrolled components in the [React documentation](https://react.dev/learn/sharing-state-between-components##controlled-and-uncontrolled-components).
:::

{{"demo": "ControlledOpenSelect.js"}}

 With a dialog

While it's discouraged by the Material Design guidelines, you can use a select inside a dialog.

{{"demo": "DialogSelect.js"}}

 Grouping

Display categories with the `ListSubheader` component or the native `<optgroup>` element.

{{"demo": "GroupedSelect.js"}}

:::warning
If you wish to wrap the ListSubheader in a custom component, you'll have to annotate it so Material UI can handle it properly when determining focusable elements.

You have two options for solving this:
Option 1: Define a static boolean field called `muiSkipListHighlight` on your component function, and set it to `true`:

```tsx
function MyListSubheader(props: ListSubheaderProps) {
  return <ListSubheader {...props} />;
}

MyListSubheader.muiSkipListHighlight = true;
export default MyListSubheader;

// elsewhere:

return (
  <Select>
    <MyListSubheader>Group 1</MyListSubheader>
    <MenuItem value={1}>Option 1</MenuItem>
    <MenuItem value={2}>Option 2</MenuItem>
    <MyListSubheader>Group 2</MyListSubheader>
    <MenuItem value={3}>Option 3</MenuItem>
    <MenuItem value={4}>Option 4</MenuItem>
    {/* ... */}
  </Select>
```

Option 2: Place a `muiSkipListHighlight` prop on each instance of your component.
The prop doesn't have to be forwarded to the ListSubheader, nor present in the underlying DOM element.
It just has to be placed on a component that's used as a subheader.

```tsx
export default function MyListSubheader(
  props: ListSubheaderProps & { muiSkipListHighlight: boolean },
) {
  const { muiSkipListHighlight, ...other } = props;
  return <ListSubheader {...other} />;
}

// elsewhere:

return (
  <Select>
    <MyListSubheader muiSkipListHighlight>Group 1</MyListSubheader>
    <MenuItem value={1}>Option 1</MenuItem>
    <MenuItem value={2}>Option 2</MenuItem>
    <MyListSubheader muiSkipListHighlight>Group 2</MyListSubheader>
    <MenuItem value={3}>Option 3</MenuItem>
    <MenuItem value={4}>Option 4</MenuItem>
    {/* ... */}
  </Select>
);
```

We recommend the first option as it doesn't require updating all the usage sites of the component.

Keep in mind this is **only necessary** if you wrap the ListSubheader in a custom component.
If you use the ListSubheader directly, **no additional code is required**.
:::

 Accessibility

To properly label your `Select` input you need an extra element with an `id` that contains a label.
That `id` needs to match the `labelId` of the `Select`, for example:

```jsx
<InputLabel id="label">Age</InputLabel>
<Select labelId="label" id="select" value="20">
  <MenuItem value="10">Ten</MenuItem>
  <MenuItem value="20">Twenty</MenuItem>
</Select>
```

Alternatively a `TextField` with an `id` and `label` creates the proper markup and
ids for you:

```jsx
<TextField id="select" label="Age" value="20" select>
  <MenuItem value="10">Ten</MenuItem>
  <MenuItem value="20">Twenty</MenuItem>
</TextField>
```

For a [native select](##native-select), you should mention a label by giving the value of the `id` attribute of the select element to the `InputLabel`'s `htmlFor` attribute:

```jsx
<InputLabel htmlFor="select">Age</InputLabel>
<NativeSelect id="select">
  <option value="10">Ten</option>
  <option value="20">Twenty</option>
</NativeSelect>
```

## Skeleton

<p class="description">Display a placeholder preview of your content before the data gets loaded to reduce load-time frustration.</p>

The data for your components might not be immediately available. You can improve the perceived responsiveness of the page by using skeletons. It feels like things are happening immediately, then the information is incrementally displayed on the screen (Cf. [Avoid The Spinner](https://www.lukew.com/ff/entry.asp?1797)).

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Usage

The component is designed to be used **directly in your components**.
For instance:

```jsx
{
  item ? (
    <img
      style={{
        width: 210,
        height: 118,
      }}
      alt={item.title}
      src={item.src}
    />
  ) : (
    <Skeleton variant="rectangular" width={210} height={118} />
  );
}
```

 Variants

The component supports 4 shape variants:

- `text` (default): represents a single line of text (you can adjust the height via font size).
- `circular`, `rectangular`, and `rounded`: come with different border radius to let you take control of the size.

{{"demo": "Variants.js"}}

 Animations

By default, the skeleton pulsates, but you can change the animation to a wave or disable it entirely.

{{"demo": "Animations.js"}}

 Pulsate example

{{"demo": "YouTube.js", "defaultCodeOpen": false}}

 Wave example

{{"demo": "Facebook.js", "defaultCodeOpen": false, "bg": true}}

 Inferring dimensions

In addition to accepting `width` and `height` props, the component can also infer the dimensions.

It works well when it comes to typography as its height is set using `em` units.

```jsx
<Typography variant="h1">{loading ? <Skeleton /> : 'h1'}</Typography>
```

{{"demo": "SkeletonTypography.js", "defaultCodeOpen": false}}

But when it comes to other components, you may not want to repeat the width and
height. In these instances, you can pass `children` and it will
infer its width and height from them.

```jsx
loading ? (
  <Skeleton variant="circular">
    <Avatar />
  </Skeleton>
) : (
  <Avatar src={data.avatar} />
);
```

{{"demo": "SkeletonChildren.js", "defaultCodeOpen": false}}

 Color

The color of the component can be customized by changing its `background-color` CSS property.
This is especially useful when on a black background (as the skeleton will otherwise be invisible).

{{"demo": "SkeletonColor.js", "bg": "inline"}}

 Accessibility

Skeleton screens provide an alternative to the traditional spinner method.
Rather than showing an abstract widget, skeleton screens create anticipation of what is to come and reduce cognitive load.

The background color of the skeleton uses the least amount of luminance to be visible in good conditions (good ambient light, good screen, no visual impairments).

 ARIA

None.

 Keyboard

The skeleton is not focusable.

## Slider

<p class="description">Sliders allow users to make selections from a range of values.</p>

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Continuous sliders

Continuous sliders allow users to select a value along a subjective range.

{{"demo": "ContinuousSlider.js"}}

 Sizes

For smaller slider, use the prop `size="small"`.

{{"demo": "SliderSizes.js"}}

 Discrete sliders

Discrete sliders can be adjusted to a specific value by referencing its value indicator.
You can generate a mark for each step with `marks={true}`.

{{"demo": "DiscreteSlider.js"}}

 Small steps

You can change the default step increment.
Make sure to adjust the `shiftStep` prop (the granularity with which the slider can step when using Page Up/Down or Shift + Arrow Up/Down) to a value divadable with the `step`.

{{"demo": "DiscreteSliderSteps.js"}}

 Custom marks

You can have custom marks by providing a rich array to the `marks` prop.

{{"demo": "DiscreteSliderMarks.js"}}

 Restricted values

You can restrict the selectable values to those provided with the `marks` prop with `step={null}`.

{{"demo": "DiscreteSliderValues.js"}}

 Label always visible

You can force the thumb label to be always visible with `valueLabelDisplay="on"`.

{{"demo": "DiscreteSliderLabel.js"}}

 Range slider

The slider can be used to set the start and end of a range by supplying an array of values to the `value` prop.

{{"demo": "RangeSlider.js"}}

 Minimum distance

You can enforce a minimum distance between values in the `onChange` event handler.
By default, when you move the pointer over a thumb while dragging another thumb, the active thumb will swap to the hovered thumb. You can disable this behavior with the `disableSwap` prop.
If you want the range to shift when reaching minimum distance, you can utilize the `activeThumb` parameter in `onChange`.

{{"demo": "MinimumDistanceSlider.js"}}

 Slider with input field

In this example, an input allows a discrete value to be set.

{{"demo": "InputSlider.js"}}

 Color

{{"demo": "ColorSlider.js"}}

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSlider.js"}}

 Music player

{{"demo": "MusicPlayerSlider.js", "bg": "inline"}}

 Vertical sliders

Set the `orientation` prop to `"vertical"` to create vertical sliders. The thumb will track vertical movement instead of horizontal movement.

{{"demo": "VerticalSlider.js"}}

:::warning
Chrome versions below 124 implement `aria-orientation` incorrectly for vertical sliders and expose them as `'horizontal'` in the accessibility tree. ([Chromium issue ##40736841](https://issues.chromium.org/issues/40736841))

The `-webkit-appearance: slider-vertical` CSS property can be used to correct this for these older versions, with the trade-off of causing a console warning in newer Chrome versions:

```css
.MuiSlider-thumb input {
  -webkit-appearance: slider-vertical;
}
```

:::

 Marks placement

You can customize your slider by adding and repositioning marks for minimum and maximum values.

{{"demo": "CustomMarks.js"}}

 Track

The track shows the range available for user selection.

 Removed track

The track can be turned off with `track={false}`.

{{"demo": "TrackFalseSlider.js"}}

 Inverted track

The track can be inverted with `track="inverted"`.

{{"demo": "TrackInvertedSlider.js"}}

 Non-linear scale

You can use the `scale` prop to represent the `value` on a different scale.

In the following demo, the value _x_ represents the value _2^x_.
Increasing _x_ by one increases the represented value by factor _2_.

{{"demo": "NonLinearSlider.js"}}

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/slider-multithumb/)

The component handles most of the work necessary to make it accessible.
However, you need to make sure that:

- Each thumb has a user-friendly label (`aria-label`, `aria-labelledby` or `getAriaLabel` prop).
- Each thumb has a user-friendly text for its current value.
  This is not required if the value matches the semantics of the label.
  You can change the name with the `getAriaValueText` or `aria-valuetext` prop.

##alert
githubSource: packages/mui-material/src/Snackbar
---

## Snackbar

<p class="description">Snackbars (also known as toasts) are used for brief notifications of processes that have been or will be performed.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

The Snackbar component appears temporarily and floats above the UI to provide users with (non-critical) updates on an app's processes.
The demo below, inspired by Google Keep, shows a basic Snackbar with a text element and two actions:

{{"demo": "SimpleSnackbar.js"}}

 Usage

Snackbars differ from [Alerts](/material-ui/react-alert/) in that Snackbars have a fixed position and a high z-index, so they're intended to break out of the document flow; Alerts, on the other hand, are usually part of the flow—except when they're [used as children of a Snackbar](##use-with-alerts).

Snackbars also from differ from [Dialogs](/material-ui/react-dialog/) in that Snackbars are not intended to convey _critical_ information or block the user from interacting with the rest of the app; Dialogs, by contrast, require input from the user in order to be dismissed.

 Basics

 Import

```jsx
import Snackbar from '@mui/material/Snackbar';
```

 Position

Use the `anchorOrigin` prop to control the Snackbar's position on the screen.

{{"demo": "PositionedSnackbar.js"}}

 Content

```jsx
import SnackbarContent from '@mui/material/SnackbarContent';
```

Use the Snackbar Content component to add text and actions to the Snackbar.

{{"demo": "LongTextSnackbar.js"}}

 Automatic dismiss

Use the `autoHideDuration` prop to automatically trigger the Snackbar's `onClose` function after a set period of time (in milliseconds).

Make sure to [provide sufficient time](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) for the user to process the information displayed on it.

{{"demo": "AutohideSnackbar.js"}}

 Transitions

You can use the `TransitionComponent` prop to change the transition of the Snackbar from [Grow](/material-ui/transitions/##grow) (the default) to others such as [Slide](/material-ui/transitions/##slide).

{{"demo": "TransitionsSnackbar.js"}}

 Customization

 Use with Alerts

Use an Alert inside a Snackbar for messages that communicate a certain severity.

{{"demo": "CustomizedSnackbars.js"}}

 Use with Floating Action Buttons

If you're using a [Floating Action Button](/material-ui/react-floating-action-button/) on mobile, Material Design recommends positioning snackbars directly above it, as shown in the demo below:

{{"demo": "FabIntegrationSnackbar.js", "iframe": true, "maxWidth": 400}}

 Common examples

 Consecutive Snackbars

This demo shows how to display multiple Snackbars without stacking them by using a consecutive animation.

{{"demo": "ConsecutiveSnackbars.js"}}

 Supplementary components

 notistack

![stars](https://img.shields.io/github/stars/iamhosseindhv/notistack.svg?style=social&label=Star)
![npm downloads](https://img.shields.io/npm/dm/notistack.svg)

With an imperative API, [notistack](https://github.com/iamhosseindhv/notistack) lets you vertically stack multiple Snackbars without having to handle their open and close states.
Even though this is discouraged in the Material Design guidelines, it is still a common pattern.

{{"demo": "IntegrationNotistack.js", "defaultCodeOpen": false}}

:::warning
Note that notistack prevents Snackbars from being [closed by pressing <kbd class="key">Escape</kbd>](##accessibility).
:::

 Accessibility

The user should be able to dismiss Snackbars by pressing <kbd class="key">Escape</kbd>. If there are multiple instances appearing at the same time and you want <kbd class="key">Escape</kbd> to dismiss only the oldest one that's currently open, call `event.preventDefault` in the `onClose` prop.

```jsx
export default function MyComponent() {
  const [open, setOpen] = React.useState(true);

  return (
    <React.Fragment>
      <Snackbar
        open={open}
        onClose={(event, reason) => {
          // `reason === 'escapeKeyDown'` if `Escape` was pressed
          setOpen(false);
          // call `event.preventDefault` to only close one Snackbar at a time.
        }}
      />
      <Snackbar open={open} onClose={() => setOpen(false)} />
    </React.Fragment>
  );
}
```

 Anatomy

The Snackbar component is composed of a root `<div>` that houses interior elements like the Snackbar Content and other optional components (such as buttons or decorators).

```html
<div role="presentation" class="MuiSnackbar-root">
  <div class="MuiPaper-root MuiSnackbarContent-root" role="alert">
    <div class="MuiSnackbarContent-message">
      <!-- Snackbar content goes here -->
    </div>
  </div>
</div>
```

 Experimental APIs - Toolpad

 useNotifications

You can create and manipulate notifications imperatively with the [`useNotifications()`](https://mui.com/toolpad/core/react-use-notifications/) API in `@toolpad/core`. This API provides state management for opening and closing snackbars. It also allows for queueing multiple notifications at once.

{{"demo": "ToolpadNotificationsNoSnap.js", "defaultCodeOpen": false}}

##types-of-transitions
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/
githubSource: packages/mui-material/src/SpeedDial
---

## Speed Dial

<p class="description">When pressed, a floating action button can display three to six related actions in the form of a Speed Dial.</p>

If more than six actions are needed, something other than a FAB should be used to present them.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic speed dial

The floating action button can display related actions.

{{"demo": "BasicSpeedDial.js"}}

 Playground

{{"demo": "PlaygroundSpeedDial.js"}}

 Controlled speed dial

The open state of the component can be controlled with the `open`/`onOpen`/`onClose` props.

{{"demo": "ControlledOpenSpeedDial.js"}}

 Custom close icon

You can provide an alternate icon for the closed and open states using the `icon` and `openIcon` props
of the `SpeedDialIcon` component.

{{"demo": "OpenIconSpeedDial.js"}}

 Persistent action tooltips

The SpeedDialActions tooltips can be displayed persistently so that users don't have to long-press to see the tooltip on touch devices.

It is enabled here across all devices for demo purposes, but in production it could use the `isTouch` logic to conditionally set the prop.

{{"demo": "SpeedDialTooltipOpen.js"}}

 Accessibility

 ARIA

 Required

- You should provide an `ariaLabel` for the speed dial component.
- You should provide a `tooltipTitle` for each speed dial action.

 Provided

- The Fab has `aria-haspopup`, `aria-expanded` and `aria-controls` attributes.
- The speed dial actions container has `role="menu"` and `aria-orientation` set according to the direction.
- The speed dial actions have `role="menuitem"`, and an `aria-describedby` attribute that references the associated tooltip.

 Keyboard

- The speed dial opens on focus.
- The Space and Enter keys trigger the selected speed dial action, and toggle the speed dial open state.
- The cursor keys move focus to the next or previous speed dial action. (Note that any cursor direction can be used initially to open the speed dial. This enables the expected behavior for the actual or perceived orientation of the speed dial, for example for a screen reader user who perceives the speed dial as a drop-down menu.)
- The Escape key closes the speed dial and, if a speed dial action was focused, returns focus to the Fab.

## Stack

<p class="description">Stack is a container component for arranging elements vertically or horizontally.</p>

 Introduction

The Stack component manages the layout of its immediate children along the vertical or horizontal axis, with optional spacing and dividers between each child.

:::info
Stack is ideal for one-dimensional layouts, while Grid is preferable when you need both vertical _and_ horizontal arrangement.
:::

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basics

```jsx
import Stack from '@mui/material/Stack';
```

The Stack component acts as a generic container, wrapping around the elements to be arranged.

Use the `spacing` prop to control the space between children.
The spacing value can be any number, including decimals, or a string.
(The prop is converted into a CSS property using the [`theme.spacing()`](/material-ui/customization/spacing/) helper.)

{{"demo": "BasicStack.js", "bg": true}}

 Stack vs. Grid

`Stack` is concerned with one-dimensional layouts, while [Grid](/material-ui/react-grid/) handles two-dimensional layouts. The default direction is `column` which stacks children vertically.

 Direction

By default, Stack arranges items vertically in a column.
Use the `direction` prop to position items horizontally in a row:

{{"demo": "DirectionStack.js", "bg": true}}

 Dividers

Use the `divider` prop to insert an element between each child.
This works particularly well with the [Divider](/material-ui/react-divider/) component, as shown below:

{{"demo": "DividerStack.js", "bg": true}}

 Responsive values

You can switch the `direction` or `spacing` values based on the active breakpoint.

{{"demo": "ResponsiveStack.js", "bg": true}}

 Flexbox gap

To use [flexbox `gap`](https://developer.mozilla.org/en-US/docs/Web/CSS/gap) for the spacing implementation, set the `useFlexGap` prop to true.

It removes the [known limitations](##limitations) of the default implementation that uses CSS nested selector. However, CSS flexbox gap is not fully supported in some browsers.

We recommend checking the [support percentage](https://caniuse.com/?search=flex%20gap) before using it.

{{"demo": "FlexboxGapStack.js", "bg": true}}

To set the prop to all stack instances, create a theme with default props:

```js
import { ThemeProvider, createTheme } from '@mui/material/styles';
import Stack from '@mui/material/Stack';

const theme = createTheme({
  components: {
    MuiStack: {
      defaultProps: {
        useFlexGap: true,
      },
    },
  },
});

function App() {
  return (
    <ThemeProvider theme={theme}>
      <Stack>…</Stack> {/* uses flexbox gap by default */}
    </ThemeProvider>
  );
}
```

 Interactive demo

Below is an interactive demo that lets you explore the visual results of the different settings:

{{"demo": "InteractiveStack.js", "hideToolbar": true, "bg": true}}

 System props

:::info
System props are deprecated and will be removed in the next major release. Please use the `sx` prop instead.

```diff
- <Stack mt={2} />
+ <Stack sx={{ mt: 2 }} />
```

:::

 Limitations

 Margin on the children

Customizing the margin on the children is not supported by default.

For instance, the top-margin on the `Button` component below will be ignored.

```jsx
<Stack>
  <Button sx={{ marginTop: '30px' }}>...</Button>
</Stack>
```

:::success
To overcome this limitation, set [`useFlexGap`](##flexbox-gap) prop to true to switch to CSS flexbox gap implementation.

You can learn more about this limitation by visiting this [RFC](https://github.com/mui/material-ui/issues/33754).
:::

 white-space: nowrap

The initial setting on flex items is `min-width: auto`.
This causes a positioning conflict when children use `white-space: nowrap;`.
You can reproduce the issue with:

```jsx
<Stack direction="row">
  <Typography noWrap>
```

In order for the item to stay within the container you need to set `min-width: 0`.

```jsx
<Stack direction="row" sx={{ minWidth: 0 }}>
  <Typography noWrap>
```

{{"demo": "ZeroWidthStack.js", "bg": true}}

 Anatomy

The Stack component is composed of a single root `<div>` element:

```html
<div class="MuiStack-root">
  <!-- Stack contents -->
</div>
```

## Stepper

<p class="description">Steppers convey progress through numbered steps. It provides a wizard-like workflow.</p>

Steppers display progress through a sequence of logical and numbered steps. They may also be used for navigation.
Steppers may display a transient feedback message after a step is saved.

- **Types of Steps**: Editable, Non-editable, Mobile, Optional
- **Types of Steppers**: Horizontal, Vertical, Linear, Non-linear

{{"component": "@mui/docs/ComponentLinkHeader"}}

:::info
This component is no longer documented in the [Material Design guidelines](https://m2.material.io/), but Material UI will continue to support it.
:::

 Introduction

The Stepper component displays progress through a sequence of logical and numbered steps.
It supports horizontal and vertical orientation for desktop and mobile viewports.

Steppers are implemented using a collection of related components:

- Stepper: the container for the steps.
- Step: an individual step in the sequence.
- Step Label: a label for a Step.
- Step Content: optional content for a Step.
- Step Button: optional button for a Step.
- Step Icon: optional icon for a Step.
- Step Connector: optional customized connector between Steps.

 Basics

```jsx
import Stepper from '@mui/material/Stepper';
import Step from '@mui/material/Step';
import StepLabel from '@mui/material/StepLabel';
```

 Horizontal stepper

Horizontal steppers are ideal when the contents of one step depend on an earlier step.

Avoid using long step names in horizontal steppers.

 Linear

A linear stepper allows the user to complete the steps in sequence.

The `Stepper` can be controlled by passing the current step index (zero-based) as the `activeStep` prop. `Stepper` orientation is set using the `orientation` prop.

This example also shows the use of an optional step by placing the `optional` prop on the second `Step` component. Note that it's up to you to manage when an optional step is skipped. Once you've determined this for a particular step you must set `completed={false}` to signify that even though the active step index has gone beyond the optional step, it's not actually complete.

{{"demo": "HorizontalLinearStepper.js"}}

 Non-linear

Non-linear steppers allow the user to enter a multi-step flow at any point.

This example is similar to the regular horizontal stepper, except steps are no longer automatically set to `disabled={true}` based on the `activeStep` prop.

The use of the `StepButton` here demonstrates clickable step labels, as well as setting the `completed`
flag. However because steps can be accessed in a non-linear fashion, it's up to your own implementation to
determine when all steps are completed (or even if they need to be completed).

{{"demo": "HorizontalNonLinearStepper.js"}}

 Alternative label

Labels can be placed below the step icon by setting the `alternativeLabel` prop on the `Stepper` component.

{{"demo": "HorizontalLinearAlternativeLabelStepper.js"}}

 Error step

{{"demo": "HorizontalStepperWithError.js"}}

 Customized horizontal stepper

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSteppers.js"}}

 Vertical stepper

Vertical steppers are designed for narrow screen sizes. They are ideal for mobile. All the features of the horizontal stepper can be implemented.

{{"demo": "VerticalLinearStepper.js"}}

 Performance

The content of a step is unmounted when closed.
If you need to make the content available to search engines or render expensive component trees inside your modal while optimizing for interaction responsiveness it might be a good idea to keep the step mounted with:

```jsx
<StepContent TransitionProps={{ unmountOnExit: false }} />
```

 Mobile stepper

This component implements a compact stepper suitable for a mobile device. It has more limited functionality than the vertical stepper. See [mobile steps](https://m1.material.io/components/steppers.html##steppers-types-of-steps) for its inspiration.

The mobile stepper supports three variants to display progress through the available steps: text, dots, and progress.

 Text

The current step and total number of steps are displayed as text.

{{"demo": "TextMobileStepper.js", "bg": true}}

 Dots

Use dots when the number of steps is small.

{{"demo": "DotsMobileStepper.js", "bg": true}}

 Progress

Use a progress bar when there are many steps, or if there are steps that need to be inserted during the process (based on responses to earlier steps).

{{"demo": "ProgressMobileStepper.js", "bg": true}}

##switches
unstyled: /base-ui/react-switch/
githubSource: packages/mui-material/src/Switch
---

## Switch

<p class="description">Switches toggle the state of a single setting on or off.</p>

Switches are the preferred way to adjust settings on mobile.
The option that the switch controls, as well as the state it's in,
should be made clear from the corresponding inline label.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic switches

{{"demo": "BasicSwitches.js"}}

 Label

You can provide a label to the `Switch` thanks to the `FormControlLabel` component.

{{"demo": "SwitchLabels.js"}}

 Size

Use the `size` prop to change the size of the switch.

{{"demo": "SwitchesSize.js"}}

 Color

{{"demo": "ColorSwitches.js"}}

 Controlled

You can control the switch with the `checked` and `onChange` props:

{{"demo": "ControlledSwitches.js"}}

 Switches with FormGroup

`FormGroup` is a helpful wrapper used to group selection controls components that provides an easier API.
However, you are encouraged to use [Checkboxes](/material-ui/react-checkbox/) instead if multiple related controls are required. (See: [When to use](##when-to-use)).

{{"demo": "SwitchesGroup.js"}}

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSwitches.js"}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/switch-introduction--docs).

 Label placement

You can change the placement of the label:

{{"demo": "FormControlLabelPosition.js"}}

 When to use

- [Checkboxes vs. Switches](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

 Accessibility

- It will render an element with the `checkbox` role not `switch` role since this
  role isn't widely supported yet. Please test first if assistive technology of your
  target audience supports this role properly. Then you can change the role with
  `<Switch inputProps={{ role: 'switch' }}>`
- All form controls should have labels, and this includes radio buttons, checkboxes, and switches. In most cases, this is done by using the `<label>` element ([FormControlLabel](/material-ui/api/form-control-label/)).
- When a label can't be used, it's necessary to add an attribute directly to the input component.
  In this case, you can apply the additional attribute (for example `aria-label`, `aria-labelledby`, `title`) via the `inputProps` prop.

```jsx
<Switch value="checkedA" inputProps={{ 'aria-label': 'Switch A' }} />
```

## Table

<p class="description">Tables display sets of data. They can be fully customized.</p>

Tables display information in a way that's easy to scan, so that users can look for patterns and insights. They can be embedded in primary content, such as cards. They can include:

- A corresponding visualization
- Navigation
- Tools to query and manipulate data

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Tables are implemented using a collection of related components:

- `<TableContainer />`: A wrapper that provides horizontally scrolling behavior for the `<Table />` component.
- `<Table />`: The main component for the table element. Renders as a `<table>` by default.
- `<TableHead />`: The container for the header row(s) of `<Table />`. Renders as a `<thead>` by default.
- `<TableBody />`: The container for the body rows of `<Table />`. Renders as a `<tbody>` by default.
- `<TableRow />`: A row in a table. Can be used in `<TableHead />`, `<TableBody />`, or `<TableFooter />`. Renders as a `<tr>` by default.
- `<TableCell />`: A cell in a table. Can be used in `<TableRow />` . Renders as a `<th>` in `<TableHead />` and `<td>` in `<TableBody />` by default.
- `<TableFooter />`: An optional container for the footer row(s) of the table. Renders as a `<tfoot>` by default.
- `<TablePagination />`: A component that provides controls for paginating table data. See the ['Sorting & selecting' example](##sorting-amp-selecting) and ['Custom Table Pagination Action' example](##custom-pagination-actions).
- `<TableSortLabel />`: A component used to display sorting controls for column headers, allowing users to sort data in ascending or descending order. See the ['Sorting & selecting' example](##sorting-amp-selecting).

 Basic table

A simple example with no frills.

{{"demo": "BasicTable.js", "bg": true}}

 Data table

The `Table` component has a close mapping to the native `<table>` elements.
This constraint makes building rich data tables challenging.

The [`DataGrid` component](/x/react-data-grid/) is designed for use-cases that are focused on handling large amounts of tabular data.
While it comes with a more rigid structure, in exchange, you gain more powerful features.

{{"demo": "DataTable.js", "bg": true}}

 Dense table

A simple example of a dense table with no frills.

{{"demo": "DenseTable.js", "bg": true}}

 Sorting & selecting

This example demonstrates the use of `Checkbox` and clickable rows for selection, with a custom `Toolbar`. It uses the `TableSortLabel` component to help style column headings.

The Table has been given a fixed width to demonstrate horizontal scrolling. In order to prevent the pagination controls from scrolling, the TablePagination component is used outside of the Table. (The ['Custom Table Pagination Action' example](##custom-pagination-actions) below shows the pagination within the TableFooter.)

{{"demo": "EnhancedTable.js", "bg": true}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTables.js", "bg": true}}

 Custom pagination options

It's possible to customize the options shown in the "Rows per page" select using the `rowsPerPageOptions` prop.
You should either provide an array of:

- **numbers**, each number will be used for the option's label and value.

  ```jsx
  <TablePagination rowsPerPageOptions={[10, 50]} />
  ```

- **objects**, the `value` and `label` keys will be used respectively for the value and label of the option (useful for language strings such as 'All').

  ```jsx
  <TablePagination rowsPerPageOptions={[10, 50, { value: -1, label: 'All' }]} />
  ```

 Custom pagination actions

The `ActionsComponent` prop of the `TablePagination` component allows the implementation of custom actions.

{{"demo": "CustomPaginationActionsTable.js", "bg": true}}

 Sticky header

Here is an example of a table with scrollable rows and fixed column headers.
It leverages the `stickyHeader` prop.

{{"demo": "StickyHeadTable.js", "bg": true}}

 Column grouping

You can group column headers by rendering multiple table rows inside a table head:

```jsx
<TableHead>
  <TableRow />
  <TableRow />
</TableHead>
```

{{"demo": "ColumnGroupingTable.js", "bg": true}}

 Collapsible table

An example of a table with expandable rows, revealing more information.
It utilizes the [`Collapse`](/material-ui/api/collapse/) component.

{{"demo": "CollapsibleTable.js", "bg": true}}

 Spanning table

A simple example with spanning rows & columns.

{{"demo": "SpanningTable.js", "bg": true}}

 Virtualized table

In the following example, we demonstrate how to use [react-virtuoso](https://github.com/petyosi/react-virtuoso) with the `Table` component.
It renders 200 rows and can easily handle more.
Virtualization helps with performance issues.

{{"demo": "ReactVirtualizedTable.js", "bg": true}}

 Accessibility

(WAI tutorial: <https://www.w3.org/WAI/tutorials/tables/>)

 Caption

A caption functions like a heading for a table. Most screen readers announce the content of captions. Captions help users to find a table and understand what it's about and decide if they want to read it.

{{"demo": "AccessibleTable.js", "bg": true}}

 Unstyled

If you would like to use an unstyled Table, you can use the primitive HTML elements and enhance the table with the TablePaginationUnstyled component.
See the demos in the [unstyled table pagination docs](/base-ui/react-table-pagination/)

## Tabs

<p class="description">Tabs make it easy to explore and switch between different views.</p>

Tabs organize and allow navigation between groups of content that are related and at the same level of hierarchy.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Introduction

Tabs are implemented using a collection of related components:

- `<Tab />` - the tab element itself. Clicking on a tab displays its corresponding panel.
- `<Tabs />` - the container that houses the tabs. Responsible for handling focus and keyboard navigation between tabs.

{{"demo": "BasicTabs.js"}}

 Basics

```jsx
import Tabs from '@mui/material/Tabs';
import Tab from '@mui/material/Tab';
```

 Experimental API

`@mui/lab` offers utility components that inject props to implement accessible tabs
following [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/):

- `<TabList />` - the container that houses the tabs. Responsible for handling focus and keyboard navigation between tabs.
- `<TabPanel />` - the card that hosts the content associated with a tab.
- `<TabContext />` - the top-level component that wraps the Tab List and Tab Panel components.

{{"demo": "LabTabs.js"}}

 Wrapped labels

Long labels will automatically wrap on tabs.
If the label is too long for the tab, it will overflow, and the text will not be visible.

{{"demo": "TabsWrappedLabel.js"}}

 Colored tab

{{"demo": "ColorTabs.js"}}

 Disabled tab

A tab can be disabled by setting the `disabled` prop.

{{"demo": "DisabledTabs.js"}}

 Fixed tabs

Fixed tabs should be used with a limited number of tabs, and when a consistent placement will aid muscle memory.

 Full width

The `variant="fullWidth"` prop should be used for smaller views.

{{"demo": "FullWidthTabs.js", "bg": true}}

 Centered

The `centered` prop should be used for larger views.

{{"demo": "CenteredTabs.js", "bg": true}}

 Scrollable tabs

 Automatic scroll buttons

Use the `variant="scrollable"` and `scrollButtons="auto"` props to display left and right scroll buttons on desktop that are hidden on mobile:

{{"demo": "ScrollableTabsButtonAuto.js", "bg": true}}

 Forced scroll buttons

Apply `scrollButtons={true}` and the `allowScrollButtonsMobile` prop to display the left and right scroll buttons on all viewports:

{{"demo": "ScrollableTabsButtonForce.js", "bg": true}}

If you want to make sure the buttons are always visible, you should customize the opacity.

```css
.MuiTabs-scrollButtons.Mui-disabled {
  opacity: 0.3;
}
```

{{"demo": "ScrollableTabsButtonVisible.js", "bg": true}}

 Prevent scroll buttons

Left and right scroll buttons are never be presented with `scrollButtons={false}`.
All scrolling must be initiated through user agent scrolling mechanisms (for example left/right swipe, shift mouse wheel, etc.)

{{"demo": "ScrollableTabsButtonPrevent.js", "bg": true}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTabs.js"}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/tabs-introduction--docs).

 Vertical tabs

To make vertical tabs instead of default horizontal ones, there is `orientation="vertical"`:

{{"demo": "VerticalTabs.js", "bg": true}}

Note that you can restore the scrollbar with `visibleScrollbar`.

 Nav tabs

By default, tabs use a `button` element, but you can provide your custom tag or component. Here's an example of implementing tabbed navigation:

{{"demo": "NavTabs.js"}}

 Third-party routing library

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server.
The `Tab` component provides the `component` prop to handle this use case.
Here is a [more detailed guide](/material-ui/integrations/routing/##tabs).

 Icon tabs

Tab labels may be either all icons or all text.

{{"demo": "IconTabs.js"}}

{{"demo": "IconLabelTabs.js"}}

 Icon position

By default, the icon is positioned at the `top` of a tab. Other supported positions are `start`, `end`, `bottom`.

{{"demo": "IconPositionTabs.js"}}

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/tabs/)

The following steps are needed in order to provide necessary information for assistive technologies:

1. Label `Tabs` via `aria-label` or `aria-labelledby`.
2. `Tab`s need to be connected to their
   corresponding `[role="tabpanel"]` by setting the correct `id`, `aria-controls` and `aria-labelledby`.

An example for the current implementation can be found in the demos on this page. We've also published [an experimental API](##experimental-api) in `@mui/lab` that does not require
extra work.

 Keyboard navigation

The components implement keyboard navigation using the "manual activation" behavior.
If you want to switch to the "selection automatically follows focus" behavior you have to pass `selectionFollowsFocus` to the `Tabs` component.
The WAI-ARIA authoring practices have a detailed guide on [how to decide when to make selection automatically follow focus](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/##x6-4-deciding-when-to-make-selection-automatically-follow-focus).

 Demo

The following two demos only differ in their keyboard navigation behavior.
Focus a tab and navigate with arrow keys to notice the difference, for example <kbd class="key">Arrow Left</kbd>.

```jsx
/* Tabs where selection follows focus */
<Tabs selectionFollowsFocus />
```

{{"demo": "AccessibleTabs1.js", "defaultCodeOpen": false}}

```jsx
/* Tabs where each tab needs to be selected manually */
<Tabs />
```

{{"demo": "AccessibleTabs2.js", "defaultCodeOpen": false}}

## Text Field

<p class="description">Text Fields let users enter and edit text.</p>

Text fields allow users to enter text into a UI. They typically appear in forms and dialogs.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic TextField

The `TextField` wrapper component is a complete form control including a label, input, and help text.
It comes with three variants: outlined (default), filled, and standard.

{{"demo": "BasicTextFields.js"}}

:::info
The standard variant of the Text Field is no longer documented in the [Material Design guidelines](https://m2.material.io/)
([this article explains why](https://medium.com/google-design/the-evolution-of-material-designs-text-fields-603688b3fe03)),
but Material UI will continue to support it.
:::

 Form props

Standard form attributes are supported, for example `required`, `disabled`, `type`, etc. as well as a `helperText` which is used to give context about a field's input, such as how the input will be used.

{{"demo": "FormPropsTextFields.js"}}

 Validation

The `error` prop toggles the error state.
The `helperText` prop can then be used to provide feedback to the user about the error.

{{"demo": "ValidationTextFields.js"}}

 Multiline

The `multiline` prop transforms the Text Field into a [MUI Base Textarea Autosize](/base-ui/react-textarea-autosize/) element.
Unless the `rows` prop is set, the height of the text field dynamically matches its content.
You can use the `minRows` and `maxRows` props to bound it.

{{"demo": "MultilineTextFields.js"}}

 Select

The `select` prop makes the text field use the [Select](/material-ui/react-select/) component internally.

{{"demo": "SelectTextFields.js"}}

 Icons

There are multiple ways to display an icon with a text field.

{{"demo": "InputWithIcon.js"}}

 Input Adornments

The main way is with an `InputAdornment`.
This can be used to add a prefix, a suffix, or an action to an input.
For instance, you can use an icon button to hide or reveal the password.

{{"demo": "InputAdornments.js"}}

 Customizing adornments

You can apply custom styles to adornments, and trigger changes to one based on attributes from another.
For example, the demo below uses the label's `[data-shrink=true]` attribute to make the suffix visible (via opacity) when the label is in its shrunken state.

{{"demo": "InputSuffixShrink.js"}}

 Sizes

Fancy smaller inputs? Use the `size` prop.

{{"demo": "TextFieldSizes.js"}}

The `filled` variant input height can be further reduced by rendering the label outside of it.

{{"demo": "TextFieldHiddenLabel.js"}}

 Margin

The `margin` prop can be used to alter the vertical spacing of the text field.
Using `none` (default) doesn't apply margins to the `FormControl` whereas `dense` and `normal` do.

{{"demo": "LayoutTextFields.js"}}

 Full width

`fullWidth` can be used to make the input take up the full width of its container.

{{"demo": "FullWidthTextField.js"}}

 Uncontrolled vs. Controlled

The component can be controlled or uncontrolled.

:::info

- A component is **controlled** when it's managed by its parent using props.
- A component is **uncontrolled** when it's managed by its own local state.

Learn more about controlled and uncontrolled components in the [React documentation](https://react.dev/learn/sharing-state-between-components##controlled-and-uncontrolled-components).
:::

{{"demo": "StateTextFields.js"}}

 Components

`TextField` is composed of smaller components (
[`FormControl`](/material-ui/api/form-control/),
[`Input`](/material-ui/api/input/),
[`FilledInput`](/material-ui/api/filled-input/),
[`InputLabel`](/material-ui/api/input-label/),
[`OutlinedInput`](/material-ui/api/outlined-input/),
and [`FormHelperText`](/material-ui/api/form-helper-text/)
) that you can leverage directly to significantly customize your form inputs.

You might also have noticed that some native HTML input properties are missing from the `TextField` component.
This is on purpose.
The component takes care of the most used properties.
Then, it's up to the user to use the underlying component shown in the following demo. Still, you can use `slotProps.htmlInput` (and `slotProps.input`, `slotProps.inputLabel` properties) if you want to avoid some boilerplate.

{{"demo": "ComposedTextField.js"}}

 Inputs

{{"demo": "Inputs.js"}}

 Color

The `color` prop changes the highlight color of the text field when focused.

{{"demo": "ColorTextFields.js"}}

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

 Using the styled API

{{"demo": "CustomizedInputsStyled.js"}}

 Using the theme style overrides API

Use the `styleOverrides` key to change any style injected by Material UI into the DOM.
See the [theme style overrides](/material-ui/customization/theme-components/##theme-style-overrides) documentation for further details.

{{"demo": "CustomizedInputsStyleOverrides.js"}}

Customization does not stop at CSS.
You can use composition to build custom components and give your app a unique feel.
Below is an example using the [`InputBase`](/material-ui/api/input-base/) component, inspired by Google Maps.

{{"demo": "CustomizedInputBase.js", "bg": true}}

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/textField-introduction--docs).

 `useFormControl`

For advanced customization use cases, a `useFormControl()` hook is exposed.
This hook returns the context value of the parent `FormControl` component.

**API**

```jsx
import { useFormControl } from '@mui/material/FormControl';
```

**Returns**

`value` (_object_):

- `value.adornedStart` (_bool_): Indicate whether the child `Input` or `Select` component has a start adornment.
- `value.setAdornedStart` (_func_): Setter function for `adornedStart` state value.
- `value.color` (_string_): The theme color is being used, inherited from `FormControl` `color` prop .
- `value.disabled` (_bool_): Indicate whether the component is being displayed in a disabled state, inherited from `FormControl` `disabled` prop.
- `value.error` (_bool_): Indicate whether the component is being displayed in an error state, inherited from `FormControl` `error` prop
- `value.filled` (_bool_): Indicate whether input is filled
- `value.focused` (_bool_): Indicate whether the component and its children are being displayed in a focused state
- `value.fullWidth` (_bool_): Indicate whether the component is taking up the full width of its container, inherited from `FormControl` `fullWidth` prop
- `value.hiddenLabel` (_bool_): Indicate whether the label is being hidden, inherited from `FormControl` `hiddenLabel` prop
- `value.required` (_bool_): Indicate whether the label is indicating that the input is required input, inherited from the `FormControl` `required` prop
- `value.size` (_string_): The size of the component, inherited from the `FormControl` `size` prop
- `value.variant` (_string_): The variant is being used by the `FormControl` component and its children, inherited from `FormControl` `variant` prop
- `value.onBlur` (_func_): Should be called when the input is blurred
- `value.onFocus` (_func_): Should be called when the input is focused
- `value.onEmpty` (_func_): Should be called when the input is emptied
- `value.onFilled` (_func_): Should be called when the input is filled

**Example**

{{"demo": "UseFormControl.js"}}

 Performance

Global styles for the auto-fill keyframes are injected and removed on each mount and unmount, respectively.
If you are loading a large number of Text Field components at once, it might be a good idea to change this default behavior by enabling [`disableInjectingGlobalStyles`](/material-ui/api/input-base/##input-base-prop-disableInjectingGlobalStyles) in `MuiInputBase`.
Make sure to inject `GlobalStyles` for the auto-fill keyframes at the top of your application.

```jsx
import { GlobalStyles, createTheme, ThemeProvider } from '@mui/material';

const theme = createTheme({
  components: {
    MuiInputBase: {
      defaultProps: {
        disableInjectingGlobalStyles: true,
      },
    },
  },
});

export default function App() {
  return (
    <ThemeProvider theme={theme}>
      <GlobalStyles
        styles={{
          '@keyframes mui-auto-fill': { from: { display: 'block' } },
          '@keyframes mui-auto-fill-cancel': { from: { display: 'block' } },
        }}
      />
      ...
    </ThemeProvider>
  );
}
```

 Limitations

 Shrink

The input label "shrink" state isn't always correct.
The input label is supposed to shrink as soon as the input is displaying something.
In some circumstances, we can't determine the "shrink" state (number input, datetime input, Stripe input). You might notice an overlap.

![shrink](/static/images/text-fields/shrink.png)

To workaround the issue, you can force the "shrink" state of the label.

```jsx
<TextField slotProps={{ inputLabel: { shrink: true } }} />
```

or

```jsx
<InputLabel shrink>Count</InputLabel>
```

 Floating label

The floating label is absolutely positioned.
It won't impact the layout of the page.
Make sure that the input is larger than the label to display correctly.

 type="number"

:::warning
We do not recommend using `type="number"` with a Text Field due to potential usability issues:

- it allows certain non-numeric characters ('e', '+', '-', '.') and silently discards others
- the functionality of scrolling to increment/decrement the number can cause accidental and hard-to-notice changes
- and more—see [Why the GOV.UK Design System team changed the input type for numbers](https://technology.blog.gov.uk/2020/02/24/why-the-gov-uk-design-system-team-changed-the-input-type-for-numbers/) for a more detailed explanation of the limitations of `<input type="number">`

  :::

If you need a text field with number validation, you can use MUI Base's [Number Input](/base-ui/react-number-input/) instead.

You can follow [this GitHub issue](https://github.com/mui/material-ui/issues/19154) to track the progress of introducing the Number Input component to Material UI.

 Helper text

The helper text prop affects the height of the text field. If two text fields are placed side by side, one with a helper text and one without, they will have different heights. For example:

{{"demo": "HelperTextMisaligned.js"}}

This can be fixed by passing a space character to the `helperText` prop:

{{"demo": "HelperTextAligned.js"}}

 Integration with 3rd party input libraries

You can use third-party libraries to format an input.
You have to provide a custom implementation of the `<input>` element with the `inputComponent` property.

The following demo uses the [react-imask](https://github.com/uNmAnNeR/imaskjs) and [react-number-format](https://github.com/s-yadav/react-number-format) libraries. The same concept could be applied to, for example [react-stripe-element](https://github.com/mui/material-ui/issues/16037).

{{"demo": "FormattedInputs.js"}}

The provided input component should expose a ref with a value that implements the following interface:

```ts
interface InputElement {
  focus(): void;
  value?: string;
}
```

```jsx
const MyInputComponent = React.forwardRef((props, ref) => {
  const { component: Component, ...other } = props;

  // implement `InputElement` interface
  React.useImperativeHandle(ref, () => ({
    focus: () => {
      // logic to focus the rendered component from 3rd party belongs here
    },
    // hiding the value e.g. react-stripe-elements
  }));

  // `Component` will be your `SomeThirdPartyComponent` from below
  return <Component {...other} />;
});

// usage
<TextField
  slotProps={{
    input: {
      inputComponent: MyInputComponent,
      inputProps: {
        component: SomeThirdPartyComponent,
      },
    },
  }}
/>;
```

 Accessibility

In order for the text field to be accessible, **the input should be linked to the label and the helper text**. The underlying DOM nodes should have this structure:

```jsx
<div class="form-control">
  <label for="my-input">Email address</label>
  <input id="my-input" aria-describedby="my-helper-text" />
  <span id="my-helper-text">We'll never share your email.</span>
</div>
```

- If you are using the `TextField` component, you just have to provide a unique `id` unless you're using the `TextField` only client-side.
  Until the UI is hydrated `TextField` without an explicit `id` will not have associated labels.
- If you are composing the component:

```jsx
<FormControl>
  <InputLabel htmlFor="my-input">Email address</InputLabel>
  <Input id="my-input" aria-describedby="my-helper-text" />
  <FormHelperText id="my-helper-text">We'll never share your email.</FormHelperText>
</FormControl>
```

 Supplementary projects

<!-- To sync with related-projects.md -->

For more advanced use cases, you might be able to take advantage of:

- [react-hook-form-mui](https://github.com/dohomi/react-hook-form-mui): Material UI and [react-hook-form](https://react-hook-form.com/) combined.
- [formik-material-ui](https://github.com/stackworx/formik-mui): Bindings for using Material UI with [formik](https://formik.org/).
- [mui-rff](https://github.com/lookfirst/mui-rff): Bindings for using Material UI with [React Final Form](https://final-form.org/react).
- [@ui-schema/ds-material](https://www.npmjs.com/package/@ui-schema/ds-material) Bindings for using Material UI with [UI Schema](https://github.com/ui-schema/ui-schema). JSON Schema compatible.

## Textarea Autosize

<p class="description">The Textarea Autosize component gives you a textarea HTML element that automatically adjusts its height to match the length of the content within.</p>

 This document has moved

:::warning
Please refer to the [Textarea Autosize](/base-ui/react-textarea-autosize/) component page in the MUI Base docs for demos and details on usage.

Textarea Autosize is a part of the standalone MUI Base component library.
It is currently re-exported from `@mui/material` for your convenience, but it will be removed from this package in a future major version after MUI Base gets a stable release.
:::

## Timeline

<p class="description">The timeline displays a list of events in chronological order.</p>

:::info
This component is not documented in the [Material Design guidelines](https://m2.material.io/), but it is available in Material UI.
:::

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic timeline

A basic timeline showing list of events.

{{"demo": "BasicTimeline.js"}}

 Left-positioned timeline

The main content of the timeline can be positioned on the left side relative to the time axis.

{{"demo": "LeftPositionedTimeline.js"}}

 Alternating timeline

The timeline can display the events on alternating sides.

{{"demo": "AlternateTimeline.js"}}

 Reverse Alternating timeline

The timeline can display the events on alternating sides in reverse order.

{{"demo": "AlternateReverseTimeline.js"}}

 Color

The `TimelineDot` can appear in different colors from theme palette.

{{"demo": "ColorsTimeline.js"}}

 Outlined

{{"demo": "OutlinedTimeline.js"}}

 Opposite content

The timeline can display content on opposite sides.

{{"demo": "OppositeContentTimeline.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTimeline.js"}}

 Alignment

There are different ways in which a Timeline can be placed within the container.

You can do it by overriding the styles.

A Timeline centers itself in the container by default.

The demos below show how to adjust the relative width of the left and right sides of a Timeline:

 Left-aligned

{{"demo": "LeftAlignedTimeline.js"}}

 Right-aligned

{{"demo": "RightAlignedTimeline.js"}}

 Left-aligned with no opposite content

{{"demo": "NoOppositeContent.js"}}

##toggle-button
githubSource: packages/mui-material/src/ToggleButton
---

## Toggle Button

<p class="description">A Toggle Button can be used to group related options.</p>

To emphasize groups of related Toggle buttons,
a group should share a common container.
The `ToggleButtonGroup` controls the selected state of its child buttons when given its own `value` prop.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Exclusive selection

With exclusive selection, selecting one option deselects any other.

In this example, text justification toggle buttons present options for left, center, right, and fully justified text (disabled), with only one item available for selection at a time.

**Note**: Exclusive selection does not enforce that a button must be active. For that effect see [enforce value set](##enforce-value-set).

{{"demo": "ToggleButtons.js"}}

 Multiple selection

Multiple selection allows for logically-grouped options, like bold, italic, and underline, to have multiple options selected.

{{"demo": "ToggleButtonsMultiple.js"}}

 Size

For larger or smaller buttons, use the `size` prop.

{{"demo": "ToggleButtonSizes.js"}}

 Color

{{"demo": "ColorToggleButton.js"}}

 Vertical buttons

The buttons can be stacked vertically with the `orientation` prop set to "vertical".

{{"demo": "VerticalToggleButtons.js"}}

 Enforce value set

If you want to enforce that at least one button must be active, you can adapt your handleChange function.

```jsx
const handleAlignment = (event, newAlignment) => {
  if (newAlignment !== null) {
    setAlignment(newAlignment);
  }
};

const handleDevices = (event, newDevices) => {
  if (newDevices.length) {
    setDevices(newDevices);
  }
};
```

{{"demo": "ToggleButtonNotEmpty.js"}}

 Standalone toggle button

{{"demo": "StandaloneToggleButton.js"}}

 Customization

Here is an example of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedDividers.js", "bg": true}}

 Accessibility

 ARIA

- ToggleButtonGroup has `role="group"`. You should provide an accessible label with `aria-label="label"`, `aria-labelledby="id"` or `<label>`.
- ToggleButton sets `aria-pressed="<bool>"` according to the button state. You should label each button with `aria-label`.

 Keyboard

At present, toggle buttons are in DOM order. Navigate between them with the tab key. The button behavior follows standard keyboard semantics.

## Tooltip

<p class="description">Tooltips display informative text when users hover over, focus on, or tap an element.</p>

When activated, Tooltips display a text label identifying an element, such as a description of its function.

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic tooltip

{{"demo": "BasicTooltip.js"}}

 Positioned tooltips

The `Tooltip` has 12 **placement** choices.
They don't have directional arrows; instead, they rely on motion emanating from the source to convey direction.

{{"demo": "PositionedTooltips.js"}}

 Customization

Here are some examples of customizing the component.
You can learn more about this in the [overrides documentation page](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTooltips.js"}}

 Arrow tooltips

You can use the `arrow` prop to give your tooltip an arrow indicating which element it refers to.

{{"demo": "ArrowTooltips.js"}}

 Distance from anchor

To adjust the distance between the tooltip and its anchor, you can use the `slotProps` prop to modify the [offset](https://popper.js.org/docs/v2/modifiers/offset/) of the popper.

{{"demo": "TooltipOffset.js"}}

Alternatively, you can use the `slotProps` prop to customize the margin of the popper.

{{"demo": "TooltipMargin.js"}}

 Custom child element

The tooltip needs to apply DOM event listeners to its child element.
If the child is a custom React element, you need to make sure that it spreads its props to the underlying DOM element.

```jsx
const MyComponent = React.forwardRef(function MyComponent(props, ref) {
  //  Spread the props to the underlying DOM element.
  return (
    <div {...props} ref={ref}>
      Bin
    </div>
  );
});

// ...

<Tooltip title="Delete">
  <MyComponent />
</Tooltip>;
```

If using a class component as a child, you'll also need to ensure that the ref is forwarded to the underlying DOM element. (A ref to the class component itself will not work.)

```jsx
class MyComponent extends React.Component {
  render() {
    const { innerRef, ...props } = this.props;
    //  Spread the props to the underlying DOM element.
    return (
      <div {...props} ref={innerRef}>
        Bin
      </div>
    );
  }
}

// Wrap MyComponent to forward the ref as expected by Tooltip
const WrappedMyComponent = React.forwardRef(function WrappedMyComponent(props, ref) {
  return <MyComponent {...props} innerRef={ref} />;
});

// ...

<Tooltip title="Delete">
  <WrappedMyComponent />
</Tooltip>;
```

 Triggers

You can define the types of events that cause a tooltip to show.

The touch action requires a long press due to the `enterTouchDelay` prop being set to `700`ms by default.

{{"demo": "TriggersTooltips.js"}}

 Controlled tooltips

You can use the `open`, `onOpen` and `onClose` props to control the behavior of the tooltip.

{{"demo": "ControlledTooltips.js"}}

 Variable width

The `Tooltip` wraps long text by default to make it readable.

{{"demo": "VariableWidth.js"}}

 Interactive

Tooltips are interactive by default (to pass [WCAG 2.1 success criterion 1.4.13](https://www.w3.org/TR/WCAG21/##content-on-hover-or-focus)).
It won't close when the user hovers over the tooltip before the `leaveDelay` is expired.
You can disable this behavior (thus failing the success criterion which is required to reach level AA) by passing `disableInteractive`.

{{"demo": "NonInteractiveTooltips.js"}}

 Disabled elements

By default disabled elements like `<button>` do not trigger user interactions so a `Tooltip` will not activate on normal events like hover. To accommodate disabled elements, add a simple wrapper element, such as a `span`.

:::warning
In order to work with Safari, you need at least one display block or flex item below the tooltip wrapper.
:::

{{"demo": "DisabledTooltips.js"}}

:::warning
If you're not wrapping a Material UI component that inherits from `ButtonBase`, for instance, a native `<button>` element, you should also add the CSS property _pointer-events: none;_ to your element when disabled:
:::

```jsx
<Tooltip title="You don't have permission to do this">
  <span>
    <button disabled={disabled} style={disabled ? { pointerEvents: 'none' } : {}}>
      A disabled button
    </button>
  </span>
</Tooltip>
```

 Transitions

Use a different transition.

{{"demo": "TransitionsTooltips.js"}}

 Follow cursor

You can enable the tooltip to follow the cursor by setting `followCursor={true}`.

{{"demo": "FollowCursorTooltips.js"}}

 Virtual element

In the event you need to implement a custom placement, you can use the `anchorEl` prop:
The value of the `anchorEl` prop can be a reference to a fake DOM element.
You need to create an object shaped like the [`VirtualElement`](https://popper.js.org/docs/v2/virtual-elements/).

{{"demo": "AnchorElTooltips.js"}}

 Showing and hiding

The tooltip is normally shown immediately when the user's mouse hovers over the element, and hides immediately when the user's mouse leaves. A delay in showing or hiding the tooltip can be added through the `enterDelay` and `leaveDelay` props.

On mobile, the tooltip is displayed when the user longpresses the element and hides after a delay of 1500ms. You can disable this feature with the `disableTouchListener` prop.

{{"demo": "DelayTooltips.js"}}

 Accessibility

(WAI-ARIA: https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/)

By default, the tooltip only labels its child element.
This is notably different from `title` which can either label **or** describe its child depending on whether the child already has a label.
For example, in:

```html
<button title="some more information">A button</button>
```

the `title` acts as an accessible description.
If you want the tooltip to act as an accessible description you can pass `describeChild`.
Note that you shouldn't use `describeChild` if the tooltip provides the only visual label. Otherwise, the child would have no accessible name and the tooltip would violate [success criterion 2.5.3 in WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html).

{{"demo": "AccessibilityTooltips.js"}}

## Transfer List

<p class="description">A Transfer List (or "shuttle") enables the user to move one or more list items between lists.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Basic transfer list

For completeness, this example includes buttons for "move all", but not every transfer list needs these.

{{"demo": "TransferList.js", "bg": true}}

 Enhanced transfer list

This example exchanges the "move all" buttons for a "select all / select none" checkbox and adds a counter.

{{"demo": "SelectAllTransferList.js", "bg": true}}

 Limitations

The component comes with a couple of limitations:

- It only works on desktop.
  If you have a limited amount of options to select, prefer the [Autocomplete](/material-ui/react-autocomplete/##multiple-values) component.
  If mobile support is important for you, have a look at [##27579](https://github.com/mui/material-ui/issues/27579).
- There are no high-level components exported from npm. The demos are based on composition.
  If this is important for you, have a look at [##27579](https://github.com/mui/material-ui/issues/27579).

## Transitions

<p class="description">Transitions help to make a UI expressive and easy to use.</p>

Material UI provides transitions that can be used to introduce some basic [motion](https://m2.material.io/design/motion/) to your applications.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Collapse

Expand from the start edge of the child element.
Use the `orientation` prop if you need a horizontal collapse.
The `collapsedSize` prop can be used to set the minimum width/height when not expanded.

{{"demo": "SimpleCollapse.js", "bg": true}}

 Fade

Fade in from transparent to opaque.

{{"demo": "SimpleFade.js", "bg": true}}

 Grow

Expands outwards from the center of the child element, while also fading in from transparent to opaque.

The second example demonstrates how to change the `transform-origin`, and conditionally applies
the `timeout` prop to change the entry speed.

{{"demo": "SimpleGrow.js", "bg": true}}

 Slide

Slide in from the edge of the screen.
The `direction` prop controls which edge of the screen the transition starts from.

The Transition component's `mountOnEnter` prop prevents the child component from being mounted
until `in` is `true`.
This prevents the relatively positioned component from scrolling into view
from its off-screen position.
Similarly, the `unmountOnExit` prop removes the component from the DOM after it has been transition off-screen.

{{"demo": "SimpleSlide.js", "bg": true}}

 Slide relative to a container

The Slide component also accepts `container` prop, which is a reference to a DOM node.
If this prop is set, the Slide component will slide from the edge of that DOM node.

{{"demo": "SlideFromContainer.js", "bg": true}}

 Zoom

Expand outwards from the center of the child element.

This example also demonstrates how to delay the enter transition.

{{"demo": "SimpleZoom.js", "bg": true}}

 Child requirement

- **Forward the style**: To better support server rendering, Material UI provides a `style` prop to the children of some transition components (Fade, Grow, Zoom, Slide).
  The `style` prop must be applied to the DOM for the animation to work as expected.
- **Forward the ref**: The transition components require the first child element to forward its ref to the DOM node. For more details about ref, check out [Caveat with refs](/material-ui/guides/composition/##caveat-with-refs)
- **Single element**: The transition components require only one child element (`React.Fragment` is not allowed).

```jsx
// The `props` object contains a `style` prop.
// You need to provide it to the `div` element as shown here.
const MyComponent = React.forwardRef(function (props, ref) {
  return (
    <div ref={ref} {...props}>
      Fade
    </div>
  );
});

export default function Main() {
  return (
    <Fade>
      {/* MyComponent must be the only child */}
      <MyComponent />
    </Fade>
  );
}
```

 TransitionGroup

To animate a component when it is mounted or unmounted, you can use the [`TransitionGroup`](https://reactcommunity.org/react-transition-group/transition-group/) component from _react-transition-group_.
As components are added or removed, the `in` prop is toggled automatically by `TransitionGroup`.

{{"demo": "TransitionGroupExample.js"}}

 TransitionComponent prop

Some Material UI components use these transitions internally. These accept a `TransitionComponent` prop to customize the default transition.
You can use any of the above components or your own.
It should respect the following conditions:

- Accepts an `in` prop. This corresponds to the open/close state.
- Call the `onEnter` callback prop when the enter transition starts.
- Call the `onExited` callback prop when the exit transition is completed.
  These two callbacks allow to unmount the children when in a closed state and fully transitioned.

For more information on creating a custom transition, visit the _react-transition-group_ [`Transition` documentation](https://reactcommunity.org/react-transition-group/transition/).
You can also visit the dedicated sections of some of the components:

- [Modal](/material-ui/react-modal/##transitions)
- [Dialog](/material-ui/react-dialog/##transitions)
- [Popper](/material-ui/react-popper/##transitions)
- [Snackbar](/material-ui/react-snackbar/##transitions)
- [Tooltip](/material-ui/react-tooltip/##transitions)

 Performance & SEO

The content of transition component is mounted by default even if `in={false}`.
This default behavior has server-side rendering and SEO in mind.
If you render expensive component trees inside your transition it might be a good idea to change this default behavior by enabling the
`unmountOnExit` prop:

```jsx
<Fade in={false} unmountOnExit />
```

As with any performance optimization this is not a silver bullet.
Be sure to identify bottlenecks first and then try out these optimization strategies.

## Typography

<p class="description">Use typography to present your design and content as clearly and efficiently as possible.</p>

{{"component": "@mui/docs/ComponentLinkHeader"}}

 Roboto font

Material UI uses the [Roboto](https://fonts.google.com/specimen/Roboto) font by default.
Add it to your project via Fontsource, or with the Google Fonts CDN.

<codeblock storageKey="package-manager">

```bash npm
npm install @fontsource/roboto
```

```bash pnpm
pnpm add @fontsource/roboto
```

```bash yarn
yarn add @fontsource/roboto
```

</codeblock>

Then you can import it in your entry point like this:

```tsx
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
```

:::info
Fontsource can be configured to load specific subsets, weights, and styles. Material UI's default typography configuration relies only on the 300, 400, 500, and 700 font weights.
:::

 Google Web Fonts

To install Roboto through the Google Web Fonts CDN, add the following code inside your project's `<head />` tag:

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap"
/>
```

 Component

 Usage

The Typography component follows the [Material Design typographic scale](https://m2.material.io/design/typography/##type-scale) that provides a limited set of type sizes that work well together for a consistent layout.

{{"demo": "Types.js"}}

 Theme keys

In some situations you might not be able to use the Typography component.
Hopefully, you might be able to take advantage of the [`typography`](/material-ui/customization/default-theme/?expand-path=$.typography) keys of the theme.

{{"demo": "TypographyTheme.js"}}

 Customization

 Adding & disabling variants

In addition to using the default typography variants, you can add custom ones, or disable any you don't need. See the [Adding & disabling variants](/material-ui/customization/typography/##adding-amp-disabling-variants) page for more info.

 Changing the semantic element

The Typography component uses the `variantMapping` prop to associate a UI variant with a semantic element.
It's important to realize that the style of a typography component is independent from the semantic underlying element.

To change the underlying element for a one-off situation, like avoiding two `h1` elements in your page, use the `component` prop:

```jsx
<Typography variant="h1" component="h2">
  h1. Heading
</Typography>
```

To change the typography element mapping globally, [use the theme](/material-ui/customization/typography/##adding-amp-disabling-variants):

```js
const theme = createTheme({
  components: {
    MuiTypography: {
      defaultProps: {
        variantMapping: {
          h1: 'h2',
          h2: 'h2',
          h3: 'h2',
          h4: 'h2',
          h5: 'h2',
          h6: 'h2',
          subtitle1: 'h2',
          subtitle2: 'h2',
          body1: 'span',
          body2: 'span',
        },
      },
    },
  },
});
```

 System props

:::info
System props are deprecated and will be removed in the next major release. Please use the `sx` prop instead.

```diff
- <Typography mt={2} />
+ <Typography sx={{ mt: 2 }} />
```

:::

 Accessibility

Key factors to follow for an accessible typography:

- **Color**. Provide enough contrast between text and its background, check out the minimum recommended [WCAG 2.0 color contrast ratio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) (4.5:1).
- **Font size**. Use [relative units (rem)](/material-ui/customization/typography/##font-size), instead of pixels, to accommodate the user's browser settings.
- **Heading hierarchy**. Based on [the W3 guidelines](https://www.w3.org/WAI/tutorials/page-structure/headings/), don't skip heading levels. Make sure to [separate the semantics from the style](##changing-the-semantic-element).

## useMediaQuery

<p class="description">This React hook listens for matches to a CSS media query. It allows the rendering of components based on whether the query matches or not.</p>

Some of the key features:

- ⚛️ It has an idiomatic React API.
- 🚀 It's performant, it observes the document to detect when its media queries change, instead of polling the values periodically.
- 📦 [1.1 kB gzipped](https://bundlephobia.com/package/@mui/material).
- 🤖 It supports server-side rendering.

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

 Basic media query

You should provide a media query to the first argument of the hook.
The media query string can be any valid CSS media query, for example [`'(prefers-color-scheme: dark)'`](/material-ui/customization/dark-mode/##system-preference).

{{"demo": "SimpleMediaQuery.js", "defaultCodeOpen": true}}

⚠️ You can't use `'print'` per browsers limitation, for example [Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=774398).

 Using breakpoint helpers

You can use Material UI's [breakpoint helpers](/material-ui/customization/breakpoints/) as follows:

```jsx
import { useTheme } from '@mui/material/styles';
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const theme = useTheme();
  const matches = useMediaQuery(theme.breakpoints.up('sm'));

  return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>;
}
```

{{"demo": "ThemeHelper.js", "defaultCodeOpen": false}}

Alternatively, you can use a callback function, accepting the theme as a first argument:

```jsx
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const matches = useMediaQuery((theme) => theme.breakpoints.up('sm'));

  return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>;
}
```

⚠️ There is **no default** theme support, you have to inject it in a parent theme provider.

 Using JavaScript syntax

You can use [json2mq](https://github.com/akiran/json2mq) to generate media query string from a JavaScript object.

{{"demo": "JavaScriptMedia.js", "defaultCodeOpen": true}}

 Testing

You need an implementation of [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) in your test environment.

For instance, [jsdom doesn't support it yet](https://jestjs.io/docs/manual-mocks##mocking-methods-which-are-not-implemented-in-jsdom). You should polyfill it.
Using [css-mediaquery](https://github.com/ericf/css-mediaquery) to emulate it is recommended.

```js
import mediaQuery from 'css-mediaquery';

function createMatchMedia(width) {
  return (query) => ({
    matches: mediaQuery.match(query, {
      width,
    }),
    addEventListener: () => {},
    removeEventListener: () => {},
  });
}

describe('MyTests', () => {
  beforeAll(() => {
    window.matchMedia = createMatchMedia(window.innerWidth);
  });
});
```

 Client-side only rendering

To perform the server-side hydration, the hook needs to render twice.
A first time with `defaultMatches`, the value of the server, and a second time with the resolved value.
This double pass rendering cycle comes with a drawback: it's slower.
You can set the `noSsr` option to `true` if you use the returned value **only** client-side.

```js
const matches = useMediaQuery('(min-width:600px)', { noSsr: true });
```

or it can turn it on globally with the theme:

```js
const theme = createTheme({
  components: {
    MuiUseMediaQuery: {
      defaultProps: {
        noSsr: true,
      },
    },
  },
});
```

:::info
Note that `noSsr` has no effects when using the `createRoot()` API (the client-side only API introduced in React 18).
:::

 Server-side rendering

:::warning
Server-side rendering and client-side media queries are fundamentally at odds.
Be aware of the tradeoff. The support can only be partial.
:::

Try relying on client-side CSS media queries first.
For instance, you could use:

- [`<Box display>`](/system/display/##hiding-elements)
- [`themes.breakpoints.up(x)`](/material-ui/customization/breakpoints/##css-media-queries)
- or [`sx prop`](/system/getting-started/the-sx-prop/)

If none of the above alternatives are an option, you can proceed reading this section of the documentation.

First, you need to guess the characteristics of the client request, from the server.
You have the choice between using:

- **User agent**. Parse the user agent string of the client to extract information. Using [ua-parser-js](https://github.com/faisalman/ua-parser-js) to parse the user agent is recommended.
- **Client hints**. Read the hints the client is sending to the server. Be aware that this feature is [not supported everywhere](https://caniuse.com/##search=client%20hint).

Finally, you need to provide an implementation of [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) to the `useMediaQuery` with the previously guessed characteristics.
Using [css-mediaquery](https://github.com/ericf/css-mediaquery) to emulate matchMedia is recommended.

For instance on the server-side:

```js
import * as ReactDOMServer from 'react-dom/server';
import parser from 'ua-parser-js';
import mediaQuery from 'css-mediaquery';
import { createTheme, ThemeProvider } from '@mui/material/styles';

function handleRender(req, res) {
  const deviceType = parser(req.headers['user-agent']).device.type || 'desktop';
  const ssrMatchMedia = (query) => ({
    matches: mediaQuery.match(query, {
      // The estimated CSS width of the browser.
      width: deviceType === 'mobile' ? '0px' : '1024px',
    }),
  });

  const theme = createTheme({
    components: {
      // Change the default options of useMediaQuery
      MuiUseMediaQuery: {
        defaultProps: {
          ssrMatchMedia,
        },
      },
    },
  });

  const html = ReactDOMServer.renderToString(
    <ThemeProvider theme={theme}>
      <App />
    </ThemeProvider>,
  );

  // …
}
```

{{"demo": "ServerSide.js", "defaultCodeOpen": false}}

Make sure you provide the same custom match media implementation to the client-side to guarantee a hydration match.

 Migrating from `withWidth()`

The `withWidth()` higher-order component injects the screen width of the page.
You can reproduce the same behavior with a `useWidth` hook:

{{"demo": "UseWidth.js"}}

 API

 `useMediaQuery(query, [options]) => matches`

 Arguments

1. `query` (_string_ | _func_): A string representing the media query to handle or a callback function accepting the theme (in the context) that returns a string.
2. `options` (_object_ [optional]):

- `options.defaultMatches` (_bool_ [optional]):
  As `window.matchMedia()` is unavailable on the server,
  it returns a default matches during the first mount. The default value is `false`.
- `options.matchMedia` (_func_ [optional]): You can provide your own implementation of _matchMedia_. This can be used for handling an iframe content window.
- `options.noSsr` (_bool_ [optional]): Defaults to `false`.
  To perform the server-side hydration, the hook needs to render twice.
  A first time with `defaultMatches`, the value of the server, and a second time with the resolved value.
  This double pass rendering cycle comes with a drawback: it's slower.
  You can set this option to `true` if you use the returned value **only** client-side.
- `options.ssrMatchMedia` (_func_ [optional]): You can provide your own implementation of _matchMedia_, it's used when rendering server-side.

Note: You can change the default options using the [`default props`](/material-ui/customization/theme-components/##theme-default-props) feature of the theme with the `MuiUseMediaQuery` key.

 Returns

`matches`: Matches is `true` if the document currently matches the media query and `false` when it does not.

 Examples

```jsx
import * as React from 'react';
import useMediaQuery from '@mui/material/useMediaQuery';

export default function SimpleMediaQuery() {
  const matches = useMediaQuery('(min-width:600px)');

  return <span>{`(min-width:600px) matches: ${matches}`}</span>;
}
```
