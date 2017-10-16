# webtreemap

> **New 2017-Oct-16**: master is now webtreemap v2, a complete rewrite with
bug fixes, more features, and a different (simpler) API.  If you're looking
for the old webtreemap, see the [v1] branch.

[v1]: https://github.com/evmar/webtreemap/tree/v1

A simple treemap implementation using web technologies (DOM nodes, CSS styling
and transitions) rather than a big canvas/svg/plugin.  It's usable as a library
as part of a larger web app, but it also includes a command-line app that dumps
a self-contained HTML file that displays a map.

Play with a [demo].

[demo]: http://evmar.github.io/webtreemap/demo.html

## Usage

### Web

The data format is a tree of `Node`, where each node is an object in the shape
described at the top of [tree.ts].

[tree.ts]: https://github.com/evmar/webtreemap/blob/master/tree.ts

```html
<script src='webtreemap.js'></script>
<script>
// Container must have its own width/height.
const container = document.getElementById('myContainer');
// See typings for full API definition.
webtreemap.render(container, data, options);
```

### Command line

```sh
$ webtreemap -o output_file < my_data
```

Command line data format is space-separated lines of "size path", where size is
a number and path is a '/'-delimited path.  This is exactly the output produced
by du, so this works:

```sh
$ du -ab some_path | webtreemap -o out.html
```

But note that there's nothing file-system-specific about the data format -- it
just uses slash as a nesting delimiter.

## Demo

### US Population

The US population data comes from the US census.

http://www.census.gov/popest/data/counties/totals/2015/CO-EST2015-01.html

The CSV from there was postprocessed by `demo/census.py` .

## Development

Use `npm run dev` to bring up file watchers that keep the demo JS bundle up
to date.  Then load `demo/demo.html` in a browser.

### Command line app

Use `tsc -w` to keep the npm-compatible JS up to date, then run e.g.:

```
$ du -ab node_modules/ | node build/cli.js --title 'node_modules usage' -o demo.html
```
