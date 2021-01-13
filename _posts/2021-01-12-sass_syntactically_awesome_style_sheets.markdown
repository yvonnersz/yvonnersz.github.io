---
layout: post
title:      "Sass: Syntactically Awesome Style Sheets"
date:       2021-01-12 21:41:00 +0000
permalink:  sass_syntactically_awesome_style_sheets
categories: tools
tags: sass, scss
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

## Sass Basics

As I begin my job search, there is one phrase that repeatedly comes up: Experience in Sass. So what is Sass exactly?

> Sass is the most mature, stable, and powerful professional grade CSS extension language in the world.

Okay, great! So Sass is a CSS extension language. But why would anyone use Sass over CSS? With my limited experience in programming, I didn't know that CSS had any upper boundaries. So is it even necessary to learn Sass or is it just an outdated technology, like jQuery? After some digging around, it seems like Sass is still widely popular and many would prefer to use Sass over working with CSS files.

> Sass lets you use features that don't exist in CSS yet like variables, nesting, mixins, inheritance and other nifty goodies that make writing CSS fun again.

Essentially, Sass would allow for styles to be easily reusable, which not only saves time and tedious typing, but also reinforces the DRY principle. CSS, by itself, has a habit of being repetitious. Being able to use variables reduces repetition in CSS and can allow for easy theme switching.

For example, repeating color values in the .css file is a chore and could potentially introduce errors if it's a large enough project. With Sass, however, one could do the following so that the web layout stays consistent:

```
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## SCSS vs SASS Syntax

According to documentation, Sass supports two difference syntaxes: SCSS and SASS. Each one can load the other, so it's up to the developer to decide which one to choose.

### SCSS (.scss)
- SCSS is a superset of CSS, which means that all valid CSS is valid SCSS.
- Because it's similar to CSS, it's the easiest syntax to get used to and the most popular.

```
@mixin button-base() {
  @include typography(button);
  @include ripple-surface;
  @include ripple-radius-bounded;

  display: inline-flex;
  position: relative;
  height: $button-height;
  border: none;
  vertical-align: middle;

  &:hover { cursor: pointer; }

  &:disabled {
    color: $mdc-button-disabled-ink-color;
    cursor: default;
    pointer-events: none;
  }
}
```

### SASS (.sass)
- Also known as the indented syntax. The indented syntax was Sass’s original syntax. 
- Supports all the same features as SCSS.

```
@mixin button-base()
  @include typography(button)
  @include ripple-surface
  @include ripple-radius-bounded

  display: inline-flex
  position: relative
  height: $button-height
  border: none
  vertical-align: middle

  &:hover
    cursor: pointer

  &:disabled
    color: $mdc-button-disabled-ink-color
    cursor: default
    pointer-events: none
```

Notes:
- Curly braces can be replaced by an indent one level deeper.
- Anytime a line ends, that counts as a semi-colon.

## How to Get Started

To start using Sass, one can just simply install it by following the instructions found on the official website:

> https://sass-lang.com/install

Cheers,
Yvonne
