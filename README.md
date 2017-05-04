# Grunt-htmlhint-plus

[![Build Status](https://travis-ci.org/poppinlp/grunt-htmlhint-plus.png?branch=master)](https://travis-ci.org/poppinlp/grunt-htmlhint-plus)
[![Dependency Status](https://david-dm.org/poppinlp/grunt-htmlhint-plus.svg)](https://david-dm.org/poppinlp/grunt-htmlhint-plus)
[![devDependency Status](https://david-dm.org/poppinlp/grunt-htmlhint-plus/dev-status.svg)](https://david-dm.org/poppinlp/grunt-htmlhint-plus#info=devDependencies)

Grunt task to hint html code. Support template.

## Getting Started

This plugin requires Grunt >=0.4.0

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-htmlhint-plus --save-dev
```

or maybe you like `yarn`:

```shell
yarn add grunt-htmlhint-plus
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-htmlhint-plus');
```

## Htmlhintplus Task

_Run this task with the `grunt htmlhintplus` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

## Options

### src {String|Array}

Default: `**/*.html`

Specify source file location. Support glob.

### options.rules {Object}

Default:
```yml
tagname-lowercase: true
attr-lowercase: true
attr-value-double-quotes: true
attr-value-not-empty: true
attr-no-duplication: true
doctype-first: true
tag-pair: true
tag-self-close: false
spec-char-escape: true
id-unique: true
src-not-empty: true
head-script-disabled: false
img-alt-require: true
doctype-html5: true
id-class-value: dash
style-disabled: false
space-tab-mixed-disabled: true
id-class-ad-disabled: true
href-abs-or-rel: true
attr-unsafe-chars: true
```

Specify hint rules. [Supported rules list](https://github.com/yaniswang/HTMLHint/wiki/Rules).

### options.htmlhintrc {String}

Default: `undefined`

Specify rules file path. This option has higher priority than `rules` option.

### options.force {Boolean}

Default: `false`

Whether to throw fatal or not at the end of this task if hint error occur.

### options.newer {Boolean}

Default: `true`

Only hint changed file and new file.

### options.ignore {Object}

Default: `{}`

Hint task will ignore strings between key-value pair from this object.

For example:

```js
// Project configuration
...
ignore: {
	'{{': '}}'
}
...
```

```html
<!-- HTML file -->
...
<a href="foo" class="c1 c2 {{variable from template engine}}">bar</a>
...
```

will be hint as

```html
<!-- HTML file -->
...
<a href="foo" class="c1 c2 ">bar</a>
...
```

### options.customRules {Array}

An array of paths to custom rule files to load and use in your HTMLHinting. See [issue #47](https://github.com/yaniswang/HTMLHint/issues/47) on the [HTMLHint project](https://github.com/yaniswang/HTMLHint). For examples of how to write a custom rule.

### options.extendRules {Boolean}

Extend the default rules instead of only running the rules specified. Default `false`.

### options.output {String|Array}

A string or array of output file types for reporting. Multiple types can also be selected separating them with a pipe character (ex: `console|checkstyle|json`). Available output types include `console`, `default` (alias for console), `text`, `json`, and `checkstyle`. Default `console`.

## Usage Examples

### Basic

```js
// Project configuration
htmlhintplus: {
    build: {
        options: {
            rules: {
                'tag-pair': true,
                'custom-rule': true
            },
            customRules: [
                'rules/custom-rule.js'
            ],
            extendRules: true,
            output: [ 'console', 'text', 'json', 'checkstyle' ]
        }
        src: 'path/to/file'
    }
}
```

### Use htmlhintrc file

```js
// Project configuration
htmlhintplus: {
    html: {
        options: {
            htmlhintrc: 'path/to/file'
        }
        src: [
            'path/to/file',
            'path/to/file2'
        ]
    }
}
```

### Use global options

```js
// Project configuration
htmlhintplus: {
    options: {
        htmlhintrc: 'path/to/file',
        newer: true
    },
    build: {
        options: {
            force: false
        },
        src: [
            'path/1/*.html',
            'path/2/**/*.html'
        ]
    }
}
```

## Demo

Run the test demo:

```shell
grunt test
```

## Changelog

See [CHANGELOG.md](https://github.com/poppinlp/grunt-htmlhint-plus/blob/master/CHANGELOG.md).