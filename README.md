CSS-Styleguide
==============

A few simple guidelines and ideas I wrote down for myself to craft consistent
and maintainable CSS. // This is a living document and is subject to change.

### General things to consider
* Think [OOCSS](https://github.com/stubbornella/oocss/tree/master/oocss) and
build reusable modules and patterns
* Don't be afraid of additional non-semantic `div`'s and classes if they make
sense and help organizing and modularizing the code. Think separation of content
and container. #OOCSS
* Responsive Design is more than just squishing the content. Think Progressive
Enhancement/Responsible Responsive Design
* Start mobile first
* Use inline SVGs if possible

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

### Comments notation
Keep files as simple, short and modular as possible.
Each one has a heading, followed by two blank lines. If a file consists of more than one module/sections, use this style to separate them. Then this heading-style is preceded by three blank lines.

    /*------------------------------------*\
        File or Module/Section Heading
    \*------------------------------------*/

Use this style for all explanatory and multi-line comments

    /**
    * Explanatory comment
    * Can be multi-line
    */
    .class {
        position: relative;
    }

Sometimes one just needs a short, inline comment:

    .class {
        color: red; /* This is red because it's important */
    }

### Always combine all SCSS files into one CSS file and minify it
style.scss:

    /**
     * Assets
     */
    @import "_assets/vars";
    @import "_assets/mixins";
    @import "_assets/normalize";
    @import "_assets/fonts";


    /**
     * Modules
     */
    @import "_modules/site-nav";
    @import "_modules/ad-box";

    /* and so on... */

This will result in style.min.css.

### Use the BEM-style for class names, variables and all sorts of things

    .nav {
        /* ... */
    }

    .nav--small {
        /* ... */
    }

    .nav__item {
        /* ... */
    }

    .nav__item--new {
        /* ... */
    }

    $blue: #0e649a;
    $blue__dark: #083654;
    $blue__dark--hover: #235f85;

    $header__height: 50px;
    $header__height--fixed: 20px;

[Read more.](http://martinwolf.org/2014/05/15/making-use-of-the-bem-naming-system/)

### Don't nest deeper than three levels

    .class {
        margin-bottom: 20px;

        .class-2 {
            background-color: blue;

            p {
                font-size: 1.3rem;
            }
        }
    }

### Don't use id's for styling, only use classes and abstain from styling html elements
Do:

    .class {
        color: #000;
    }

Don't do:

    #id {
        color: #000;
    }

    header {
        background-color: blue;
    }

    div.ad-box {
        border: 1px solid red;
    }

But you can select html elements like `p`, `blockquote`, and other text-based ones.

### Prefixed classes or id's which are used by JavaScript

    <a class="more-link js_more-link">Read more...</a>

    <nav class="page-nav" id="js_page-nav"></nav>

### Add Sass `@extend`s at the beginning of properties

    .class {
        @extend %clearfix;

        padding: 10px;
        font-size: 1.3rem;
    }

### Add UTF-8 charset

    @charset "UTF-8";


### Four spaces indenting
Sublime Text Settings:

    "tab_size": 4,
    "translate_tabs_to_spaces": true,

### Line length: 80 characters
Sublime Text Setting:

    "rulers": [80]

### Multiple selectors, each in new line

    .class-1,
    .class-2,
    .class-3 {
        font-size: 1.5rem;
    }

### Don't use `!important`
An exception could be a state style like

    .is-false {
        color: red !important;
    }

### Don't use shorthand notations if possible
If you only want to set one value, be explicit, don't set values you don't have
to.

Use:

    .class {
        margin-bottom: 20px;
    }

**Don't** use:

    .class {
        margin: 0 0 20px 0;
    }

### Omit units and leading zeros

    .class {
        top: 0;
        opacity: .7;
    }

### Use Hex color codes shorthand notation and lowercase letters

    .class {
        color: #fff;
        background-color: #000;
    }

### Don't use magic numbers
... which just happen to work for no particular reason.

    .class {
        position: relative;
        top: 3px;
    }

### No prefixing, let autoprefixer do the work

    .class {
        box-sizing: border-box;
    }

Will be automatically outputted as

    .class {
        -webkit-box-sizing: border-box;
           -moz-box-sizing: border-box;
                box-sizing: border-box;
    }

### Use a Sass mixin for site-wide breakpoints
And don't name breakpoints after actual devices like `iphone` or `tablet`. Use
arbitrary names.

    @mixin breakpoint($point) {
        @if $point == bp1 {
            @media (min-width: 460px) {
                @content;
            }
        }
        @if $point == bp2 {
            @media (min-width: 640px) {
                @content;
            }
        }
        @elseif $point == retina {
            @media (-webkit-min-device-pixel-ratio: 1.25),
                   (min-resolution: 120dpi)
                   (-o-min-device-pixel-ratio: 5/4) {
                @content;
            }
        }
    }


### Nest media queries/Sass breakpoint mixin inside of selectors

    .class {
        padding: 10px;

        @media (min-width: 500px) {
            padding: 20px;
        }
    }

    .class {
        font-size: 2rem;

        @include breakpoint(bp1) {
            font-size: 1.5rem;
        }
    }

### Use `rem` with `px` fallback and `px` value for body base `font-size`
THIS IS NOT YET TESTED AND USED:

    $font-size__base: 16;
    $font-size__body: font-size__base +px;

    @mixin font-size($size) {
        font-size: $size +px;
        font-size: $size / $font-size__base +rem;
    }

    body {
        font-size: $font-size__body +px;
    }

    .class {
        @include font-size(20);
    }

    /* CSS Output: */
    .class {
        font-size: 20px; /* Fallback */
        font-size: 1.25rem;
    }
