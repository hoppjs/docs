# Using Plugins

Most of the magic of build tools comes from plugins. hopp doesn't
handle any of the transformation for you, it just helps you utilize
existing transformation tools with great efficiency.

If you need help finding a hopp plugin that suits your needs, you
can checkout our [site](https://hoppjs.com/) for a plugin search.

To start using the plugin, simply install it locally and save it
to your `package.json`. Regardless of whether you save it in the
dependencies or developer dependencies, hopp will automatically
load your plugins into the task manager.

Let's look at an example. The following is a minimal package.json
that would cause hopp to load the `hopp-sample-plugin` plugin.

```json
{
  "devDependencies": {
    "hopp-sample-plugin": "*"
  }
}
```

When using this plugin in your hoppfile, you don't need to do
any extra loading, just call it as a method of your task chain.
For instance:

```javascript
exports.default =
  hopp('src/*.js')
    .samplePlugin()
    .dest('dist')
```

**Note:** As you can see above, the `-` in the plugin name tell
hopp which words are part of the plugin's name and it will convert
them to camelcase for you to use.