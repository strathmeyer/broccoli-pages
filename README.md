# Broccoli Pages Filter

Allows you to generate HTML from Markdown and HTML fragments. You can specify metadata for each page.
In metadata, you can specify a Handlebars template to be used to wrap this content.

## Example Page
```markdown
---
title: Hello World
description: some text
template: default.hbs
---
**Beautiful World**
```

## Usage

```javascript
var MarkdownPages = require('broccoli-pages').MarkdownPages;
var HTMLPages = require('broccoli-pages').HTMLPages;
var HBSPages = require('broccoli-pages').HBSPages;
var pickFiles = require('broccoli-static-compiler');

var options = {
  templates: './templates',
  helpers: './helpers',
  partials: './templates/partials',
  globals: {
    message: "Hello World!",
    team: [ 'Bob', 'Joe', 'Mary' ]
  }
};

var content = pickFiles('content', {
  srcDir: '/',
  files: ['**/*.*'],
  destDir: '/'
});

var html;

html = HTMLPages(content, options);
html = MarkdownPages(html, options);
html = HBSPages(html, options);

module.exports = html;
```

You can see an example [Brocfile.js](example/Brocfile.js) and [example](example) directory.
