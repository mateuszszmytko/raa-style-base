# Raa Style Base
Raa Style Base is a modular [Sass](http://sass-lang.com/) framework, fully based on  mixins and functions. Each module (set of mixins and functions) is independent and doesn't require the use of other modules to work. When no modules are used, framework will output no code.

Raa Style Base helps you to easily create custom grid, container, manage breakpoints, responsive fonts and colors.


## Installation
`npm install @raa/style-base` with NPM or `yarn add @raa/style-base` with yarn.

**Make sure you have [node](https://nodejs.org/) installed.*

## Basic usage
To use Raa Style Base, you need to import package in your main `.scss` file, e.g. `main.scss` or `style.scss` and call initial mixin.
```scss
@import '@raa/style-base';

@include raa-style-base((
    xs: 0,       
    sm: 576px, 
    md: 768px, 
    lg: 992px, 
    xl: 1200px, 
));

// your code
* {
    outline: none;
    box-sizing: border-box;
}

```
In Raa Style Base initial mixin, you can define breakpoints map. Every module will be based on it. You need to name each breakpoint and set its value, e.g. breakpoint name `md` will be `768px`. You can use `em` as well.

But it will output no code anyway, you need to use one of module listed below.

## Layout Modules

### 1. Grid
Grid module contains only one mixin and create responsive grid based on flex.

#### Define
```scss
// create-grid($class-name: 'grid', $columns-count: 12, $gutter: 30px);
@include create-grid('grid', 12, 30px);
```

#### Usage
```html
<div class="grid">
    <div class="grid__item md-6 xl-4">
        It will take 50% (6/12) of space when min-width >= 768px and 33.(3)% (4/12) when min-width >= 1200px
    </div>
    <div class="grid__item md-6 xl-4">
        It will take 50% (6/12) of space when min-width >= 768px and 33.(3)% (4/12) when min-width >= 1200px
    </div>
</div>
```
Column classes will be based on your breakpoints map.
You can check more examples [here](https://stackblitz.com/edit/raa-base-style-examples?file=base-style.scss).

---
### 2. Container
Container module, like Grid, contains only one mixin. 
#### Define
```scss
// create-container($class-name: 'container', $container-max-widths, $gutter: 30px)
@include create-container('container', ( sm: 540px, md: 720px, lg: 960px, xl: 1170px ), 30px);
```
This mixin will create responsive container, based on breakpoints map. E.g. when screen size will be 768px (`sm` breakpoint), container will have 720px.


## Utility Modules
### 1.Media
**Media** module contains two simple mixins, which help you define your media queries, based on breakpoints map.

#### Usage
```scss
.button {
    display: inline-block;

    padding: 5px 15px;

    &--wide {
        padding: 5px 25px;
    }
}

// it will output media query with 576px min-width.
@include media('md') { 
    .button {
        padding: 5px 35px;

        &--wide {
            padding: 5px 65px;
        }
    }
}

// it will output media query with 991px max-width.
@include media-max('lg') { 
    .button {
        padding: 5px 35px;

        &--wide {
            padding: 5px 65px;
        }
    }
}
```

#### Functions and mixins
| Name        | Type           | Description  |
| ------------- |-------------| -----|
| **media**              | *mixin*    | Create media query with min-width based on breakpoints map. |
| **media-max**          | *mixin*    | Create media query with max-width based on breakpoints map. |

---
### 2. Colors
Colors module helps you manage your site colors, you can define your colors and use them by using `color` function.


#### Define
In your main `.scss` file
```scss
@import '@raa/style-base';

@include define-colors((
    'primary': #eb8a23,
    'text': #111,
    'background': #fff,
));

// you can add your color as well
@include add-color('secondary', '#da14aa'); 
```
You can set your custom names and values.

#### Usage
```scss
body {
    background: color('background');
    color: color('text');
}

.button {
    background: color('primary');

    &--secondary {
        background: color('secondary');
    }
}

```

#### Functions and mixins
| Name        | Type           | Description  |
| ------------- |-------------| -----|
| **define-colors** | *mixin* | Define your colors map. |
| **add-color**              | *mixin*    | Add color to your colors map. |
| **color**          | *function*    | Return color value based on argument. |
---
### 3. Fonts
Fonts module helps you to manage your fonts. There are 2 maps to define, for font families and font sizes.

#### Define
In your main `.scss` file
```scss
@import '@raa/style-base';

@include define-fonts((
    'default': 'Open Sans',
    'heading': 'Roboto',
));

@include define-font-sizes(( 
    'title': (xs: 24px, lg: 28px, xl: 32px), 
    'default': 1rem, 
    'small': .75rem,
    'tiny': 9px 11px 
));

```
When defining your font-sizes map, you can use nested maps as well (see `title` value), which will create responsive font-sizes (`font-size` will be based on breakpoints). E.g. when use `title` value, on `xs` (screen >= 0) element will have 24px font-size, but when reach `lg` (screen >= 992px), `font-size` will change to `28px` (and 32px when reach `xl`).

You can use arrays as well (see `tiny` value), it will works like maps. Each value will will use breakpoint with this index. E.g. `9px` on `xs`, `11px` on `sm`.

#### Usage
```scss
// set base font-size to 1rem and base font-family to `Open sans`.
body {
    @include font('default', 'default');
    background: color('background');
}

// set font-size to 24px, but when reach 'lg' (screen >= 992px), it will be 28px
.site-title {
    @include font('title');
}

h1,
h2 {
    font-family: font-family('heading');
}

```

#### Functions and mixins
| Name        | Type           | Description  |
| ------------- |-------------| -----|
| **define-fonts** | *mixin* | Define your fonts map. |
| **add-font**              | *mixin*    | Add font to your fonts map. |
| **define-font-sizes** | *mixin* | Define your fonts-sizes map. |
| **add-font-size**              | *mixin*    | Add font-size to your font-sizes map. |
| **font-family**          | *function*    | Return font-valie value based on argument. |
| **font**          | *function*    | Return `font-size` (and `font-family` if defined) property. |

---

## Example usage
```scss
@import '@raa/style-base';

// call initial mixin
@include raa-style-base((
    xs: 0,       
    sm: 576px, 
    md: 768px, 
    lg: 992px, 
    xl: 1200px, 
));

// define your colors
@include define-colors((
    'primary': #eb8a23,
    'text': #111,
    'background': #fff,
));

//define your fonts
@include define-fonts((
    'default': 'Open Sans',
    'heading': 'Roboto',
));

@include define-font-sizes(( 
    'title': (xs: 24px, lg: 28px, xl: 32px), 
    'default': 1rem, 
    'small': .75rem,
    'tiny': 9px 11px 
));

//create container and grid
@include create-container('container', ( sm: 540px, md: 720px, lg: 960px, xl: 1170px ), 30px);
@include create-grid('grid', 12, 30px);
```

