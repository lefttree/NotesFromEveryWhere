# HTML Questions

## Intro

This file has all the questions I've reviewed, and some keywords for indication.

Some answers can be find here [link](http://flowerszhong.github.io/2013/11/20/html-questions.html)

## HTML

1. What does a `doctype` do?

`<!DOCTYPE>` preamble, instruction for the browser about the version of HTML.

2. What's the difference between standards mode and quirks mode?

Old browser like Navigator 4 and IE

- quirks mode
- full standards mode
- standards mode

Determined by `DOCTYPE`

- [MDN](https://developer.mozilla.org/en-US/docs/Quirks_Mode_and_Standards_Mode)

3. Difference between HTML and XHTML?

XHTML is HTML written as XML. stricter than HTML. Must be marked up correctly.

4. Are there any problems with serving pages as application/xhtml+xml?

Serviing different content/headers. cache, content-type

5. How do you serve a page with content in multiple languages?

`<html lang="en">` should be reset for each language

`lang` can be used with almost **every** HTML element.

6. What kind of things must you be wary of when design or developing for multilingual sites?

url, date, text, word length, colors

- [quora](https://www.quora.com/What-kind-of-things-one-should-be-wary-of-when-designing-or-developing-for-multilingual-sites)

7. What are `data-` attribute good for?

The `data-*` attribute is used to store custom data private to the page or application.
The stored (custom) data can then be used in the page's JavaScript to create a
more engaging user experience (without any Ajax calls or server-side database queries).

It's ignored by user agent without any visual representation.

```html
<article
    id='electriccars'
    data-columns="3"
    data-index-number="1234"
    data-parent="cars"
    >
...
</article>
```

**Access**

JavaScript

- `getAttribute()`
- `dataset` like `article.dataset.columns`

CSS

```css
article:before {
    content: attr(data-parent);
}

article[data-columns='3'] {
    width: 400px;
}
```

- Do not store content that should be visible and accessiable in data attributes
- IE 11 + support
- performance issue

8. Consider HTML5 as an open web platform. What are the building blocks of HTML5?

- more semantic text markup
- new form elements
- video and audio
- new js API
- canvas and SVG
- new communication API
- geolocation API
- web worker API
- new data storage

9. Describe the difference between `cookies`, `sessionStorage` and `localStorage`

HTML5 web storage

    - local storage
    - session storage
    - web database

    more secure and faster, data is not included with every server request

cookie

10. `<script>`, `<script async>` and `<script defer>`

- immediately
- continue to load HTML
- run the script when page finished parsing

11. Why is it generally a good idea to position CSS `<link>`s between `<head></head>`
and JS `<script>`s just before `</body>`? Do you know any exceptions?

Modern approach is to use `<script async>` to download scripts asap

[link](http://stackoverflow.com/questions/436411/where-is-the-best-place-to-put-script-tags-in-html-markup)

12. Progessive rendering

Examples:
    - lazy loading
    - prioritizing visible content

## CSS

## Javascript


