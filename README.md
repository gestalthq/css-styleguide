# Elements of CSS Style
This guide documents the style, organization, and naming conventions used to write and maintain our CSS.

Note/disclaimer from author: from my experience, maintaining clean Markup/CSS in a large application is both chore and an artform. I borrow from a lot of people below, but what makes the most sense for our app is ultimately up to the developer. Read it, understand it, follow it, update it, criticize it, correct it, extend it, and document it.


## Idiomatic CSS
CSS is written to adhere (fairly strictly) to Nicholas Gallagher's [Principles of Writing Idiomatic CSS](https://github.com/necolas/idiomatic-css). The most important section to take note of is "4. Format", included and modified below:

### Format

The chosen code format must ensure that code is: easy to read; easy to clearly
comment; minimizes the chance of accidentally introducing errors; and results
in useful diffs and blames.

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include a single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes,
  e.g., `content: ""`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero-values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function
  values.
* Include a semi-colon at the end of the last declaration in a declaration
  block.
* Place the closing brace of a ruleset in the same column as the first
  character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    font-family: helvetica, arial, sans-serif;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
    color: #333;
}

.selector-a,
.selector-b {
    padding: 10px;
}
```

#### Declaration order

If declarations are to be consistently ordered, it should be in accordance with
a single, simple principle.

Smaller teams may prefer to cluster related properties (e.g. positioning and
box-model) together.

```css
.selector {
    /* Positioning */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 10;
    opacity: 1;

    /* Display & Box Model */
    box-sizing: border-box;
    display: inline-block;
    overflow: hidden;
    width: 100px;
    height: 100px;
    min-width: 50px;
    min-height: 50px;
    margin: 10px;
    padding: 10px;
    border: 10px solid #333;
    border-radius: 10;

    /* Typography */
    font-family: sans-serif;
    font-size: 16px;
    line-height: 1.5em;
    text-align: center;
    text-decoration: underline;
    text-transform: uppercase;

    /* Other */
    background: #000;
    color: #fff;
}
```

Larger teams may prefer the simplicity and ease-of-maintenance that comes with
alphabetical ordering.

#### Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Width/height, paddings, margins, and top/right/bottom/left pairs can exist in single-line format.

```css
.selector {
    position: relative;
    top: 0; left: 0; right: 0;
    display: inline-block;
    width: 100px; height: 150px;
}
```

## SMACSS
Stylesheets are structured and organized following Jonathan Snook's [Scalable and Modular Architecture for CSS (SMACSS)](https://smacss.com/). This format is taken loosely (as recommended), and is adapted more formally as needed based on the complexity of the application. Currently, these are the major divisions:

### layout.css (base and layout in SMACSS)
layout.css should include base and layout rules outlined under SMACSS. This generally include styles for the outer container of the site, and style generally anything that would be included in a Rails layout. That said, layout.css should not need to be touched if changes are just intended to extend the current design.


### components.css (modules in SMACSS)
components.css includes independently reusable modules that do not belong to any particular view or layout. They are generally design components that can be mixed and matched accordingly. Components are usually static or relatively positioned blocks or inline-blocks, fluid to the contained content or fills to the containing parent container, and has independent margins and paddings. Examples are buttons, tooltips, modals, reused custom controls...

### variables.css (themes in SMACSS)

### page-specific.css
page-specific.css includes styles for laying out a particular page. Aside from things handled by layout.css and components.css, everything else falls into this file. Therefore, this file serves as a good code smell for when styles (or design) needs to be refactored. Common components, if makes sense, should be styled in a reusable manner and moved into components.css when possible. If the application grows and styles become more complex, it makes sense to break this further into styles by body-class, or styles by body-id.



## Block Element Modifier (BEM) Methodology
Naming follows (loosely) Yandex's [Block Element Modifier (BEM)](http://bem.info/) methodology for namespacing classes:

- A single hyphen is used for adjective-noun separation (e.g., payroll-calculator)
- A double hypen is used for actual namespacing between blocks and its elements/modifiers (e.g., payroll-calculator--header--dark)

**blocks** are major logical design components/widgets (e.g., tooltip)
**elements** are the technical/structural components that make up that block (e.g., tooltip--handle, tooltip--bubble)
**modifiers** are the variations/configurations to that block or element (e.g., tooltip--horizontal, tooltip--vertical)

## Other
BEM gives you the freedom to name your blocks/components anything, but I also tend to follow [Twitter Bootstrap](http://getbootstrap.com/)'s markup conventions whenever I can (e.g., control-groups, heroes, wells, etc.)