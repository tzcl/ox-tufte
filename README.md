# ox-tufte

ox-tufte is an export backend for Org mode that exports buffers to HTML that is compatible with [Tufte CSS](https://edwardtufte.github.io/tufte-css/) out of the box (i.e., you don't need to make any CSS modifications).

The goal behind ox-tufte is to be able to generate Tufte-CSS-compatible HTML while preserving the Org mode editing experience. It is sometimes best to use [inline HTML](https://orgmode.org/manual/Quoting-HTML-tags.html) to get the output the way you want but in general ox-tufte makes life easier.

Note, this repo doesn't contain the Tufte CSS files. You can download them separately [here](https://github.com/edwardtufte/tufte-css).

## Features

The following Org elements are mapped to Tufte CSS features:

| Org element                 | Tufte CSS feature                  |
| --------------------------- | ---------------------------------- |
| Center block                | Indented quotation                 |
| Footnote                    | Side note (numbered)               |
| Links with the prefix `mn:` | Margin notes (not numbered)        |
| Quote block                 | Epigraph (italicised quote)        |
| Verse block                 | Epigraph with whitespace preserved |
| Source block                | Code block                         |

The only elements that really disrupts the flow of your document in Org mode are `mn` links. I've used inline HTML but using [macros](https://orgmode.org/manual/Macro-Replacement.html) might be a better solution.

## How it works

ox-tufte is derived from the Org mode HTML exporter with modifications to make the resulting HTML compatible with Tufte CSS. The overwritten functions are

| Original function           | ox-tufte function                | Why?                                           |
| ---------------------- | ----------------- | ---- |
| org-html-center-block       | org-tufte-center-block           | Make center blocks produce indented quotations |
| org-html-footnote-reference | org-tufte-footnote-reference     | Make footnotes produce sidenotes               |
| org-html-headline           | org-tufte-headline               | Avoid wrapping heading tags in divs            |
| org-html-link               | org-tufte-maybe-margin-note-link | See if a link is a margin note                 |
| org-html-quote-block        | org-tufte-quote-block            | Make quote blocks produce epigraphs            |
| org-html-section            | org-tufte-section                | Avoid wrapping paragraphs in divs              |
| org-html-src-block          | org-tufte-src-block              | Wrap code blocks with pre tags for formatting  |
| org-html-verse-block        | org-tufte-verse-block            | Make verse blocks produce epigraphs            |

## Example

See `example.org` for my recreation of the [Tufte CSS overview page](https://edwardtufte.github.io/tufte-css/).
