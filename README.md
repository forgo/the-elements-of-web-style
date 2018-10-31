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
1) Optimize line length for readability.

Studies show the ideal number of characters (for readability) on a line before wrapping is somewhere between 50 and 75 characters<sup>[1](#line-length-readability)</sup>. This mostly applies to continuous, paragraph-style content.

With more terse content (e.g. - ), having a smaller width is not as much of a concern because "breaking the reader's" rhythym isn't as much of a concern with a blurb like a title.

On the other hand, consider if we allow the search results to be displayed in a list-format instead of a grid format. For long, winding, technical titles (which is not uncommon for data scientists to create), we might consider wrapping the title text before this supposed 75-character threshold to avoid the other concern: "the reader’s eyes will have a hard time focusing on the text."

### References
- <a name="line-length-readability">[1]</a> [Readability: the Optimal Line Length](https://baymard.com/blog/line-length-readability)
- [The Elements of Typographic Style Applied to the Web](http://webtypography.net/2.1.2)
- [Ideal line length for content](http://maxdesign.com.au/articles/em/)

## V. A FEW MATTERS OF FORM
1) Maintain proportionality.

Dimensional styles such as `font-size`, `padding`, `margin`, `border`, `box-shadow`, and so on within the `<body>` of the site should resize proportionally with screen size and device orienation.

Maintaining these proportions can be accomplished with a globally-applied CSS `@media` rules. These rules are a sequence of `min-width` thresholds about which the base font size any animated properties<sup>[2](#animated-properties)</sup> can be transitioned. The `min-width`s and `font-size` specified here are intended by be absolute units<sup>[3](#css-units)</sup> (e.g. - `px`). Subsequent dimensional styles set in the application use relative units (e.g. - `em`) to maintain proportion relative to the absolute font-size set at the different thresholds.

The `font-size`s and thresholds are up to the designer and may be different for different content and font types. The `font-size`s are easily tweaked after the fact to produce optimal proportion. In theory, more thresholds account for more use cases. In practice, we can leverage the fact that most devices have common resolutions<sup>[4](#screen-resolutions)</sup> in `px` units, so common factors among screen resolutions should suffice. 


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

You can think of these font sizes as what represents '1em' in subsequent styles on the page. We attempt to make all our component inline-styles 'em'-based so that our content looks natural and proportional for as many screen sizes as possible. This is also especially important for dimensional styles such as padding, margin, offsets, borders, shadows, etc...

For example:

With `padding: '2em'` when the device min-width is between 160px and 320px, the fixed pixel equivalent would be:

`2 * (11px) = 22px`

However, when the device min-width is between 320px and 480px, the fixed-pixel equivalent would be:

`2 * (12px) = 24px`

Therefore, when the screen increases past a 320px width threshold, the padding you had set to a constant '2em' would effectively animate from '22px' to '24px'. The benefit here is that the units are relative to our base font-size. This gives proportionality and generally prevents having to refactor hard-coded pixel units that are inherently relative to other dimensions in your site. Think aspect ratios, the spacing between the text of one paragraph to the next, and the buffer between the border of a button and the text or image inside of it.

Let's say you started with a paragraph font-size of '10px' and had set the margin or padding between paragraphs to always be '16px'. This might look aesthetic to start with

Typically, without explicitly styling otherwise or being determined by a parent element's style, the text of an element will default to '1em', so setting an explicit font-size is generally avoided unless the element actually calls for it, and it should still be 'em' based.


### References
- <a name="animated-properties">[1]</a> [CSS Aniamted Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)
- <a name="css-units">[2]</a> [CSS Units](https://www.w3schools.com/cssref/css_units.asp)
- <a name="screen-resolutions">[3]</a> [Screen Resolution Statistics](https://www.rapidtables.com/web/dev/screen-resolution-statistics.html)

## VI. STYLES AND TECHNIQUES COMMONLY MISUSED

## VII. AN APPROACH TO STYLE (With a List of Reminders)

## VIII. AFTERWORD

## IX. GLOSSARY

## X. INDEX

