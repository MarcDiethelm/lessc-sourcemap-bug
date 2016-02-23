lessc source map bug – demo
===========================

How to reproduce

- `npm install`
  - installs `less` locally
- `npm test`
  - runs `lessc --source-map ./build/less-imports.less ./build/styles.css`
- Result: a source map is created at `./build/styles.css.map`. The paths within it are absolute.
- Expected: they should be resolved relative paths.

This is a real-world scenario that has cost me many, many hours of frustration. In my projects I use a tool called
[grunt-less-imports](https://github.com/MarcDiethelm/grunt-less-imports) to generate a file consisting of import
statements. It's superior than using concatenation or maintaining a cascade of imports by hand, because it is generated
using globbing to look for files that need to be imported.

However it turns out that if the generated file uses `../` to reach the files it is importing than the
resulting source map will be broken, i.e. containing absolute paths.

I have tried to remedy this by using the available source map options, but no cigar.