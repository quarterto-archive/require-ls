# require-ls

A [Livescript](http://gkz.github.com/LiveScript/) loader plugin
that may work with module loaders like [RequireJS](http://requirejs.org),
[curl](https://github.com/unscriptable/curl) and
[backdraft](http://bdframework.org/bdLoad/docs/bdLoad-tutorial/bdLoad-tutorial.html).

It is known to work with RequireJS 1.0+.

This loader plugin makes it easy to write your JS functionality in Livescript,
and easily use it in the browser, Node or Rhino. Plus, if you use the RequireJS
optimizer, your Livescript files can be translated to JavaScript, and inlined
into optimized layers for fast performance.

In development, it uses XMLHttpRequest to fetch the .ls files, so you can only
fetch files that are on the same domain as the HTML page, and most browsers place
restrictions on using XMLHttpRequest from local file URLs, so use a web server to
serve your .ls files.

## Usage <a name="usage"></a>

1) Download Livescript for the browser that registers as an AMD module. You
that by using a "raw" GitHub URL. It takes the form of:

    https://raw.github.com/gkz/LiveScript/[BRANCH-OR-VERSION]/extras/livescript.js

Example links:

* [master](https://raw.github.com/gkz/LiveScript/master/extras/livescript.js)
* [1.3.3](https://raw.github.com/gkz/LiveScript/1.3.3/extras/livescript.js)

2) Download the [latest version of ls.js](https://raw.github.com/quarterto/require-ls/latest/ls.js).

3) Reference Livescript files via the ls! plugin name:

    require(['ls!app'], function (app) {

    });

Or, if creating a module:

    define(['ls!util'], function (util) {
        util.doSomething();
    });

If you are using define() in a module written with Livescript:

    define ['ls!util'], (util) ->
        util.doSomething

**VERY IMPORTANT**: Only define anonymous modules using Livescript. Otherwise,
the optimization work will not happen correctly -- the name of the module is changed
to allow inlining of the translated JS content.

## Complete web project <a name="demo"></a>

The **demo** directory shows a complete web example. See the demo/index.html file
as the entry point into the demo. It is not a fancy demo, just shows basic use.

# Optimizing <a name="optimizing"></a>

See **demo/build.sh** for an example build script that drives the optimizer with
the **demo/build.js** build config.

The build will generate a **demo-build** directory with the optimized files. Where
the unoptimized demo directory will load 7 files, the optimized one only loads 2,
and the Livescript files have been converted to JavaScript. Since all the Livescript
modules have been converted to JS after the build, the Livescript module and
the source ls.js module are not included/needed in the built file.

If you want to do dynamic loading of Livescript files after a build, then
comment out `stubModules: ['ls']` and `exclude: ['LiveScript']` from the build
file so that they will be included in the build.

## License <a name="license"></a>

Available via the MIT or new BSD license.
