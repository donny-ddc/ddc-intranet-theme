---
layout: default
permalink: /
---

# Table of Contents plugin for Bootstrap

[![Build Status](https://travis-ci.org/afeld/bootstrap-toc.svg?branch=gh-pages)](https://travis-ci.org/afeld/bootstrap-toc)

This [Bootstrap](http://getbootstrap.com/) plugin allows you to generate a table of contents for any page, based on the heading elements (`<h1>`, `<h2>`, etc.). It is meant to emulate the sidebar you see on [the Bootstrap v3 documentation site](https://getbootstrap.com/docs/3.3/css/).

This page is an example of the plugin in action – the table of contents you see on the left (or top, on mobile) was automatically generated, without having to manually keep all of the navigation items in sync with the headings.

## Usage

1. Set up Bootstrap v4.
   - For Bootstrap v3, see [the older instructions](https://github.com/afeld/bootstrap-toc/blob/v0.4.1/index.md#usage).
1. Include the Bootstrap Table of Contents stylesheet and JavaScript file. [Unminified versions](https://github.com/afeld/bootstrap-toc/tree/gh-pages/dist) are also available.

   ```html
   <!-- add after bootstrap.min.css -->
   <link
     rel="stylesheet"
     href="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.css"
   />
   <!-- add after bootstrap.min.js -->
   <script src="https://cdn.rawgit.com/afeld/bootstrap-toc/v1.0.1/dist/bootstrap-toc.min.js"></script>
   ```

1. Pick one of the two options below.
1. Determine the [layout](#layout).

### Via data attributes

_Simplest._

Create a `<nav>` element with a `data-toggle="toc"` attribute.

```html
<nav id="toc" data-toggle="toc"></nav>
```

You can put this wherever on the page you like. Since this plugin leverages Bootstrap's [Scrollspy](https://getbootstrap.com/docs/4.0/components/scrollspy/) plugin, you will also need to add a couple attributes to the `<body>`:

```html
<body data-spy="scroll" data-target="#toc"></body>
```

### Via JavaScript

_If you need customization._

If you prefer to create your navigation element another way (e.g. within single-page apps), you can pass a jQuery object into `Toc.init()`.

```html
<nav id="toc"></nav>
```

```javascript
$(function() {
  var navSelector = "#toc";
  var $myNav = $(navSelector);
  Toc.init($myNav);
  $("body").scrollspy({
    target: navSelector
  });
});
```

See the [Scrollspy](https://getbootstrap.com/docs/4.0/components/scrollspy/) documentation for more information about initializing that plugin.

#### Options

When calling `Toc.init()`, you can either pass in the jQuery object for the `<nav>` element (as seen above), or an options object:

```javascript
Toc.init({
  $nav: $("#myNav")
  // ...
});
```

All options are optional, unless otherwise indicated.

| option   | type          | notes                                                                                                                                                      |
| -------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$nav`   | jQuery Object | (required) The element that the navigation will be created in.                                                                                             |
| `$scope` | jQuery Object | The element where the search for headings will be limited to, or the list of headings that will be used in the navigation. Defaults to `$(document.body)`. |

{: .table }

## Customization

The following options can be specified at the heading level via `data-toc-*` attributes.

### Displayed text

By default, Bootstrap TOC will use the text from the heading element in the table of contents. If you want to customize what is displayed, add a `data-toc-text` attribute with the desired text. For example:

```html
<h2 data-toc-text="Short text">Longer text</h2>
```

displays "Longer text" as the heading, but "Short text" in the sidebar.

### Skipping

To prevent a particular heading from being added to the table of contents, add a `data-toc-skip` [boolean attribute](https://www.w3.org/TR/2008/WD-html5-20080610/semantics.html#boolean).

```html
<h2 data-toc-skip>Some heading you don't want in the nav</h2>
```

## Layout

This plugin isn't opinionated about where it should be placed on the page, but a common use case is to have the table of contents created as a ["sticky"](https://getbootstrap.com/docs/4.0/utilities/position/#sticky-top) sidebar.

```html
<body data-spy="scroll" data-target="#toc">
  <div class="container">
    <div class="row">
      <!-- sidebar, which will move to the top on a small screen -->
      <div class="col-sm-3">
        <nav id="toc" data-toggle="toc" class="sticky-top"></nav>
      </div>
      <!-- main content area -->
      <div class="col-sm-9">...</div>
    </div>
  </div>
</body>
```

You may also want to include this in your stylesheet:

```css
{% include layout.css %}
```

_Note: if you're upgrading from version <= 0.4.1 to 1.0.0+, these have changed._

## Examples

- [Advanced JS course syllabus](https://advanced-js.github.io/syllabus/)
- [aws-http](https://rishikeshdarandale.github.io/aws-http/)
- [OpenStreetMap Carto Tutorials](https://ircama.github.io/osm-carto-tutorials/tile-server-ubuntu/)

## See also

- [Adding links to all headings on your page](http://bryanbraun.github.io/anchorjs/)
- [Contributor information](https://github.com/afeld/bootstrap-toc/blob/gh-pages/CONTRIBUTING.md)
- [Updating the URL hash based on scroll](https://gist.github.com/iamravenous/4a1545dc3ccd24abf89e)

This plugin was heavily inspired by:

- [Bootstrap Docs Sidebar example](https://jsfiddle.net/gableroux/S2SMK/)
- [Tocify plugin](http://gregfranko.com/jquery.tocify.js/)
- [TOC plugin](http://projects.jga.me/toc/)
