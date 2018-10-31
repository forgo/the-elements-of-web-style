# The Elements of Web Style
Universal techniques to improve and enhance any web UI.

## I. INTRODUCTORY
This guide is based on the author's personal experience in web design from 2005 to now. The rules I lay out are my opinions formed partly from experience in corporate, academic, government, and contractual contexts. 

My personal projects, from the days of futzing with custom CSS on a MySpace profile (R.I.P) to the concepts I implemented the "right way" (the cathartic solution to bad management), also inform this guide.

Primarily I'd like to convey, contrary to popular belief, process _can_ yield aesthetically pleasing results alongside functional results. Furthermore, that process does not have to be complex. When it comes to style, there are a lot of good heuristics floating around the web and in my head. Here's what I'd like to do with those:

- consolidate coherent and consumable rules into applicable scenarios
- differentiate conflicting good ideas by constraining or expanding them
- give concrete, demonstrable code examples

## II. CREDITS
I've taken cues from many sources over the years, many of them littered over the internet in the form of developer blog posts, question and answer forums, and good ol' comment sections. In retrospect, there's no way I could cite all the inspirations for my ideas, but I will try to give credit where credit is due throughout this guide.

I would be remiss to not give some high-level shoutouts:

- [Eric Meyer](https://meyerweb.com/ui/about.html)
  - This dude has helped shape web style since before I learned what CSS was.
- [stackoverflow.com](https://stackoverflow.com/)
  - An invaluable resource of countless developers from time immemorial (actually 2008, but you know)
- [The Elements of Style](http://www.jlakes.org/ch/web/The-elements-of-style.pdf)
  - A classic English reference book, the format of which I flippantly borrow. 

## III. ELEMENTARY RULES OF CSS

## IV. ELEMENTARY PRINCIPLES OF LAYOUT
### 1) Optimize line length for readability.

Studies show the ideal number of characters (for readability) on a line before wrapping is somewhere between 50 and 75 characters<sup>[1](#line-length-readability)</sup>. This mostly applies to continuous, paragraph-style content.

With more terse content (e.g. - ), having a smaller width is not as much of a concern because "breaking the reader's" rhythym isn't as much of a concern with a blurb like a title.

On the other hand, consider if we allow the search results to be displayed in a list-format instead of a grid format. For long, winding, technical titles (which is not uncommon for data scientists to create), we might consider wrapping the title text before this supposed 75-character threshold to avoid the other concern: "the reader’s eyes will have a hard time focusing on the text."

### References
- <a name="line-length-readability">[1]</a> [Readability: the Optimal Line Length](https://baymard.com/blog/line-length-readability)
- [The Elements of Typographic Style Applied to the Web](http://webtypography.net/2.1.2)
- [Ideal line length for content](http://maxdesign.com.au/articles/em/)

## V. A FEW MATTERS OF FORM
### 1) Maintain proportionality.

Dimensional styles such as `font-size`, `padding`, `margin`, `border`, `box-shadow`, and so on within the `<body>` of the site should resize proportionally with screen size and device orienation.

Maintaining these proportions can be accomplished with a globally-applied CSS `@media` rules. These rules are a sequence of `min-width` thresholds about which the base font size and animated properties<sup>[2](#animated-properties)</sup> can be transitioned. The `min-width`s and `font-size` specified here are intended to be absolute units<sup>[3](#css-units)</sup> (e.g. - `px`).

The `font-size`s and thresholds are up to the designer and may be different for different content and font types. The `font-size`s are easily tweaked after the fact to produce optimal proportion. In theory, more thresholds account for more use cases.

In practice, we can leverage the fact that most devices have common resolutions<sup>[4](#screen-resolutions)</sup> in `px` units, so common factors among screen resolutions should suffice. Keep in mind `font-size` may not need to jump whole pixel values between adjacent thresholds. If so, these threshold boundaries can be collapsed.

### Example
```css
@media (min-width: 160px) {
  body {
    font-size: 11px;
    transition: all 0.2s ease-out;
  }
}

@media (min-width: 320px) {
  body {
    font-size: 12px;
    transition: all 0.2s ease-out;
  }
}

@media (min-width: 480px) {
  body {
    font-size: 13px;
    transition: all 0.2s ease-out;
  }
}

@media (min-width: 640px) {
  body {
    font-size: 14px;
    transition: all 0.2s ease-out;
  }
}

@media (min-width: 800px) {
  body {
    font-size: 15px;
    transition: all 0.2s ease-out;
  }
}

@media (min-width: 960px) {
  body {
    font-size: 16px;
    transition: all 0.2s ease-out;
  }
}
```

Subsequent dimensional styles should be set in relative units (e.g. - `em`) to maintain proportion at the different thresholds. You can think of the above `font-size`s as what represents `1em` on differently sized screens and windows.

With `padding: '2em'` when the device width is between `160-320px`, the fixed-pixel equivalent would be:

`2 * (1em) = 2 * (11px) = 22px`

However, when the device width is between `320-480px`, the fixed-pixel equivalent would be:

`2 * (1em) = 2 * (12px) = 24px`

Therefore, when the screen increases past a `320px` width threshold, the padding you had set to a constant `2em` would effectively animate from `22px` to `24px`. The benefit here is that the units are relative to our base `font-size`s set in the corresponding `@media` query. When the screen size is changing due to the user expanding a window or rotating a mobile-device, the transition provides an additional benefit of animating what it can for a more seamless visual effect.

This maintains consistent proportion and prevents having to refactor hard-coded pixel units whenever you change the layout or other styles.

Imagine the spacing between the text of one paragraph to the next, and the spacing between the border of a button and the text inside of it.

The `font-size` of an element will default to `1em`, so it will inherit the definition of `1em` from the `px`-based `font-size` above it -- unless that `font-size` is explicitly overwritten in a parent of the element. Setting an absolute `font-size` unit outside of the `@media` CSS queries should be generally avoided.

### References
- <a name="animated-properties">[1]</a> [CSS Animated Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)
- <a name="css-units">[2]</a> [CSS Units](https://www.w3schools.com/cssref/css_units.asp)
- <a name="screen-resolutions">[3]</a> [Screen Resolution Statistics](https://www.rapidtables.com/web/dev/screen-resolution-statistics.html)

### 2) Employ the golden ratio.

When using relative dimensions, use time-tested universal constants and mathematical concepts. I once found myself in a situation with coworkers, tweaking the dimensions of a rectangular component on our site. Nobody was satisfied with outcome of the guess-and-check method being employed. So, I decided to utilize some math. The golden ratio (phi: φ ≈ 1.618), has long been known to produce aesthetically pleasing proportions in architecture and also occurs in nature.

If the width `w` of an element is fixed, I can easily calculate the height `h` to maintain an aspect ratio `AR` equal to the golden ratio `φ`.

### Example
```
h = ?
w = 12em
AR = w/h = φ
h = w/φ ≈ 12em/1.618 ≈ 7.416em
```


## VI. STYLES AND TECHNIQUES COMMONLY MISUSED

## VII. AN APPROACH TO STYLE (With a List of Reminders)

## VIII. AFTERWORD

## IX. GLOSSARY

## X. INDEX

