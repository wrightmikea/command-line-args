[![view on npm](http://img.shields.io/npm/v/command-line-args.svg)](https://www.npmjs.org/package/command-line-args)
[![npm module downloads per month](http://img.shields.io/npm/dm/command-line-args.svg)](https://www.npmjs.org/package/command-line-args)
[![Build Status](https://travis-ci.org/75lb/command-line-args.svg?branch=master)](https://travis-ci.org/75lb/command-line-args)
[![Dependency Status](https://david-dm.org/75lb/command-line-args.svg)](https://david-dm.org/75lb/command-line-args)

**work in progress, draft documentation**

#command-line-args
A command-line parser and usage-guide producer.. Particularly good at organising large sets of options. 

##Install
```sh
$ npm install command-line-args --save
```

##Synopsis
the following `app.js`...
```js
var cliArgs = require("command-line-args");

/* define the command-line options */
var cli = cliArgs([
    { name: "verbose", type: Boolean, alias: "v", description: "Write plenty output" },
    { name: "help", type: Boolean, description: "Print usage instructions" },
    { name: "files", type: Array, defaultOption: true, description: "The input files" }
]);

/* parse the supplied command-line values */
var options = cli.parse();

/* generate a usage guide */
var usage = cli.usage({
    header: "A synopsis application.",
    footer: "For more information, visit http://example.com"
});
    
console.log(options.help ? usage : options);
```
...returns this output at the command line:
```sh
$ node app.js
{}

$ node app.js -v
{ verbose: true }

$ node app.js README.md package.json
{ files: [ 'README.md', 'package.json' ] }

$ node app.js README.md package.json -v
{ verbose: true, files: [ 'README.md', 'package.json' ] }

$ node app.js --help

  A synopsis application.

  Usage

  -v, --verbose    Write plenty output
  --help           Print usage instructions
  --files <array>  The input files

  For more information, visit http://example.com

```

#API Reference
**Example**  
```js
var cliArgs = require("command-line-args");
var cli = cliArgs([
    { name: "help", type: Boolean, alias: "h" },
    { name: "files", type: Array, defaultOption: true}
]);
var argv = cli.parse();
```

<a name="module_command-line-args"></a>
##class: CliArgs ⏏
**Members**

* [new CliArgs(options)](#module_command-line-args)
* [cli.parse([argv])](#module_command-line-args#parse)
* [cli.getUsage(options)](#module_command-line-args#getUsage)
* [type: cli~OptionDefinition](#module_command-line-args.OptionDefinition)

<a name="module_command-line-args"></a>
###new CliArgs(options)
A constructor function, taking your desired command-line option definitions as input, returning an instance of `command-line-args` which you can `parse()` or `getUsage()`.

**Params**

- options [Array.&lt;OptionDefinition&gt;](#module_command-line-args.OptionDefinition) - list of option definitions

<a name="module_command-line-args#parse"></a>
###cli.parse([argv])
Returns a flat, or grouped object containing the values set at the command-line

**Params**

- [argv=process.argv] `object` - Optional argv array, pass to override the default `process.argv`.

**Returns**: `object`  
**Example**  
Output from `parse()` looks something like this:
```js
{
    delete: "thisfile.txt",
    force: true
}
```

or, if the option definitions are grouped:
```js
{
    standard: {
        delete: "thisfile.txt",
        force: true
    },
    extra: {
        intentions: "bad"
    }
}
```

<a name="module_command-line-args#getUsage"></a>
###cli.getUsage(options)
**Params**

- options `object` - options for template
  - title `string` - a title
  - header `string` - a header
  - footer `string` - a footer
  - forms `array` - the invocation forms

**Returns**: `string`  
<a name="module_command-line-args.OptionDefinition"></a>
###type: cli~OptionDefinition
Defines an option

**Scope**: inner typedef of [command-line-args](#module_command-line-args)  
**Type**: `object`  


*documented by [jsdoc-to-markdown](https://github.com/75lb/jsdoc-to-markdown)*.
