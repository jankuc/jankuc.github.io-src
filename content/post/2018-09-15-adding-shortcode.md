---
title: Adding mermaid shortcode to hugo theme
subtitle:
tags: ["example", "diagram", "mermaid"]
date: 2018-09-15
---

Hugo supports shortcodes, which according to [documentation](https://gohugo.io/content-management/shortcodes/) are

>simple snippets inside your content files calling built-in or custom templates.

There are buit-ins like visualization of an instagram post, or youtube video. But there is a place for custom ones as described thoroughy [here](https://gohugo.io/templates/shortcode-templates/).

<!--more-->

This post will describe a process to add a mermaid shortcode for visualization flowchart, sequence, or GANTT diagrams. The mermaid project's home page is at [mermaidjs.github.io](https://mermaidjs.github.io/) with some examples.

With the shortcode, we will need to add the `mermaid.js` code that renders the diagrams from the source markdown, some `.css` and the shortcode definition. The sources are based on mermaid support in [Learn Theme](https://themes.gohugo.io/hugo-theme-learn/) with modifications from [docdock theme](https://github.com/vjeantet/hugo-theme-docdock).

## Sources

First the shortcode styles will be added to the `static/css/mermaid.css` and the code that generates them into `static/js/mermaid.js`. We will need these files in the shortcode definition

## Shortcode definition

The definition is added as an html file into the `theme` directory under `layouts/shortcodes/` and the filename defines the shortcode, so it'll be `mermaid.html`. In the file we will link to the `css` and `js` file added earlier and define an `align` parameter to have control over it's alignment on the page. The source looks as follows: 

```html
<link href="{{"css/mermaid.css" | relURL}}" type="text/css" rel="stylesheet"/>
<script defer src="{{"js/mermaid.js" | relURL}}">
    mermaid.initialize({startOnLoad:true});
</script>
<div class="mermaid" align="{{ if .Get "align" }}{{ .Get "align" }}{{ else }}center{{ end }}" >
    {{ safeHTML .Inner  }}
</div>
```

The third line runs the `mermaid.js`'s `initialize()` function on the `mermaid` shortcode content.
