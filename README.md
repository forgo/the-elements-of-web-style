`This guide is actively being written.`
 
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
### 1) Whenever possible, write rules that are reusable.

In other aspects of our lives, rules are more useful when applied to a broader audience. In CSS, the `id` attribute is intended to be a unique value in your document. Singling out "special cases" can be useful, but good style often comes down to consistency (arguably the fundamental reason for a `class` attribute).

Here is a particularly good example of design consistency:

![visualization of the box-model](https://github.com/forgo/the-elements-of-web-style/blob/5b7bf57744e2e44f0072fce738ab220d418e7b1b/img/box-model-good.png)

[Chrome Developer Tools](https://developers.google.com/web/tools/chrome-devtools/) gives us a convenient way to visualize some of the box-model by highlighting the margin and padding of elements when hovering over rules which apply to them. Train your eye to see these spacings without visual aid. Take note of spacing consistencies across the entire page. It is clear this page and the components which compose it were well-considered ahead of time.

There's no way of knowing upon a cursory inspection that the CSS rules were optimized and minimized to produce this final display. We do know that there is opportunity, in this case, to do so without inducing refactor nightmares. 

Now imagine the layout of the page depended on haphazard shifting, bumping, and scaling of elements; moreover, imagine elements are absolutely and relatively positioned, with overlapping box-models and inadvertent duplicate `id` attributes. The final product might look just as well to the naked eye, but what if your content changed or rearranged? What if you needed to reduce the size of your static assets such as CSS files?

It's important to note content can dictate styling rules, so these rules should not be made in a vacuum. In the case of a magazine, the overall look-and-feel may not have changed over the centuries, but you can expect the length of articles, paragraphs, and headlines to be constantly changing, so your rules should be able to accomodate that variation without sacrificing the readability or aesthetics of the page.

## IV. ELEMENTARY PRINCIPLES OF LAYOUT
### 1) Optimize line length for readability.

Studies show the ideal number of characters (for readability) on a line before wrapping is somewhere between 50 and 75 characters<sup>[1](#line-length-readability)</sup>. This mostly applies to continuous, paragraph-style content.

With more terse content like , having a smaller width is not as much of a concern because "breaking the reader's" rhythym isn't as much of a concern with a blurb like a title.

On the other hand, consider if we allow the search results to be displayed in a list-format instead of a grid format. For long, winding, technical titles (which is not uncommon for data scientists to create), we might consider wrapping the title text before this supposed 75-character threshold to avoid the other concern: "the reader’s eyes will have a hard time focusing on the text."

### References
- <a name="line-length-readability">[1]</a> [Readability: the Optimal Line Length](https://baymard.com/blog/line-length-readability)
- [The Elements of Typographic Style Applied to the Web](http://webtypography.net/2.1.2)
- [Ideal line length for content](http://maxdesign.com.au/articles/em/)

## V. A FEW MATTERS OF FORM
### 1) Maintain proportionality.

Dimensional styles such as `font-size`, `padding`, `margin`, `border`, `box-shadow`, and so on within the `<body>` of the site should, ideally, resize proportionally with screen size and device orientation.

The disclaimer to be made here is a major one. Sometimes you are dealing with an existing design system or designers may -- in many cases -- be working from a mindset of fixed-pixel based dimensions. If this is the case, it can be unreasonable to shift to a paradigm of relative units (e.g. - `em`, `ex`, `vw`, `vh`, etc.).

If this common constraint is encountered, it does not negate proportionality as a measure of good form, but does make adapting to different screen sizes a more meticulous exercise and one which could factor into your maintenance costs and designs evolve over time. Think of maintaining separate components for different devices and screen types that can diverge in source and authors over time.

In a strictly pixel-based design, think of ways to write components in thematically flexible ways. For example, anticipate a "compact, "normal", and "relaxed" theme ahead of time and inject those as concrete styles in components as a matter of convention. Planning and executing this type of work may seem tedious, but this can save via the mechanism of consistency. A simple contextual switch may allow components to flow in different contexts.

In a relative-units design, relativity needs a common reference point. One very convenient way of maintaining proportions can be accomplished with a globally-applied CSS `@media` rules. These rules are a sequence of `min-width` thresholds about which the base font size and animated properties<sup>[2](#animated-properties)</sup> can be transitioned. The `min-width`s and `font-size` specified here are intended to be absolute units<sup>[3](#css-units)</sup> (e.g. - `px`).

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

As soon as I had set this aspect ratio, my coworkers immediately recognized it was the natural answer to the problem. Variations and divisions of the golden ratio can be used similarly to set dimensional styles such as `font-size`, `margin`, `padding`.

If you inspect a component style, don't be put off by non-whole `em`-based values. There can be an actual method to this madness. Take note of what some of these numbers might represent:

```
1.618em ≈ φ (the golden ratio)
0.618em ≈ 1/φ (inverse golden ratio)
0.309em ≈ 0.5/φ (half inverse golden ratio)
0.105em ≈ 0.25/φ (quarter inverse golden ratio)
```

You can imagine another set of numbers used that nest the golden ratio multiplicatively, if that satsifies you more:

```
1.618em ≈ φ (the golden ratio)
0.618em ≈ 1/φ (inverse golden ratio)
0.382em ≈ 1/φ² (inverse golden ratio squared)
0.236em ≈ 1/φ³ (inverse golden cubed)
0.146em ≈ 1/φ⁴ (inverse golden quartic)
...
```

The golden ratio itself is sometimes too much spacing to employ for certain elements, and a smaller margin or padding may be desired. This is why I often use the inverse golden ratio and derivations of it.

By themselves and strictly speaking, these values have very little meaning without the context in which they are set. Mostly, we find that they lend themselves naturally to an aesthetically pleasing layout when used properly. Most importantly, these values should be used *consistently* throughout your site.

For example, the margin between paragraphs might be `1.618em`, but this is likely too big of a spacing when in the context of a button's content padding. In this situation you could apply `0.309em`. These mappings are not set in stone, but once you find a proportion that flows with your content, being consistent with them most often yields consistently pleasing results.


## VI. STYLES AND TECHNIQUES COMMONLY MISUSED
1) Spacing is a convention, not a convenience.

The goal of computers is to make our lives easier. When it comes to user interfaces, we want to create reusable components that can naturally flow into any part of the site, without patching values and extending functionality. 

How can we accomplish this? A mistake I commonly see developers making is to place a new component into a site and then style it until it looks "good". The problem I see with this approach is that it's unnecessary and counterproductive.

Think for a moment why your component doesn't "fit" quite right when you first place it on the page. Consider the following problems and potential solutions in this situation:

| Problem | Potential Solution |
| --- | --- |
| Bad default browser spacings | CSS Resets (helpful start) |
| No universally agreed-upon convention | Convention that will prevent whack-o-mole styling |
| Dimensions do not resize dynamically with screen | Use CSS Flexbox<sup>[1](#css-flexbox)</sup> and Grid Layout<sup>[2](#css-grid)</sup> |

Flexbox and Grid Layout have some built in properties to allow some conventional spacing, but there are situations where the content in-between still needs to be handled with care. The most common situation is the general flow and spacing of headings, subheadings, and paragraphs in an article or blog. In these situations I have come up with a general convention for margin and spacing.

Remember that margin and padding may accomplish the same spacing in some contexts, applying a margin over a padding can have consequences in a site with dynamic content. For example, adding margin to a 100% window width element can lead to situations where horizontal scroll is introduced and the content extends beyond where you intend.

In contrast, padding can be thought as pushing the content of an element inward. This is a bit of an oversimplification of the box-model, but it can help guide this spacing convention. Remember, that it helps to have a CSS reset so you can assume elements default to a 0 margin and padding -- rather than having to explicitly override those values when they are not needed.

TODO: graphical example of layout + spacing convention (good vs bad)...

Depending on how complex your layout gets and how you want to handle scrolling content you may find this technique more problematic to approach. For example...

TODO: graphical example of more complex layout and explanation of how you can approach it...

### References
- <a name="css-flexbox">[1]</a> [CSS Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
- <a name="css-grid">[2]</a> [CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)

## VII. AN APPROACH TO STYLE (With a List of Reminders)

1) Some style is truly iterative, creative, and not process-oriented.

There is no one-size fits all solution for style. The goal of this guide is to help you recognize where you are making your life difficult, so you can spend more time on a truly creative process.

2) No matter the convention you employ, be _consistent_.

You can use all the fancy tricks and tools out there, but if you do not employ them consistently, your outcomes will suffer from the same inconsistency.

3) Be explicit where you can.

Where reasonable, do not rely on the automatic behavior of languages, libraries, and frameworks. The convenience of tools is negated by use cases they do not cover. If your use case falls outside the average, do not settle for average.

## VIII. AFTERWORD

If you take nothing else away from this guide, I hope to convey the value of consistency. After working on many projects in many industries, I tend to value the idea of consistency over perfection. Consistency reduces the tools and time needed to make changes you will inevitably want to make. Consistency is the work you put in, accepting what you are making will not be static. Also, this practice encourages solid understanding of the problem domain. In other words, understand what pieces will change so that you can retain the quality and effort of what should be constant.

There is balance in all things. We likely do not want a switch to turn on and off all lights in an entire house at once. In the same way, creating a common wire for all components should have the flexibility to be overriden. This can be accomplished several ways. One approach is to only use a thematic context if the component explicitly opts into it. Perhaps it is desirable to require components to opt-out to reduce boilerplate code for the 90% use-cases. It's generally more important that you stick to one of these approaches as a convention -- rather than to pontificate on which is better. Your goal is to reduce the time to iterate on and improve user experiences, not win a philosophy debate.

Classically, this can be thought of as a separation of concern. In the past, MVC was a popular way to convey this, but I like to take it a step further. Let's assume, as good developers, we have isolated our business logic completely from our visual and formatting concerns. Then it's still behooves us to optimize the "view" by creating patterns to distinguish styles which are likely to change and those which are likely constant.

This is a slightly uncomfortable elaboration as it doesn't fit neatly into conventional wisdom. You might start to see lines blurred between a business requirement and design conventions. For instance, if a users is supposed to be allowed to type more content, but designers only anticipated content of a certain length, it is your job to reconcile that difference. There may not be a right answer, and -- if there's an optimal one -- it may not be the easiest or most cost-effective. Those conversations need to be had, and the more you experience these situations, the more you will be able to quickly adapt or have a solution on hand to address it again.

## IX. GLOSSARY

## X. INDEX

