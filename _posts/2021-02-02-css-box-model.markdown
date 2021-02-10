---
layout: post
title:      "CSS: Box-Model"
date:       2021-02-02 21:41:00 +0000
permalink:  css_box_model
categories: tools
tags: css, box-model
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

Earlier this year, I got asked this question for my mock technical interview. It threw me off because I had studied up on JavaScript concepts and not CSS. I had a vague idea of what the CSS box model was, but couldn't answer it definitely. As a front-end engineer, I was told that they are exact with their measurements, down to the last pixel.

So lets get started. What is the CSS box model?

## CSS Box Model
The CSS box model is a box that wraps around every HTML element. 

From inside out, it consists of: the actual content, padding, borders, and margins.

1. Content - The content of the box, where text and images appear.
2. Padding - Transparent area around the content.
3. Border - A border that goes around the padding and content.
4. Margin - Transparent area outside the border.

So for example, if I want a div element that is 350px wide, this is how it would be done:

```
div {
  width: 320px; // 320px
  padding: 10px; // left + right = 340px 
  border: 5px solid gray; // left + right = 350px
  margin: 0;
}
```

## Box Sizing

Back in the early days of the web, most browsers interpreted the box model as described above; but Internet Explorer interpreted it differently. 

For example, if we set an element with a width of 200 pixels and a padding of 20 pixels, the total width would STILL be 200 pixels. The padding would cut into the original width, resulting in content area to be 160 pixels (200px - 20px left - 20px right).

Some would argue that Internet Explorer's approach to the box model made more sense and we can replicate it with the box-sizing property.

## Content-Box vs. Border-Box

### Content-Box

This is the default box model.

```
article {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 1px solid #000;
} // 242 pixels wide
```

### Border-Box

This is IE's interpretation of the box model.

```
article {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 1px solid #000;
} // 158 pixels wide for element
```

Personally, I would agree that the border-box property makes a lot more sense. 

Which box-sizing property do you prefer?

Cheers,
Yvonne