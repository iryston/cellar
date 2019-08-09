# Cellar CSS grid system

**Responsive, Sass-based, BEM-syntax CSS grid system**
Based on [Avalanche](https://github.com/colourgarden/avalanche).

## Benefits of Cellar

- Easy configurable naming conventions.
- Only create the selectors you'll actually use.
- No code duplication.
- No floats. No clears. No .last.
- Nesting to infinity and beyond.
- Easy beakpoint naming.
- Integrated media query mixin. Connect media queries to breakpoints.

## Demo

View [the demo](https://iryston.github.io/cellar/) to see Cellar in action!

## Installation

1. Import `_cellar.scss` to your project via NPM or manually copying to vendor folder (`@import "vendor/cellar"`)
2. Override settings to fit your requirements or use the defaults
3. Compile!

### NPM

`npm install --save cellar`

## Usage

Example of a two column, responsive, centered grid.

```html
<div class="row row_center">
  <div class="row__col row__col_3/4 row__col_1/2_s"></div>
  <div class="row__col row__col_1/4 row__col_1/2_s"></div>
</div>
```

## Settings

**`$clr-namespace`**
Global prefix for layout and column class names. Default: `row`.

**`$clr-element-name`**
Element (in a BEM context) or column name. Default: `col`.

**`$clr-element-class-chain`**
Chain characters/separator between BEM block and element. Default: `__`.

**`$clr-modifier-class-chain`**
Chain characters/separator between BEM block and modifier. Default: `_`.

**`$clr-breakpoint-class-chain`**
Chain characters/separator between width class and breakpoint. Default: `_`.

**`$clr-width-class-chain`**
Prefix for width class names. Default: `'_'`.

**`$clr-gutter`**
Gutter width between columns. Default: `20px`.

**`$clr-width-class-style`**
Naming style of width classes. Default: `'fraction'`. Options: `fraction` (1/2, 3/4 etc), `percentage` (25, 50 etc), `fragment` (1-of-3, 4-of-5 etc).
*N.B. If using percentage then `$clr-width-class-namespace` above cannot be null. Cellar escapes leading integers for fraction and fragment naming styles but this isn't possible with percentage style as Sass attempts to escape the whole number (e.g. 50 instead of just 5 or 30 instead of just 3) so fails*.

**`$clr-widths`**
Sass list of width denominator values (when expressed as a fraction). For example, 2 produces 1/2 width class, 3 produces 1/3 and 2/3 width classes etc. Default: `( 2, 3, 4, 6, 10 )`.
*N.B. This setting has a large impact on the size of your compiled CSS. Avoid bloat by inputting just the numbers you'll use.*

**`$clr-enable-responsive`**
Enable/disable the inclusion of responsive width classes. With this enabled, class names (for denominators set above) will be created for each of your breakpoint aliases (set below). Default: `true`.

**`$clr-breakpoints`**
Sass map of responsive breakpoint aliases and associated media queries (in key-value pairs).
*N.B. This setting has a large impact on the size of your compiled CSS. Avoid bloat by inputting just the breakpoints you'll use.*

Default (Bootstrap based):

```scss
(
  "sm":       "screen and (min-width: 576px)",
  "md":       "screen and (min-width: 768px)",
  "lg":       "screen and (min-width: 992px)",
  "xl":       "screen and (min-width: 1200px)"
) !default; // Responsive breakpoints. Add/remove as appropriate
```

Large range of sizes:

```scss
(
  "xs":      "screen and (min-width: 320px)",
  "xso":     "screen and (min-width: 320px) and (max-width: 639px)",
  "s":       "screen and (min-width: 640px)",
  "so":      "screen and (min-width: 640px) and (max-width: 799px)",
  "m":       "screen and (min-width: 800px)",
  "mo":      "screen and (min-width: 800px) and (max-width: 1023px)",
  "l":       "screen and (min-width: 1024px)",
  "lo":      "screen and (min-width: 1024px) and (max-width: 1199px)",
  "xl":      "screen and (min-width: 1200px)",
  "xlo":     "screen and (min-width: 1200px) and (max-width: 1399px)",
  "xxl":     "screen and (min-width: 1400px)",
  "retina":  "screen and (-webkit-min-device-pixel-ratio: 2), screen and (min-resolution: 192dpi), screen and (min-resolution: 2dppx)"
) !default; // Responsive breakpoints. Add/remove as appropriate
```

## Grid layouts

Apply as modifier classes to your base `row` element. For example; `<div class="row row--center">`.

All optionable layouts listed below are switched off by default. Set to `true` to enable.

**`$clr-enable-center`**
All columns are horizontally centered within the row.

**`$clr-enable-column-center`**
Center an individual column within the row.
*N.B. Class should be applied to an individual column, not the row container. For example; `<div class="row__col row__col--center">`.*

**`$clr-enable-right`**
All columns are horizontally aligned to the right within the container.

**`$clr-enable-middle`**
All columns are vertically centered within in the container.

**`$clr-enable-bottom`**
All columns are vertically aligned to the bottom of the container.

**`$clr-enable-flush`**
Gutters removed between columns.

**`$clr-enable-tiny`**
Gutters between columns set to a quarter of the global gutter value. Default: `5px`.

**`$clr-enable-small`**
Gutters between columns set to half of the global gutter value. Default: `10px`.

**`$clr-enable-large`**
Gutters between columns set to double the global gutter value. Default: `40px`.

**`$clr-enable-huge`**
Gutters between columns set to quadruple the global gutter value. Default: `80px`.

**`$clr-enable-auto`**
All columns take up an unspecified width set by their content.

**`$clr-enable-rev`**
Columns are displayed in the opposite of their source order.

## Media query

Cellar includes a media query mixin that makes use of the breakpoint aliases you set. This enables better coupling between your grid and other responsive content items. Usage as follows.

```scss
@include clr-mq(xl){
  .content-item{
    /* responsive CSS */
  }
}
```

## Browser support

All modern browsers are supported and Internet Explorer from IE9 upwards. If IE8 support is required then all that is needed is a pixel-value to be set for `font-size` on `.row__col`. This is due to IE8 not supporting rem units. Use of a 'rem-to-px' check during build is recommended.

## Contributing

When issuing a pull request to improve this project, please:

1. Rigourously comment your code, particularly where new variables are introduced or manipulated
2. Ensure your work passes the stylelint linter.
3. Be as descriptive as possible in your commit message

## Questions

If you have any questions or need some help then feel free to [open an issue](https://github.com/iryston/cellar/issues/new).
