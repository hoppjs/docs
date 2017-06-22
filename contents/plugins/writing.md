# Writing your first plugin

This section will help you start writing your plugin from scratch. However, we recommend
that you clone the [hoppjs/hopp-sample-plugin](https://github.com/hoppjs/hopp-sample-plugin)
repository when you're working on your actual plugin. It contains the initial setup that you
will need to write your plugin.

**This section assumes that you have already read about hopp and know how it works.**

## So... ES5? ES2015? ES2050?

hopp maintains compatibility with node v4 but all the code should be written using the latest
stable (stage 3 & 4 features) ECMAScript features and transpiled using [babel-preset-env](https://github.com/babel/babel-preset-env).

This means that you should be writing your code using ES2015 modules (import/export) and async
functions (where applicable). If you would still like to write your plugin without any transpiling,
this guide will also cover the manual ways to handle certain things (but not all).

## Where the magic happens

The main magic of your plugin should be contained in an asynchronous function. This function will
be a callback used to transform either chunks of files or entire files (more on this in a minute).
This function must be your plugin's default export. If you are not using babel to transpile your
plugin, you may set your function to `module.exports` but this will affect the config section later.

Your function will receive two arguments, the conventional names for which are: `ctx` and `data`.

 - `ctx`: an object with information about your plugin and utilities. This object should be seen
 as an overarching config object. If you use this object to store any data, that data will be able
 to you during **every** call of your plugin.
 - `data`: an object containing the contents and metadata of the current file chunk. This object
 should be seen as a local or temporary storage because it will be destroyed once the chunk reaches
 the end of the pipeline. You can use this to modify how other plugins see this chunk but your
 plugin will never see this data again.

Since the transformation function is asynchronous, it should return a promise which must be resolved
and given the *data object*. **DO NOT RETURN JUST THE MODIFIED CONTENTS.** If you just return the
modified contents, the pipeline will fail and yell at the user. Here's an example:

**DON'T**

```javascript
export default async function (ctx, data) {
  return String(data.body)
}
```

**DO**

```javascript
export default async function (ctx, data) {
  data.body = String(data.body)
  return data
}
```

The 'DO' code from above is a good example of a plugin that just converts all incoming data into
a string.

### The `ctx` object

 - `args`: an array of the arguments passed to your plugin. These come from the hoppfile and are
 different for each task that your plugin participates in. For instance, if your plugin is called
 in the hoppfile below, the value of `args` will be `['hello', true]`.
 - `log`: a logging function that mimics `console.log()`. It prepends your logs with hopp-style
 logs that describe what task your plugin is part of and the name of your plugin.
 - `debug`: a logging function that mimics `console.log()`. The output for this is only shown when
 hopp is run with the verbose flag enabled.
 - `error`: a logging function that mimics `console.error()`. This will print output to stderr but
 will not cause hopp to fail. For hopp to stop the build, you must reject the promise or throw an
 error.

```javascript
import hopp from 'hopp'

export default
  hopp([ 'src/*.js' ])
    .plugin('hello', true)
    .dest('dist')
```

### The `data` object

 - `file` (string): the absolute path to the file this chunk is part of. To get the dirname or basename,
 please use the `path` module.
 - `dest` (string): the absolute path to the output file for this chunk. Changing this will not rename
 the destination, just break the pipeline.
 - `size` (number): the size of the file before it was read off the disk.
 - `done` (boolean): true if this data chunk is the last chunk in this file, false otherwise.
 - `body` (buffer/string): a buffer read from the file. This may come to your plugin as a string if a
 plugin before your plugin has chosen to convert it. We recommend manually coercing it into a string
 (using `.toString('utf8')`) if you would like to use it as a string.