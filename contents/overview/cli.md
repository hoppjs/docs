# The CLI

This is the documentation to help you out with using the
hopp CLI tool.

The hopp tool's help message looks something like this:

```
usage: hopp [OPTIONS] [TASKS]

  -d, --directory  set path to project directory
  -r, --require    require a module before doing anything
  -R, --recache    force cache busting
  -j, --jobs       set number of jobs to use for parallel tasks
  -v, --verbose    enable debug messages
  -V, --version    get version info
  -h, --help       display this message
```

## `-d, --directory`

This sets the path to the project directory. All files are considered
to be relative to this location and the location must contain the 
hoppfile.js, hopp.lock, input & output folders. Really just everything.
It's basically a shortcut for `cd $dir && hopp && cd ..`.

## `-r, --require`

This flag is similar to node's own `--require` flag. It allows you to
instruct hopp to preload some module before doing anything else. This is
useful for loading any register hooks such as `babel-register` or
`coffee-script/register` (if you are using ES2015 features or writing in
coffee-script).

## `-R, --recache`

If you are ever in a situation where your cache is stale or hopp is
refusing to work with an outdated cache, you can use this option to completely
overwrite the cache with a brand new cache. This works by ignoring the
cache on boot and then generating a fresh cache during the build.

This can also be achieved by deleting the `hopp.lock` file and then
running hopp.

## `-j, --jobs`

You might be familiar with the `-j` flag in the tool `make`. This flag
was modelled after that idea. It will distribute the parallel tasks amongst
the number of processes that you specify. This number should always be a positive
number.

If you specify `-j 0` or `--jobs 0`, hopp will assume that you meant to use the
number of cores as the number of jobs.

**Notes:**

 1. This **only works on tasks specified using `hopp.all()`** - not on individual
tasks. It's designed to speed up the execution of many tasks rather than optimize
heavy task chains (we use other methods for that).
 2. **There is no guarantee that this will speed up your builds.** Clustering has a high
 startup and shutdown cost and therefore if your tasks are relatively quick (as hopp
 tries to make sure they are), the useless time spent on clustering will slow down your
 build significantly.
 3. **More jobs != more performance.** Different situations require different number of
 jobs to be optimal. For instance, in our main repo for hopp, we currently have 6 parallel
 tasks in the build process. On my laptop that has a quad-core CPU, 4 jobs is actually a lot
 slower than not using any parallelism. But 2 jobs is the fastest - and so that's what I use.
 It's just a product of realizing at what point does the cost of parallelism drops below the
 cost of too many tasks on one process.

## `-v, --verbose`

Pretty standard flag. It will enable all of hopp's inner debug logging to show up
in the console. If you've got a TTY that supports pretty colors, the debug logs will
be dimmed so that they don't distract from the main logs and errors.

All of the verbose output is written to a `hopp-debug.log` file if hopp runs into any
failures. If you run into a genuine failure (not caused by your code), please open a
new issue on [our Github](https://github.com/hoppjs/hopp) and upload that file.

## `-V, --version`

Outputs the version number from the `package.json`.

## `-h, --help`

Prints the above message.