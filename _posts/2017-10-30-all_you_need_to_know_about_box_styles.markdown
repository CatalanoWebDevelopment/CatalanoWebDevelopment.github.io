---
layout: post
title:      "All You Need to Know About Box Styles "
date:       2017-10-30 20:07:41 +0000
permalink:  all_you_need_to_know_about_box_styles
---

## (They Really Can Save You)

1. What is a "Box Model"
2. How do I use a Box Style
3. Samples of Box Styles!

### What the heck is a Box Model?!
Well, I believe it is best stated by W3Schools:
> All HTML elements can be considered as boxes. In CSS, the term "box model" is used when talking about design and layout.

That being said, it may be helpful to have an actual image in mind before we begin speaking about how to actually *style* this box. So, here we are! 

![CodeProject.com](https://www.codeproject.com/KB/HTML/567385/boxmodel-image.png)

Wow. Kind of a lot going on there! Not to worry though, everything can be broken down quite simply <3

* **Content**: The content of the box, where text and images appear,
* **Padding**: Clears an area around the content. The padding is transparent,
* **Border**  : The frame that encompasses the padding and the content,
* **Margin**  : Clears an area outside the border. The margin is transparent.

So, lets sum this up! A box model is merely the representation of elements and their associated spacial properties. In order to create space between particular elements, we can access these to do so! Keep in mind that borders, padding, and margin carry special properties when written into CSS:

* `margin: top margin, right margin, bottom margin, left margin;` (In pixels, percent, or EM)
* `padding: top padding, right padding, bottom padding, left padding;` (In pixels, percent, or EM)
* `border: line type, line width, color;` (RGB or Hexadecimal code may be used for the color! The width follows the rules of padding and margin)

### So How Do I Style These...
**Great question!** CSS (Cascading Style Sheets) offers multiple different methods to style your box model. These include, but are not limited to, the following: 

* Box shadows
* Background Colors
* Mix/Blend Mode
* Border Radius
* [And More!](https://tympanus.net/codrops/2012/10/23/basic-ready-to-use-css-styles/)

#### Let's Break it Down
**Box Shadows**
* Whats the syntax?

*Shorthand:* `box-shadow: horizontal offset, vertical offset, blur radius, base color;`

* Want an example?

```
p {
  margin: 0;
}

article {
  max-width: 500px;
  padding: 10px;
  background-color: red;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.25));
}  

.simple {
  box-shadow: 5px 5px 5px rgba(0,0,0,0.7);
}
```

* This outputs!

![Hey there](https://i.imgur.com/Tn0zaWO.png)

**Border-Radius**
* How does it work?

Border-radius is a rather interesting method to use that is still gaining cross-browser stability. Essentially, by adding an increasing amount of pixels, em, or percent, it transforms the border of an element to a circle. Using `-moz-`, `-webkit-`, and `-o-` prior to styling your `border-radius` will increase its effectiveness over many browser types (Safari, Mozilla FireFox, etc..)

* What's the syntax? (The following will make the border into a circle)

```
-webkit-border-radius: 100%;
-moz-border-radius: 100%;
-o-border-radius: 100%;
border-radius: 100%;
```

Don't forget to include `-moz-`, `-webkit-`, etc!!!

**What about the rest?**
These were included in some of the styling for reference. If you'd like more information, please visit the links which I've provide below. Happy Coding!!


### Helpful Resources
[W3Schools - Box Model](https://www.w3schools.com/css/css_boxmodel.asp) <br>
[MDN - Box Styling](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_boxes)
