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

Studies show the ideal number of characters (for readability) on a line before wrapping is somewhere between 50 and 75 characters<sup>[1](#myfootnote1)</sup>. Of course, this is mostly applicable to continuous, paragraph style content. In the case of our 25em-wide search result card, having a smaller width is not as much of a concern because "breaking the reader's" rhythym isn't as much of a concern with a blurb like a title.

On the other hand, consider if we allow the search results to be displayed in a list-format instead of a grid format. For long, winding, technical titles (which is not uncommon for data scientists to create), we might consider wrapping the title text before this supposed 75-character threshold to avoid the other concern: "the reader’s eyes will have a hard time focusing on the text."

### References
- [Readability: the Optimal Line Length](https://baymard.com/blog/line-length-readability)
- [The Elements of Typographic Style Applied to the Web](http://webtypography.net/2.1.2)
- [Ideal line length for content](http://maxdesign.com.au/articles/em/)
<a name="myfootnote1">1</a>: Footnote content goes here

## V. A FEW MATTERS OF FORM
1) Maintain proportionality.



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

### References
- []()

## VI. STYLES AND TECHNIQUES COMMONLY MISUSED

## VII. AN APPROACH TO STYLE (With a List of Reminders)

## VIII. AFTERWORD

## IX. GLOSSARY

## X. INDEX

