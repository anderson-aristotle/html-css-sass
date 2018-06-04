[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# HTML, CSS, & Sass

## Prerequisites

-   [ga-wdi-boston/html-css](https://git.generalassemb.ly/ga-wdi-boston/html-css)
-   [ga-wdi-boston/html-css-layout](https://git.generalassemb.ly/ga-wdi-boston/html-css-layout)

## Objectives

-   Explain nested CSS rules
-   Store style rules in variables
-   Calculate styles using variables and arithmetic operations
-   Make a custom mixin to DRY out CSS

## Preparation

1.  Fork and clone this repository.
 [FAQ](https://git.generalassemb.ly/ga-wdi-boston/meta/wiki/ForkAndClone)
1.  Create a new branch, `training`, for your work.
1.  Checkout to the `training` branch.
1.  Install dependencies with `npm install`.

## Sass

[Sass](http://sass-lang.com) (Syntactically Awesome Style Sheets) is a powerful
[CSS preprocessor](https://github.com/showcases/css-preprocessors). CSS
preprocessors use programming languages like Ruby, C, or JavaScript to add
features to your stylesheets that are absent from native CSS.
Some examples include:

-   variables,
-   calculations,
-   and extensions or mix-ins.

Examples of how you can use a preprocessor like Sass:

-   [Build A Pleasing Color Scheme Programmatically](http://thesassway.com/advanced/how-to-programtically-go-from-one-color-to-another-in-sass)
-   [Build Your Own Custom Grid](http://webdesign.tutsplus.com/tutorials/a-simple-responsive-grid-made-even-better-with-sass--cms-21540)
-   [Make Your Application Themeable](http://webdesign.tutsplus.com/tutorials/how-to-use-sass-to-build-one-project-with-multiple-themes--cms-22104)


## Nested Selectors

This should feel natural. Let's go from:

```CSS
section.intro {
  max-width: 1200px;
  text-align: center;
}

section.intro > h1 {
  font-size: 32px;
  color: #000;
}

section.intro > h1:hover {
  opacity: .5;
}

section.intro > ul {
  list-style-type: none;
}

section.intro > ul li {
  padding: 10px auto;
}
```

To:

```CSS
section.intro {
  max-width: 1200px;
  text-align: center;
  & > h1 {
    font-size: 32px;
    color: #000;
    &:hover{
      opacity: .5;
    }
  }
  & > ul {
    list-style-type: none;
    li{
      padding: 10px auto;
    }
  }
}
```

## Demo: Save Colors as Variables

Let's start by demonstrating how variables are defined in an example application.
Have a look at the current styles in
[`assets/styles/index.scss`](assets/styles/index.scss).

`Best Practices: You should save important bits of style, especially colors, with a descriptive, useful name.`

## Code Along: Semantic Color Names and Theming

1. Create two files in `assets/styles/` called `theme.scss` and `colors.scss`.
2. Copy and paste all of the code from `index.scss` to `theme.scss`.

These variables' names aren't that great. First, let's create a colors module
that defines semantic names for the inscrutable hexadecimal color literals we're
using. Then, let's create a theme module that gives us a better idea of how these
colors map to styles on our page.

Finally, let's include the theme in
[`assets/styles/index.scss`](assets/styles/index.scss), which serves as our
style "manifest". Webpack will look for styles here and then let Sass follow
import statements to find all the files it needs. If we leave a module out of
this file and it isn't included inside another module, it won't affect the
styling of our page.

In general, you should only `@import` a module **once**. The manifest is usually
a good place for that.

## Lab: Typography

Typography is a complex subject, but for now, when we talk about typography,
we mean CSS rules aimed at improving the readability of your website. Such
rules include, but are not limited to:

-   `margin`
-   `width` and friends (like `max-width`)
-   `line-height`
-   `font-size`
-   `padding`

Have a look at [Better M@%4^ f$*%
Website](http://bettermotherfuckingwebsite.com/). Use your hacker skills to
figure out the CSS rules the site uses to make content more readable.

Save _**only** the rules that deal with typography_ in
[`assets/styles/typography.scss`](assets/styles/typography.scss) and be sure to
include it inside your manifest!
Challenge your self and try to incorporate variables in your code :information_desk_person:

## Lab: Use Sass Functions

Now, make use of existing color definitions and the Sass [`darken` function](https://robots.thoughtbot.com/controlling-color-with-sass-color-functions)
 to darken the `$background-color` for your quote by 10% instead of writing a
 color literal.

Also, use a [calculation](http://sass-lang.com/guide) based on default `font-size` instead of using a literal `px` unit to make your quote's font size 50% larger.

Use variables to store the results of calculations.

## Code Along: Create a Custom Function

Define the custom `tint` and `shade` functions described in the [Sass
Guidelines](http://sass-guidelin.es/#lightening-and-darkening-colors) for
manipulating color. They provide greater control than `darken` and `lighten`.

Where should we place these functions?

## Lab: Use a Custom Function

Use your custom `shade` function instead of the `darken` function.

## Lab: Sass Mixins

Mixins are one of the most used features from the whole Sass language. They are the key to reusability and DRY (“don’t repeat yourself”) components. And for good reason: mixins allow authors to define styles that can be reused throughout the stylesheet without needing to resort to non-semantic classes such as `float-left`.

[Sass Mixins](http://sass-lang.com/guide#mixins) are a great way to reduce code
duplication. Mixins can be included in rule declarations to import common rules
that are task-focused.

Our application has too much whitespace on a mobile device. Have a look at some
[example mixins](http://www.sitepoint.com/sass-mixins-kickstart-project/).
 We're going to use the last one, the
 [breakpoint mixin](http://www.sitepoint.com/sass-mixins-kickstart-project/#breakpoint-handler), to reveal our intention to change styles on mobile devices.

## Code Along: Create a Mixin

Copy the example code into a new Sass module at
[`assets/styles/breakpoint.scss`](assets/styles/breakpoint.scss). Delete the
`custom` breakpoint since it won't be useful for most projects.

_Do not_ worry about understanding this mixin code. Instead, go back to the
article that introduced the mixin and focus on understanding how the mixin is
used.

Now that we've defined the mixin, let's include it where appropriate. Where are
our readability settings defined?

The problem with including our breakpoints in our `typography` module is that we
need to ensure the breakpoints are the last rules applied. For now, create a new file [`assets/styles/breakpoints.scss`](assets/styles/breakpoints.scss) and include
it in the manifest.

## Lab: Use a Mixin

The mixin should change the style of the selected element
so that whitespace in that element is half of the default for devices smaller
than `tiny`.

1. Import your the Sass module that has your mixin.
2. Choose the selector you want to apply the mixin to.
3. Use `@include` to use your mixin.

## Best Practices

You'll notice that the Sass linter yells at you for a lot of things that might
seem silly. Follow the advice anyway. These simple rules, while annoying at
first, will lead to DRYer rules declarations and prevent accidental surprises
when developing your own custom CSS.

Best practice include, but are not limited to:

-   Do not use HTML `id` attributes to select elements for styling.
-   Always save color literals in meaningful variable names, defined as
    hexadecimal values.
-   Instead of hard-coding size units, give them a good name and use arithmetic
    to adjust as necessary.
-   Re-used calculations should be stored in a variable.
-   Sort rule declarations by property name in alphabetical order.

For more best practices, see [Sass Guidelines](http://sass-guidelin.es/), a
community-maintained list of best practices and explanations.

## Additional Resources

-   [Additional resource on organizing SASS files and folders](https://scotch.io/tutorials/aesthetic-sass-1-architecture-and-style-organization)
-   [Color-Hex - Explore Colors and Color Palattes](http://www.color-hex.com)
-   [Color Picker - Explore Colors for HTML and CSS](http://www.hexcolortool.com)
-   [Controlling color with Sass color functions](https://robots.thoughtbot.com/controlling-color-with-sass-color-functions)
-   [PXtoEM.com: PX to EM conversion made simple.](http://pxtoem.com/)
-   [Sassmeister](https://www.sassmeister.com/)
-   [Sass cheatsheet](https://devhints.io/sass)

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
