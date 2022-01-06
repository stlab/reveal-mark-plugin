# Reveal.js / Mark.js plugin

This is a fork of a part of Reveal.js' own "highlight" plugin, which supports
animated marking (emphasizing) of specific code regions by line or line range.

This plugin additionally supports marking:

- In non-code content
- By matched regexp
- Across HTML elements

The latter is particularly important if you are trying to mark regions in code
that already has HTML syntax highlighting, e.g. inserted by a preprocessor like
[Jekyll](https://jekyllrb.com).

## Usage

Just as marking with reveal's plugin is controlled by attaching a
`data-highlight` attribute to the thing to be emphasized, this plugin uses a
`data-mark` attribute, with a compatible (superset) syntax.  Marking steps are
separated by vertical bars, and can target zero or more comma-separated regions,
each of which can be a line number or a line range, e.g.

```html
<pre data-mark="1,3|2,5-7|4"><code>
   ...
</code><pre>
```

In this example, lines 1 and 3 start out marked, after the first animation step
lines 2, 5, 6 and 7 are marked, and after the second animation step only line 4
is marked.

In this plugin, regions can also be specified as JavaScript regular expressions
delimited by an arbitrary non-`|`, non-digit. The first match for the regular
expression is marked, e.g.

```html
<blockquote data-mark="|/creative/,#design#|4">
   ...
</blockquote>
```

This example starts out with no marks, then the first occurrences of “creative”
and “design” in the `<blockquote>` are marked, then line 4 of the `<blockquote>`
is marked.

## Syntax

Arbitrary whitespace is allowed at the beginning and end of the `data-mark`
string, and around step delimiters (`|`), region delimiters (`,`) and line range
delimiters (`-`).  

To include a regexp delimiter in a regexp literally, you can
escape it with a backslash, but you may be better off choosing a different
regexp delimiter.

The final delimiter of a regexp can be followed by an arbitrary string composed
of the characters `dgimsuy`, indicating the [standard JS regexp
flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#advanced_searching_with_flags).
