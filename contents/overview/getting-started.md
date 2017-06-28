# Getting Started

To start using hopp, you have to **install it globally** first. To
do this, simply run `npm i -g hopp`. Unlike some of the other build
tools, hopp does not need to be installed into each project
individually - it uses some hacks to get around that.

Secondly, you must **setup your build**. hopp uses the convention
over configuration style and therefore you write your code in a
file called `hoppfile.js` (place in the root of your project).
You can choose to write this file using ES2015 features or natively
supported features, it's up to you. If you choose to write it in
ES2015 (the way we do), please read the [Modernizing hoppfiles](#modernizing-hoppfiles)
section.

Your hoppfile must import the hopp task manager from the package
`hopp` (see line #1 of the sample hoppfile below). This task manager
allows you to setup your hopp tasks and preloads your plugins for you.
It is a function that can be used to define the glob of your source files
(see line #4) and then it chains to form the other methods. The task chain
must end with the destination method to define the output for your compiled
files. If your task uses bundling (i.e. concats the files into one), the path
that you provide to `.dest()` will be treated as a file (see line #10). Otherwise,
it will be treated as a folder (see line #5).

```javascript
const hopp = require('hopp')

exports.noBundling =
  hopp([ 'src/js/**/**.js' ])
    .dest('dist/js')

exports.bundling =
  hopp([ 'src/js/**/**.js' ])
    .someBundlingPlugin()
    .dest('dist/js/bundle.js')
```

The name of the export is used as the name of your task. The default task is under
'default' (`exports.default = ...`).

## git + hopp.lock

hopp generates a file called `hopp.lock` when it builds and it uses this file to store
information about its builds (in order to optimize future builds).

The rule of thumb for whether or not you should commit this file is simple:

**If you are committing your output files (compiled sources) to git, you should commit
the `hopp.lock` file.**

This is because `hopp.lock` assumes that the built source is intact since the last build.
Due to this, there's also another rule you should follow:

**NEVER MODIFY THE BUILT FILES DIRECTLY.** Use hopp to do it.

## Modernizing hoppfiles

If you want to write your hoppfiles using ES2015, you must install
babel-register local to your project. We recommend using the [env](https://npmjs.org/babel-preset-env) preset. You can add any extra presets
or plugins you'd like to your babel config. Here's a basic one that uses the
env preset:

```json
{
  "presets": [
    ["env", {
      "targets": {
        "node": "current"
      }
    }]
  ]
}
```

To instruct hopp to conduct the transpiling during a build, you can
tell hopp to preload the babel-register module before doing any of
the building. You can do this using the `-r` or `--require` flag. This
will trigger transpiling of your `hoppfile.js` so you can write in
modern code (i.e. `hopp -r babel-register`).

Here's a copy of the same hoppfile as above but written in ES2015:

```javascript
import hopp from 'hopp'

export const noBundling =
  hopp([ 'src/js/**/**.js' ])
    .dest('dist/js')

export const bundling =
  hopp([ 'src/js/**/**.js' ])
    .someBundlingPlugin()
    .dest('dist/js/bundle.js')
```