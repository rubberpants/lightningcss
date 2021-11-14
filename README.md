# parcel-css

A WIP CSS parser, transformer, and minifier written in Rust.

## Features

- **Extremely fast** – Parsing and minifying large files is completed in milliseconds, often with significantly smaller output than other tools. See benchmarks below.
- **Typed property values** – many other CSS parsers treat property values as an untyped series of tokens. This means that each transformer that wants to do something with these values must interpret them itself, leading to duplicate work and inconsistencies. `parcel-css` parses all values using the grammar from the CSS specification, and exposes a specific value type for each property.
- **Minification** – One of the main purposes of `parcel-css` is to minify CSS to make it smaller. This includes many optimizations including:
  - Combining longhand properties into shorthands where possible.
  - Merging adjacent rules with the same selectors or declarations.
  - Combining CSS transforms into a single matrix or visa versa when smaller.
  - Removing vendor prefixes that are not needed, based on the provided browser targets.
  - Reducing `calc()` expressions where possible.
  - Converting colors to shorter hex notation where possible.
  - Minifying gradients.
  - Normalizing property value order.
  - Removing default property sub-values which will be inferred by browsers.
  - Many micro-optimizations, e.g. converting to shorter units, removing unnecessary quotation marks, etc.
- **Vendor prefixing** – `parcel-css` accepts a list of browser targets, and automatically adds (and removes) vendor prefixes.
- **CSS modules** – TODO

## Benchmarks

```
$ node bench.js bootstrap-4.css 
cssnano: 557.216ms
159636 bytes

esbuild: 17.79ms
160332 bytes

parcel-css: 5.231ms
144293 bytes


$ node bench.js animate.css
cssnano: 279.961ms
71723 bytes

esbuild: 11.781ms
72183 bytes

parcel-css: 2.029ms
23707 bytes


$ node bench.js tailwind.css 
cssnano: 2.193s
1925626 bytes

esbuild: 106.392ms
1961642 bytes

parcel-css: 43.564ms
1906588 bytes
```
