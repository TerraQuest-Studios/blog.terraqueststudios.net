---
title: "Native CSS Mixins?"
summary: Implementing CSS mixins like in native CSS
date: 2025-02-08
author: ["wsor4035"]
cover:
    image: green-leafed-trees-under-night-sky.jpg
    hiddenInList: true
    caption: by Paul Pastourmatzis - [Source](https://unsplash.com/photos/green-leafed-trees-under-night-sky-5jSRM-M1z2Y)
---

## CSS Mixins, What are they?

Quick summary, CSS `mixins` (and `includes`) are a concept that comes from [SASS](https://sass-lang.com/). It allows you to deduplicate CSS, 
essentianlly making your own functions that you can call when you are styling classes. An example of a mixin is as follows:

```scss
@mixin my-mixin {
    color: white;
    background-color: grey;
    padding: 1rem;
    margin: 0;
    border: 4px solid pink;
}
```
\
Now to use that mixin, you would have to use have to `include` it in a class declaration such as:

```scss
/* sole purpose of selector */
h1 {
    @include my-mixin;
}

/* with other css properties */
h5 {
    @include my-mixin;
    text-decoration: underline;
    text-underline-offset: 0.5rem;
    text-transform: capitalize;
}
```
\
Once compiled by SASS you would have an output (comments for demonstrative purposes) that looks something like:

```css
h1 {
    /* start: from CSS mixin */
    color: white;
    background-color: grey;
    padding: 1rem;
    margin: 0;
    border: 4px solid pink;
    /* end: from CSS mixin */
}

h5 {
    /* start: from CSS mixin */
    color: white;
    background-color: grey;
    padding: 1rem;
    margin: 0;
    border: 4px solid pink;
    /* end: from CSS mixin */
    text-decoration: underline;
    text-underline-offset: 0.5rem;
    text-transform: capitalize;
}
```

## Great, So how do I use these natively?

Glad you asked, the TLDR is by abusing CSS [`animations`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation) and [`keyframes`](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes). So to follow our example from above, lets first 
declare our mixin:

```css
@keyframes my-mixin {
    from {
        color: white;
        background-color: grey;
        padding: 1rem;
        margin: 0;
        border: 4px solid pink;
    }
}
```
\
Looks like a standard CSS `keyframe` right? you would be correct. The "magic" comes in when you go to use the css keyframe:

```css
/* sole purpose of selector */
h1 {
    animation: 1s paused my-mixin;
}

/* with other css properties */
h5 {
    animation: 1s paused my-mixin;
    text-decoration: underline;
    text-underline-offset: 0.5rem;
    text-transform: capitalize;
}
```
\
As you can see, we are simply calling the `keyframe` using a placeholder time, in our case `1s`, not that it matters much. The real magic 
comes from the fact that we have `paused` for our `<single-animation-play-state>` parameter. You may be thinking at this point, this is all 
fine and dandy, but it uses CSS `animations`, [can't those be performance expensive?](https://developer.mozilla.org/en-US/docs/Web/Performance/Animation_performance_and_frame_rate)
Well, I cant exactly say as I didn't personally test it, but since the animation is paused, rather than truely running, its probably fine. 
For more information, have a read of [this article](https://css-tricks.com/how-to-play-and-pause-css-animations-with-css-custom-properties/) 
by Mads Stoumann over on CSS-Tricks.

## The Future
i'll be the first to admit that the whole implementation is a giant "hack" and I complemently would not blame you for not wanting to
use it :). We ["recently"](https://caniuse.com/css-nesting) [^1] got [CSS nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting) 
in across browsers which traditionally was a SASS feature, so how about mixins? Well the good news is that the CSS Working Group has an issue for it, 
[w3c/csswg-drafts#9350](https://github.com/w3c/csswg-drafts/issues/9350) and has [resolved to adopt it](https://github.com/w3c/csswg-drafts/issues/9350#issuecomment-1939628591).
For further reading I would recommend taking a peak at [this article](https://css.oddbird.net/sasslike/mixins-functions/) over on oddbird.net to get a good summary.

[^1]: I say recently, due to policy of how long you want to support older browsers. A big sticking point being IOS Safari's antiquated way of shipping updates 
    tied to IOS version updates. This also further cause problems due to Chrome, Firefox, etc essentially being skins over the top of Safari on IOS due to Apple
    restrictions.