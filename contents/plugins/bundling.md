# Handling bundling

Bundling refers to any sort of concatenation that is being done
by your plugin. You can this of such a plugin as a many to one
(files) plugin.

In order to support bundling, your plugin must set the `bundle`
option in its exported config to `true`. Your plugin will still
be run against incoming files as any other plugin but hopp will
attempt to use tiny sourcemaps to make the bundling faster.

However, if your plugin requires **all** the files in the stream
in order to compute the bundle (incredibly ineffective), then you
must also set the `recache` option to `true`.

**Note:** It is also worth noting that neither of these options
will automatically switch to buffering mode. If you cannot support
streams and must rely on buffers, you must enable that separately.

## Considerations

Each of these options slows the build down a bit more. If your
plugin is forcing cache busting & using buffering over streaming,
then most of hopp's optimizations will be disabled for the entirety
of the task chain that your plugin exists in.

In order to counter these affects, there are certain things you can
do. The better option is to try and optimize your plugin as much as
possible to not need entire files or to not need a full list of files.
You can take advantage of the persistent caching to store your list
of files or try and write a streaming parsing that operates on chunks.

If none of these options work for you, try and encourage users to
decouple the task in which your plugin is being used with other plugins.
Your task's input can be the output of another task and your task may
depend on the other task. This way the user can take advantage of the
optimizations of hopp for as many operations as possible rather than
slowing down for the entirety of the build.