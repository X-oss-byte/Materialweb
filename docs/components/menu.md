<!-- catalog-only-start --><!-- ---
name: Menus
dirname: menu
-----><!-- catalog-only-end -->

<catalog-component-header>
<catalog-component-header-title slot="title">

# Menus

<!-- no-catalog-start -->

<!--*
# Document freshness: For more information, see go/fresh-source.
freshness: { owner: 'emarquez' reviewed: '2023-08-28' }
tag: 'docType:reference'
*-->

<!-- go/md-menu -->

<!-- [TOC] -->

<!-- external-only-start -->
**This documentation is fully rendered on the
[Material Web catalog](https://material-web.dev/components/menu/).**
<!-- external-only-end -->

<!-- no-catalog-end -->

[Menus](https://m3.material.io/components/menus)<!-- {.external} --> display a list of
choices on a temporary surface.

</catalog-component-header-title>

<img
    class="hero"
    alt="A phone showing a vertical threedot, pressed, icon button and a menu floating below it with the following visible items: Revert, Settings, and Send Feedback"
    src="images/menu/hero.webp">

</catalog-component-header>

*   [Design article](https://m3.material.io/components/menus) <!-- {.external} -->
*   [Source code](https://github.com/material-components/material-web/tree/main/menu)
    <!-- {.external} -->

<!-- catalog-only-start -->

<!--

## Interactive Demo

{% playgroundexample dirname=dirname,previewHeight=1000,editorHeight=700 %}

-->

<!-- catalog-only-end -->

## Usage

When opened, menus position themselves to an anchor. Thus, either `anchor` or
`anchorElement` must be supplied to `md-menu` before opening. Additionally, a
shared parent of `position:relative` should be present around the menu and it's
anchor.

Menus also render menu items such as `md-menu-item` and handle keyboard
navigation between `md-menu-item`s as well as typeahead functionality.
Additionally, `md-menu` interacts with `md-menu-item`s to help you determine how
a menu was closed. Listen for and inspect the `close-menu` custom event's
`details` to determine what action and items closed the menu.

<!-- no-catalog-start -->

!["Two filled buttons next to each other. The first one says set with idref and
the other says set with element ref. There is an opened menu anchored to the
bottom of the right button with the items: Apple, Banana,
Cucumber."](images/menu/usage.webp)

<!-- no-catalog-end -->
<!-- catalog-include "figures/menu/usage.html" -->

```html
<!-- Note the position: relative style -->
<span style="position: relative">
  <md-filled-button id="usage-anchor">Set with idref</md-filled-button>
  <md-menu id="usage-menu" anchor="usage-anchor">
    <md-menu-item headline="Apple"></md-menu-item>
    <md-menu-item headline="Banana"></md-menu-item>
    <md-menu-item headline="Cucumber"></md-menu-item>
  </md-menu>
</span>

<script type="module">
  // This example uses anchor as an ID reference
  const anchorEl = document.body.querySelector('#usage-anchor');
  const menuEl = document.body.querySelector('#usage-menu');

  anchorEl.addEventListener('click', () => { menuEl.show(); });
</script>

<span style="position: relative">
  <md-filled-button id="usage-anchor-2">Set with element ref</md-filled-button>
  <md-menu id="usage-menu-2">
    <md-menu-item headline="Apple"></md-menu-item>
    <md-menu-item headline="Banana"></md-menu-item>
    <md-menu-item headline="Cucumber"></md-menu-item>
  </md-menu>
</span>

<script type="module">
  // This example uses MdMenu.prototype.anchorElement to set the anchor as an
  // HTMLElement reference.
  const anchorEl = document.body.querySelector('#usage-anchor-2');
  const menuEl = document.body.querySelector('#usage-menu-2');
  menuEl.anchorElement = anchorEl;

  anchorEl.addEventListener('click', () => { menuEl.show(); });
</script>
```

### Submenus

You can compose submenus inside of an `<md-sub-menu-item>`'s `submenu` slot, but
first the `has-overflow` attribute must be set on the root `<md-menu>` to
disable overflow scrolling and display the nested submenus.

<!-- no-catalog-start -->

!["A filled button that says menu with submenus. There is a menu anchored to the
bottom of it with the first item selected that says fruits with A followed by a
right arrow. To the right is anchored a submenu with 3 items, Apricot, Avocado,
Apples. The Apples item is selected and has a left arrow before the text and
another submenu anchored to it on the left. That menu has three items, Fuji,
Granny Smith, and Red Delicious."](images/menu/usage-submenu.webp)

<!-- no-catalog-end -->
<!-- catalog-include "figures/menu/usage-submenu.html" -->

```html
<!-- Note the position: relative style -->
<span style="position: relative">
  <md-filled-button id="usage-submenu-anchor">
    Menu with Submenus
  </md-filled-button>
  <!-- Note the has-overflow attribute -->
  <md-menu has-overflow id="usage-submenu" anchor="usage-submenu-anchor">
    <md-sub-menu-item headline="Fruits with A">
      <!-- Submenu must be slotted into sub-menu-item's submenu slot -->
      <md-menu slot="submenu">
        <md-menu-item headline="Apricot"></md-menu-item>
        <md-menu-item headline="Avocado"></md-menu-item>

        <!-- Nest as many as you want and control menu anchoring -->
        <md-sub-menu-item
            headline="Apples"
            menu-corner="START_END"
            anchor-corner="START_START">
          <md-menu slot="submenu">
            <md-menu-item headline="Fuji"></md-menu-item>
            <md-menu-item headline="Granny Smith"></md-menu-item>
            <md-menu-item headline="Red Delicious"></md-menu-item>
          </md-menu>

          <!-- Arrow icons are helpful affordances -->
          <md-icon
              slot="start-icon"
              style="font-size: 24px;height:24px;">
            arrow_left
          </md-icon>
        </md-sub-menu-item>
      </md-menu>

      <!-- Arrow icons are helpful affordances -->
      <md-icon slot="end">arrow_right</md-icon>
    </md-sub-menu-item>

    <md-menu-item headline="Banana"></md-menu-item>
    <md-menu-item headline="Cucumber"></md-menu-item>
  </md-menu>
</span>

<script type="module">
  const anchorEl = document.body.querySelector('#usage-submenu-anchor');
  const menuEl = document.body.querySelector('#usage-submenu');

  anchorEl.addEventListener('click', () => { menuEl.show(); });
</script>
```

### Fixed menus

Internally menu uses `position: absolute` by default. Though there are cases
when the anchor and the node cannot share a common ancestor that is `position:
relative`, or sometimes, menu will render below another item due to limitations
with `position: absolute`. In most of these cases, you would want to use the
`fixed` attribute to position the menu relative to the window instead of
relative to the parent.

> Note: Fixed menu positions are positioned relative to the window and not the
> document. This means that the menu will not scroll with the anchor as the page
> is scrolled.

<!-- no-catalog-start -->

!["A filled button that says open fixed menu. There is an open menu anchored to
the bottom of the button with three items, Apple, Banana, and
Cucumber."](images/menu/usage-fixed.webp)

<!-- no-catalog-end -->
<!-- catalog-include "figures/menu/usage-fixed.html" -->

```html
<!-- Note the lack of position: relative parent. -->
<div style="margin: 16px;">
  <md-filled-button id="usage-fixed-anchor">Open fixed menu</md-filled-button>
</div>

<!-- Fixed menus do not require a common ancestor with the anchor. -->
<md-menu fixed id="usage-fixed" anchor="usage-fixed-anchor">
  <md-menu-item headline="Apple"></md-menu-item>
  <md-menu-item headline="Banana"></md-menu-item>
  <md-menu-item headline="Cucumber"></md-menu-item>
</md-menu>

<script type="module">
  const anchorEl = document.body.querySelector('#usage-fixed-anchor');
  const menuEl = document.body.querySelector('#usage-fixed');

  anchorEl.addEventListener('click', () => { menuEl.show(); });
</script>
```

## Accessibility

By default Menu is set up to function as a `role="menu"` with children as
`role="menuitem"`. A common use case for this is the menu button example, where
you would need to add keyboard interactions to the button to open the menu
([see W3C example](https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/examples/menu-button-actions/)<!-- {.external} -->).

Menu can also be adapted for other use cases.

The role of the `md-list` inside the menu can be set with the `type` attribute.
The role of each individual `md-menu-item` can also be set with the `type`
attribute. Anything else slotted into the menu that is not a list item in most
cases should be set to `role="none"`, and `md-divider` should have
`role="separator"`.

```html
<!--
  A simplified example of an autocomplete component – missing javascript logic for interaction.
-->
<md-filled-text-field
    id="textfield"
    type="combobox"
    aria-controls="menu"
    aria-autocomplete="list"
    aria-expanded="true"
    aria-activedescendant="1"
    value="Ala">
</md-filled-textfield>
<md-menu
    id="menu"
    anchor="textfield"
    role="listbox"
    aria-label="states"
    open>
  <md-menu-item type="option" id="0" headline="Alabama"></md-menu-item>
  <md-divider role="separator"></md-divider>
  <md-menu-item type="option" id="1" headline="Alaska" aria-selected="true">
  </md-menu-item>
</md-menu>
```

## Theming

Menus support [Material theming](../theming/README.md) and can be customized in
terms of color. Additionally, `md-menu` composes `md-list`, and each menu item
extends `md-list-item` ([see theming documentation](./list#theming)), so most
the tokens for those components can also be used for Menu.

### Menu Tokens

Token                                     | Default value
----------------------------------------- | -------------
`--md-menu-container-color`               | `--md-sys-color-surface-container`
`--md-menu-container-shape`               | `4px`
`--md-menu-item-container-color`          | `--md-sys-color-surface-container`
`--md-menu-item-selected-container-color` | `--md-sys-color-surface-container-highest`

*   [Menu tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-menu.scss)
    <!-- {.external} -->
*   [Menu item tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-menu-item.scss)
    <!-- {.external} -->
*   [List tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-list.scss)
    <!-- {.external} -->
*   [List item tokens](https://github.com/material-components/material-web/blob/main/tokens/_md-comp-list-item.scss)
    <!-- {.external} -->

### Example

<!-- no-catalog-start -->

![A filled button with the text Themed menu. Attached is a 3 item menu with the
items Apple, Banana, and Cucumber. They are both in a green hue and the menu has
a sharp 0px border radius.](images/menu/theming.webp)

<!-- no-catalog-end -->
<!-- catalog-include "figures/menu/theming.html" -->

```html
<style>
  ::root {
    background-color: #f4fbfa;
    --md-menu-container-color: #f4fbfa;
    --md-menu-container-shape: 0px;
    --md-menu-item-container-color: transparent;
    --md-list-item-container-shape: 28px;
    --md-list-item-label-text-color: #161d1d;
    --md-list-item-supporting-text-color: #3f4948;
    --md-list-item-trailing-supporting-text-color: #3f4948;
    --md-list-item-label-text-type: system-ui;
    --md-list-item-supporting-text-type: system-ui;
    --md-list-item-trailing-supporting-text-type: system-ui;
  }
  /* Styles for button and not relevant to menu */
  md-filled-button {
    --md-sys-color-primary: #006a6a;
    --md-sys-color-on-primary: #ffffff;
  }
</style>

<span style="position: relative">
  <md-filled-button id="theming-anchor">Themed menu</md-filled-button>
  <md-menu id="theming-menu" anchor="theming-anchor">
    <md-menu-item headline="Apple"></md-menu-item>
    <md-menu-item headline="Banana"></md-menu-item>
    <md-menu-item headline="Cucumber"></md-menu-item>
  </md-menu>
</span>

<script type="module">
  const anchorEl = document.body.querySelector("#theming-anchor");
  const menuEl = document.body.querySelector("#theming-menu");

  anchorEl.addEventListener("click", () => {
    menuEl.show();
  });
</script>
```

<!-- auto-generated API docs start -->

## API


### MdMenu

#### Properties

Property | Type | Default | Description
--- | --- | --- | ---
`anchor` | `string` | `''` | The ID of the element in the same root node in which the menu should align<br>to. Overrides setting `anchorElement = elementReference`.<br><br>__NOTE__: anchor or anchorElement must either be an HTMLElement or resolve<br>to an HTMLElement in order for menu to open.
`fixed` | `boolean` | `false` | Makes the element use `position:fixed` instead of `position:absolute`. In<br>most cases, the menu should position itself above most other<br>`position:absolute` or `position:fixed` elements when placed inside of<br>them. e.g. using a menu inside of an `md-dialog`.<br><br>__NOTE__: Fixed menus will not scroll with the page and will be fixed to<br>the window instead.
`quick` | `boolean` | `false` | Skips the opening and closing animations.
`hasOverflow` | `boolean` | `false` | Displays overflow content like a submenu.<br><br>__NOTE__: This may cause adverse effects if you set<br>`md-menu {max-height:...}`<br>and have items overflowing items in the "y" direction.
`open` | `boolean` | `false` | Opens the menu and makes it visible. Alternative to the `.show()` and<br>`.close()` methods
`xOffset` | `number` | `0` | Offsets the menu's inline alignment from the anchor by the given number in<br>pixels. This value is direction aware and will follow the LTR / RTL<br>direction.<br><br>e.g. LTR: positive -> right, negative -> left<br> RTL: positive -> left, negative -> right
`yOffset` | `number` | `0` | Offsets the menu's block alignment from the anchor by the given number in<br>pixels.<br><br>e.g. positive -> down, negative -> up
`listTabIndex` | `number` | `-1` | The tabindex of the underlying list element.
`type` | `string` | `'menu'` | The role of the underlying list element.
`typeaheadDelay` | `number` | `DEFAULT_TYPEAHEAD_BUFFER_TIME` | The max time between the keystrokes of the typeahead menu behavior before<br>it clears the typeahead buffer.
`anchorCorner` | `string` | `'END_START'` | The corner of the anchor which to align the menu in the standard logical<br>property style of <block>_<inline>.<br><br>NOTE: This value may not be respected by the menu positioning algorithm<br>if the menu would render outisde the viewport.
`menuCorner` | `string` | `'START_START'` | The corner of the menu which to align the anchor in the standard logical<br>property style of <block>_<inline>.<br><br>NOTE: This value may not be respected by the menu positioning algorithm<br>if the menu would render outisde the viewport.
`stayOpenOnOutsideClick` | `boolean` | `false` | Keeps the user clicks outside the menu.<br><br>NOTE: clicking outside may still cause focusout to close the menu so see<br>`stayOpenOnFocusout`.
`stayOpenOnFocusout` | `boolean` | `false` | Keeps the menu open when focus leaves the menu's composed subtree.<br><br>NOTE: Focusout behavior will stop propagation of the focusout event. Set<br>this property to true to opt-out of menu's focuout handling altogether.
`skipRestoreFocus` | `boolean` | `false` | After closing, does not restore focus to the last focused element before<br>the menu was opened.
`defaultFocus` | `string` | `'FIRST_ITEM'` | The element that should be focused by default once opened.<br><br>NOTE: When setting default focus to 'LIST_ROOT', remember to change<br>`list-tabindex` to `0` when necessary.
`typeaheadController` | `TypeaheadController` | `function { ... }` | Handles typeahead navigation through the menu.
`anchorElement` | `HTMLElement & Partial<SurfacePositionTarget>` | `undefined` | The element which the menu should align to. If `anchor` is set to a<br>non-empty idref string, then `anchorEl` will resolve to the element with<br>the given id in the same root node. Otherwise, `null`.
`items` | `MenuItem[]` | `undefined` | The menu items associated with this menu. The items must be `MenuItem`s and<br>have both the `md-menu-item` and `md-list-item` attributes.

#### Methods

Method | Parameters | Returns | Description
--- | --- | --- | ---
`close` | _None_ | `void` | 
`show` | _None_ | `void` | 
`activateNextItem` | _None_ | `MenuItem` | Activates the next item in the menu. If at the end of the menu, the first<br>item will be activated.
`activatePreviousItem` | _None_ | `MenuItem` | Activates the previous item in the menu. If at the start of the menu, the<br>last item will be activated.

#### Events

Event | Type | Bubbles | Composed | Description
--- | --- | --- | --- | ---
`opening` | `undefined` | No | No | Fired before the opening animation begins
`opened` | `undefined` | No | No | Fired once the menu is open, after any animations
`closing` | `undefined` | No | No | Fired before the closing animation begins
`closed` | `undefined` | No | No | Fired once the menu is closed, after any animations

### MdMenuItem

#### Properties

Property | Type | Default | Description
--- | --- | --- | ---
`isMenuItem` | `boolean` | `true` | READONLY: self-identifies as a menu item and sets its identifying attribute
`keepOpen` | `boolean` | `false` | Keeps the menu open if clicked or keyboard selected.
`type` | `string` | `'menuitem'` | 
`headline` | `string` | `''` | The primary, headline text of the list item.
`supportingText` | `string` | `''` | The one-line supporting text below the headline. Set<br>`multiLineSupportingText` to `true` to support multiple lines in the<br>supporting text.
`multiLineSupportingText` | `boolean` | `false` | Modifies `supportingText` to support multiple lines.
`trailingSupportingText` | `string` | `''` | The supporting text placed at the end of the item. Overridden by elements<br>slotted into the `end` slot.
`disabled` | `boolean` | `false` | Disables the item and makes it non-selectable and non-interactive.
`type` | `string` | `'listitem'` | Sets the role of the list item. Set to 'nothing' to clear the role. This<br>property will be ignored if `href` is set since the underlying element will<br>be a native anchor tag.
`isListItem` | `boolean` | `true` | READONLY. Sets the `md-list-item` attribute on the element.
`href` | `string` | `''` | Sets the underlying `HTMLAnchorElement`'s `href` resource attribute.
`target` | `string` | `''` | Sets the underlying `HTMLAnchorElement`'s `target` attribute when `href` is<br>set.
`tabIndex` | `number` | `0` | 

#### Events

Event | Type | Bubbles | Composed | Description
--- | --- | --- | --- | ---
`close-menu` | `CloseMenuEvent` | Yes | Yes | Requests the parent menu to deselect other<br>items when a submenu opens.

### MdSubMenuItem

#### Properties

Property | Type | Default | Description
--- | --- | --- | ---
`anchorCorner` | `string` | `'START_END'` | The anchorCorner to set on the submenu.
`menuCorner` | `string` | `'START_START'` | The menuCorner to set on the submenu.
`hoverOpenDelay` | `number` | `400` | The delay between mouseenter and submenu opening.
`hoverCloseDelay` | `number` | `400` | The delay between ponterleave and the submenu closing.
`selected` | `boolean` | `false` | Sets the item in the selected visual state when a submenu is opened.
`isMenuItem` | `boolean` | `true` | READONLY: self-identifies as a menu item and sets its identifying attribute
`keepOpen` | `boolean` | `false` | Keeps the menu open if clicked or keyboard selected.
`type` | `string` | `'menuitem'` | 
`headline` | `string` | `''` | The primary, headline text of the list item.
`supportingText` | `string` | `''` | The one-line supporting text below the headline. Set<br>`multiLineSupportingText` to `true` to support multiple lines in the<br>supporting text.
`multiLineSupportingText` | `boolean` | `false` | Modifies `supportingText` to support multiple lines.
`trailingSupportingText` | `string` | `''` | The supporting text placed at the end of the item. Overridden by elements<br>slotted into the `end` slot.
`disabled` | `boolean` | `false` | Disables the item and makes it non-selectable and non-interactive.
`type` | `string` | `'listitem'` | Sets the role of the list item. Set to 'nothing' to clear the role. This<br>property will be ignored if `href` is set since the underlying element will<br>be a native anchor tag.
`isListItem` | `boolean` | `true` | READONLY. Sets the `md-list-item` attribute on the element.
`href` | `string` | `''` | Sets the underlying `HTMLAnchorElement`'s `href` resource attribute.
`target` | `string` | `''` | Sets the underlying `HTMLAnchorElement`'s `target` attribute when `href` is<br>set.
`tabIndex` | `number` | `0` | 

#### Methods

Method | Parameters | Returns | Description
--- | --- | --- | ---
`show` | `onOpened` | `void` | Shows the submenu.
`close` | `onClosed` | `void` | Closes the submenu.

#### Events

Event | Type | Bubbles | Composed | Description
--- | --- | --- | --- | ---
`deactivate-items` | `CloseMenuEvent` | Yes | Yes | Requests the parent menu to deselect other items when<br>a submenu opens.
`request-activation` | `undefined` | No | No | Requests the parent make the element focusable and<br>focuses the item.
`deactivate-typeahead` | `undefined` | No | No | Requests the parent menu to deactivate the<br>typeahead functionality when a submenu opens
`activate-typeahead` | `undefined` | No | No | Requests the parent menu to activate the typeahead<br>functionality when a submenu closes
`close-menu` | `CloseMenuEvent` | Yes | Yes | Requests the parent menu to deselect other<br>items when a submenu opens.

<!-- auto-generated API docs end -->
