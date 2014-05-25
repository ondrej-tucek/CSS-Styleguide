CSS-Styleguide
==============

A few simple rules and ideas I wrote done for myself to craft consistent and
maintainable CSS.

## Add UTF-8 charset

    @charset "UTF-8";

## Comments notation
Keep files as simple, short and modular as possible. Each one has a heading.

    /*------------------------------------*\
        $File Heading
    \*------------------------------------*/

Each section in a file has a heading

    /**
    * Section Heading or longer comment
    */
    .class {
        position: relative;
    }

Sometimes one just needs a short comment

    /* Simple one-line comment */
    .class {
        color: red;
    }


## Declaration order
Keeping consitent declaration order throughout the CSS helps organization and
speeds up the development

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
        margin-right: 20px;
        margin-bottom: 10px;
        margin-left: 20px;
        padding-top: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        padding-left: 10px;

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

        /*
    }

## Misc
* no id's for styling, use classes and abstain from styling html elements
* Use `js_` prefixed classes or id's for Javscript
* four spaces indenting
* only three levels deep nesting
* line length: 80 characters
* multiple selectors, each in new line
* BEM-style class names (`nav`, `nav__item`, `nav--small`, `nav__item--new`)
* OOCSS, build reusable modules and patterns
* don't be afraid of `div`'s and classes if they make sense and help the
  organisation
* no shorthand notations if possible (`margin-bottom: 20px;` instead of
  `margin: 0 0 20px 0;`)
* no prefixing, let autoprefixer do the work
* omit units and leading zeros if possible (`top: 0;` or `opacity: .7;`)
* hex color codes shorthand notation: `#000` instead of `#000000`
* hey color codes in lowercase