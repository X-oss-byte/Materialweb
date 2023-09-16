<!-- catalog-only-start --><!-- ---
name: Select
dirname: select
-----><!-- catalog-only-end -->

<catalog-component-header image-align="start">
<catalog-component-header-title slot="title">

# Select

<!-- no-catalog-start -->

<!--*
# Document freshness: For more information, see go/fresh-source.
freshness: { owner: 'ajakubowicz' reviewed: '2023-09-14' }
tag: 'docType:reference'
*-->

<!-- go/md-select -->

<!-- [TOC] -->

<!-- external-only-start -->
**This documentation is fully rendered on the
[Material Web catalog](https://material-web.dev/components/<component>/)**
<!-- external-only-end -->

<!-- no-catalog-end -->

[Select menus](https://m3.material.io/components/menus/overview#b1704de4-94b7-4177-9e96-b677ae767cb4)<!-- {.external} -->
display a list of choices on temporary surfaces and display the currently
selected menu item above the menu.

</catalog-component-header-title>

<img class="hero" src="images/select/hero.png" alt="A textfield containing the text Item 2, with a dropdown menu containing Item 1, Item 2, and Item 3.">

</catalog-component-header>

*   Design article (*coming soon*)
*   API Documentation (*coming soon*)
*   [Source code](https://github.com/material-components/material-web/tree/main/select)
    <!-- {.external} -->

## Usage

Select (formally referred to as a dropdown menu) allows choosing a value from a
fixed list of available options. It is analogous to the native HTML
[`<select>` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)<!-- {.external} -->.

<!-- no-catalog-start -->
<!-- TODO: Image of the figure below. -->
<!-- no-catalog-end -->
<!-- catalog-include "figures/select/usage.html" -->

```html
<md-outlined-select>
  <md-select-option headline=""></md-select-option>
  <md-select-option selected value="apple" headline="Apple"></md-select-option>
  <md-select-option value="apricot" headline="Apricot"></md-select-option>
</md-outlined-select>

<md-filled-select>
  <md-select-option headline=""></md-select-option>
  <md-select-option value="apple" headline="Apple"></md-select-option>
  <md-select-option value="apricot" headline="Apricot"></md-select-option>
</md-filled-select>
```

### Required select

Indicate that a selection is mandatory by adding the `required` attribute.

```html
<md-filled-select required>
  <md-select-option value="one" headline="One"></md-select-option>
  <md-select-option value="two" headline="Two"></md-select-option>
</md-filled-select>
```

### Other supported properties

<!-- mdformat off(breaks rendering of table in the catalog) -->

| Attribute         | Property         | Description                           |
| ----------------- | ---------------- | ------------------------------------- |
| `quick`           | `quick`          | Opens menu dropdown immediately without animation. |
| `error-text`      | `errorText`      | Error message that replaces supporting text when `error` is true. Will override error message displayed by `reportValidity()`. |
| `label`           | `label`          | The floating label for the field.     |
| `supporting-text` | `supportingText` | Conveys additional information below the select, such as how it should be used. |
| `error`           | `error`          | Whether select is in a visually invalid state. |
| `menu-fixed`      | `menuFixed`      | Whether the underlying dropdown menu should be `position\: fixed` to display in a top-level manner. May be required when `md-select` is within a `md-dialog`. |
| `typeahead-delay` | `typeaheadDelay` | The max time between keystrokes of the typeahead select before clearing the buffer. |

<!-- mdformat on -->

<!--
## Accessibility

*Insert a 1-2 sentence description of a common accessibility scenario, followed
by a code snippet. Do not include a rendered image for accessibility examples.*

```html
<component-name aria-label="Example">
```

*Repeat with additional examples as needed to explain how to make the component
accessible.* -->

## Theming

Select supports
[Material theming](https://github.com/material-components/material-web/blob/main/docs/theming/README.md)<!-- {.external} -->
and can be customized in terms of color, typography, and shape.

### Filled Select tokens

Token                                           | Default value
----------------------------------------------- | -------------
`--md-filled-select-text-field-container-color` | `--md-sys-color-surface-container-highest`
`--md-filled-select-text-field-container-shape` | `4px`
`--md-filled-field-content-color`               | `--md-sys-color-on-surface`
`--md-filled-field-content-font`                | `--md-sys-typescale-body-large-font`

*   [Filled Select tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-filled-select.scss)
    <!-- {.external} -->

To theme the select's dropdown menu, use the `md-menu` component tokens on the
`::part(menu)` selector.

### Filled Select example

<!-- no-catalog-start -->
<!-- ![Image of a <component> with a different theme applied](images/<component>/theming.png "<Component> theming example.") -->
<!-- no-catalog-end -->
<!-- catalog-include "figures/select/theming-filled.html" -->

```html
<style>
:root {
  --md-filled-select-text-field-container-shape: 0px;
  --md-filled-select-text-field-container-color: #f7faf9;
  --md-filled-field-content-color: #005353;
  --md-filled-field-content-font: system-ui;
}

md-filled-select::part(menu) {
  --md-menu-container-color: #f4fbfa;
  --md-menu-container-shape: 0px;
  --md-menu-item-container-color: transparent;
}
</style>

<md-filled-select>
  <md-select-option selected value="apple" headline="Apple"></md-select-option>
  <md-select-option value="tomato" headline="Tomato"></md-select-option>
</md-filled-select>
```

### Outlined Select tokens

Token                                              | Default value
-------------------------------------------------- | -------------
`--md-outlined-select-text-field-outline-color`    | `--md-sys-color-outline`
`--md-outlined-select-text-field-container-shape`  | `4px`
`--md-outlined-select-text-field-input-text-color` | `--md-sys-color-on-surface`
`--md-outlined-select-text-field-input-text-font`  | `--md-sys-typescale-body-large-font`

*   [Outlined Select tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-outlined-select.scss)
    <!-- {.external} -->

### Outlined Select example

<!-- no-catalog-start -->
<!-- ![Image of a <component> with a different theme applied](images/<component>/theming.png "<Component> theming example.") -->
<!-- no-catalog-end -->
<!-- catalog-include "figures/select/theming-outlined.html" -->

```html
<style>
:root {
  --md-outlined-select-text-field-outline-color: #6e7979;
  --md-outlined-select-text-field-container-shape: 0px;
  --md-outlined-select-text-field-input-text-color: #005353;
  --md-outlined-select-text-field-input-text-font: system-ui;
}

md-outlined-select::part(menu) {
  --md-menu-container-color: #f4fbfa;
  --md-menu-container-shape: 0px;
  --md-menu-item-container-color: transparent;
}
</style>

<md-outlined-select>
  <md-select-option selected value="apple" headline="Apple"></md-select-option>
  <md-select-option value="tomato" headline="Tomato"></md-select-option>
</md-outlined-select>
```
