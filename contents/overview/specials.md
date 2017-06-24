# More on tasks

There's a few different types of tasks and different
ways to define them. Here they are.

## Parallel tasks

There are two types of parallel tasks in hopp:

  1. The default type is asynchronous tasks. This is similar to
  fly's coroutines. It will simply spin off the different tasks
  in their own promises and wait for all of them to resolve.
  2. Truly concurrent tasks. These are actually run on separate
  node clusters (i.e. separate node processes). These must be
  manually enabled via the CLI and cannot be put into the build
  file (use it properly, it will slow down smaller builds, it's
  made for larger builds).

To define a parallel task, use the `hopp.parallel` method in your
build file and pass an array of task names that must be run in
parallel.

Sample hoppfile.js:

```javascript
// more code is needed, it's been omitted

export default hopp.parallel([
  'js',
  'css'
])
```

## Stepped tasks

These tasks are very similar to parallel tasks except they
are ordered and therefore one must end before another begins.

Instead of using the `.parallel()` method, you should use the
`.steps` method:

```javascript
// more code is needed, it's been omitted

export default hopp.steps([
  'js',
  'css'
])
```

## Watch tasks

hopp does not support a watch mode in the way that you would
expect (sorry). Instead of watching a glob of files and then
triggering a task when those files change, in hopp, you would
watch a task. The task is responsible for defining the proper
globs that need to be watched.

The API is the same as that for parallel and steps:

```javascript
// more code is needed, it's been omitted

export default hopp.watch([
  'js',
  'css'
])
```