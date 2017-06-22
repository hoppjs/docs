# Writing your first plugin

This section will help you start writing your plugin from scratch. However, we recommend
that you clone the [hoppjs/hopp-sample-plugin](https://github.com/hoppjs/hopp-sample-plugin)
repository when you're working on your actual plugin. It contains the initial setup that you
will need to write your plugin.

## So... ES5? ES2015? ES2050?

hopp maintains compatibility with node v4 but all the code should be written using the latest
stable (stage 3 & 4 features) ECMAScript features and transpiled using [babel-preset-env](https://github.com/babel/babel-preset-env).

This means that you should be writing your code using ES2015 modules (import/export) and async
functions (where applicable). If you would still like to write your plugin without any transpiling,
this guide will also cover the manual ways to handle certain things (but not all).

## 