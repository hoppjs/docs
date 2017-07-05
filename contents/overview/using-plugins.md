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
that would cause hopp to load the `hopp-plugin-sample` plugin.

```json
{
  "devDependencies": {
    "hopp-plugin-sample": "*"
  }
}
```

When using this plugin in your hoppfile, you don't need to do
any extra loading, just call it as a method of your task chain.
For instance:

```javascript
exports.default =
  hopp('src/*.js')
    .sample()
    .dest('dist')
```

**Note:** As you can see above, the `-` in the plugin name tells
hopp which words are part of the plugin's name and it will convert
them to camelcase for you to use.

If you would like to pass any options to the plugin, simply add them
as parameters to the function call. For instance:

```javascript
exports.default =
  hopp('src/*.js')
    .sample({
      // options go here
      beAwesome: true
    })
    .dest('dist')
```

## Local plugins

> Supported in hopp >= 1.2.0.

Sometimes, you may want to load plugins which are stored locally and
aren't published npm packages (in case you have something project
specific that needs to get done or you're trying to test a plugin
you're developing). To tell hopp to load these plugins, you can
call `hopp.load()` with the absolute path to plugin directory in your
hoppfile.

Here's an example that would be appropriate if you had a plugin called
`sample` stored in `plugins/sample`:

```javascript
const hopp = require('hopp')

hopp.load(`${__dirname}/plugins/sample`)

export default
  hopp([ 'src/**/*.js' ])
    .sample()
    .dest('dist')
```