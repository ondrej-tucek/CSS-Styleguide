CSS-Styleguide
==============

A few simple Guidelines and ideas I wrote done for myself to craft consistent
and maintainable CSS.

### Comments notation
Keep files as simple, short and modular as possible. Each one has a heading.

    /*------------------------------------*\
        $File Heading
    \*------------------------------------*/

Each section in a file has a heading

    /**
    * Section Heading or multi-line comment
    */
    .class {
        position: relative;
    }

Sometimes one just needs a short comment

    /* Simple one-line comment */
    .class {
        color: red;
    }


### Declaration order
Keeping a consitent declaration order throughout the all CSS files helps
organization and speeds up the development process.

    .class {
        /* Positioning */
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 1;

        /* Box-Model and Display */
        display: block;
        overflow: hidden;
        width: 100px;
        height: 50px;
        margin-top: 10px;
        margin-right: 10px;
        margin-bottom: 20px;
        margin-left: 10px;
        padding: 10px;

        /* Typography */
        color: #000;
        font-family: Georgia, serif;
        font-size: 1rem;
        line-height: 1.3;

        /* Visuals */
        background-color: #ccc;
        border: 1px solid #000;
        border-radius: 3px;
        opacity: .8;
    }


### Misc
* Add UTF-8 charset `@charset "UTF-8";`
* Don't use CSS @import, always combine all CSS files into one and minify it
* No id's for styling, use classes and abstain from styling html elements
* Use `js_` prefixed classes or id's for Javscript
* Four spaces indenting
* Only three levels deep nesting
* Line length: 80 characters
* Multiple selectors, each in new line
* BEM-style class names (`nav`, `nav__item`, `nav--small`, `nav__item--new`)
* OOCSS, build reusable modules and patterns
* Don't be afraid of `div`'s and classes if they make sense and help the
  organization
* Don't use `!important` (Exceptions could be state styles like `is-false`)
* No shorthand notations if possible (`margin-bottom: 20px;` instead of
  `margin: 0 0 20px 0;`)
* No prefixing, let autoprefixer do the work
* Omit units and leading zeros if possible (`top: 0;` or `opacity: .7;`)
* Use Hhx color codes shorthand notation: `#000` instead of `#000000` and write
  them in lowercase letters
* Don't use magic numbers. (`position: relative; top: 3px`)
* Use (inline) SVG if possible
* Use `rem` with `px` fallback
* Use a Sass mixin for site-wide breakpoints
* Don't name breakpoints after actual devices (NO: `@inlcude breakpoint(table) {}`)
  YES: `@include breakpoint(bp1) {}`)
* Nest media queries/Sass breakpoint mixin inside of selectors
        .class {
            padding: 10px;

            @media (min-width: 500px) {
                padding: 20px;
            }
        }
* ...