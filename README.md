# node-jshint

A command line interface and npm package for jshint.

## Install

To use jshint from any location (for npm v1.x) you need to install using the global (-g) flag.

    npm install -g jshint

## Symbolic Link to ~/.jshint

```bash
ln -s ~/Public/node-jshint/.jshintrc ./.jshintrc
```

## Usage

The command line interface looks like this.

    jshint path path2 [options]

You can also require JSHint itself as a module.

    var jshint = require('jshint');

Note: If you are using npm v1.x be sure to install jshint locally (without the -g flag) or link it globally.

## Text Editor Plugins

* [gedit-node-jshint](https://github.com/niftylettuce/gedit-node-jshint) - Simply use CTRL+J in gedit to run JSHint using `node-jshint`.
* [vim syntastic](https://github.com/scrooloose/syntastic) - Run node-jshint at each file save.
* [sublime-jshint](https://github.com/uipoet/sublime-jshint) - `F7` or `command-B` on any .js file. `F4` next error line,column. `shift-F4` previous error line,column.

## Custom Reporters

Specify a custom reporter module (see example/reporter.js).

    --reporter path/to/reporter.js

Use a jslint compatible xml reporter.

    --jslint-reporter

Show additional non-error data generated by jshint (unused globals etc).

    --show-non-errors

## Configuration Options

**Note:** This behavior described below is very different from versions prior to `0.6`.

The CLI uses the default options that come with JSHint. To have your own configuration apply, there are several methods you can use:

### Specify Manually

Setting the `--config=/path/to/your/config` command line option to specify your own configuration file outside of the directory tree for your project.

### Within your Project's Directory Tree

When the CLI is called, and a configuration file isn't specified already, `node-jshint` will attempt to locate one for you starting in `pwd`. (or "present working directory") If this does not yield a `.jshintrc` file, it will move one level up (`..`) the directory tree all the way up to the filesystem root. If a file is found, it stops immediately and uses that set of configuration.

This setup allows you to set up **one** configuration file for your entire project. (place it in the root folder) As long as you run `jshint` from anywhere within your project directory tree, the same configuration file will be used.

### Home Directory

If all the methods above do not yield a `.jshintrc` to use, the last place that will be checked is your user's `$HOME` directory.

## Ignoring Files and Directories

If there is a .jshintignore file in your project's directory tree, (also provided you run `jshint` from within your project's directory true) then any directories or files specified will be skipped over. (behaves just like a `.gitignore` file)

**Note:** Pattern matching uses minimatch, with the nocase [option](https://github.com/isaacs/minimatch). When there is no match, it performs a left side match (when no forward slashes present and path is a directory).

## Installing dependencies for development

    ./configure

## Build Commands

    jake -T

## Project Guidelines

* All tests are passing.
* No (new) JSHint errors are introduced.
