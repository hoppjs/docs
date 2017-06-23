# hopp Plugin Guidelines

We want to help ensure that the hopp plugin ecosystem is a
quality ecosystem and maintains the values of hopp. In an
attempt to accomplish this, we will be maintaining this set
of guidelines to define what a quality plugin is. If you fail
to meet these guidelines, we're afraid we cannot include your
plugin in the official plugin registry. So please make sure
you read this document before setting sail on your project.

 1. **An alternate plugin that solves the same goal must not
 exist.** For instance, if a `hopp-eslint` plugin already exists,
 there is no reason to create another plugin and name it something
 like `hopp-better-eslint`. Instead, try to contribute to the
 existing plugin repository and if there is a serious problem
 (such as the original maintainer no longer providing maintainence)
 then please [contact us](mailto:hopp@apps.alibhai.co) and we will
 try to help you out.

 2. **All plugins must be compatible with node v4 but promote modern
 development.** hopp provides legacy support for node v4 users - and we
 intend on always supporting the oldest maintained node as major versions
 of hopp get released. However, we want to move forwards as much as possible
 towards the newer ECMAScript versions.

 3. **All plugin names must start with `hopp-plugin-`.** This is the convention
 for hopp plugins and it is used by hopp to do its autoloading. If your plugin
 just starts with `hopp-` and not `hopp-plugin-`, it will not be loaded. The extra
 plugin bit is there in case anyone wishes to build utilities or hacks for hopp
 and would like to release it as a non-plugin.