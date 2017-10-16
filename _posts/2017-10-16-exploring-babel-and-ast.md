---
layout: post
title:  "Exploring JavaScript Compiler - Babel and Abstract Syntax Tree"
image: ''
date:   2017-10-16 00:00:00
tags:
- JavaScript
- Babel
- Compiler
- AST
description: ''
categories:
- JavaScript 
---

<p class="music-read"><iframe src="https://open.spotify.com/embed/track/3ZffCQKLFLUvYM59XKLbVm" width="300" height="80" frameborder="0" allowtransparency="true"></iframe></p>

<img src="/assets/img/posts/2017-10-16-exploring-babel-and-ast/snapshot_babel_repl.png">

## Introduction to Babel
[Babel](https://babeljs.io/) is a JavaScript compiler that converts human readable code to machine friendly format named
Abstract Syntax Tree (AST) to **visit**, **analyze** and possibly **modify** the AST then write AST over files as runtime code. 

As JavaScript was initially born for browsers and different browsers possibly understand different JavaScript syntax, the desired runtime code should be compatible across different JavaScript interpreters
(e.g. IE9 vs Google Chrome, Node.js 6 vs Node.js 8). [caniuse.com](https://caniuse.com/#search=array.isArray) is a tool born for developers to search availability of syntax and build-in functions (Object prototype). [Browserstack](https://www.browserstack.com/) is another tool can be used for browser compatibility testing. 

Babel is famous for transpiling ES6 JavaScript code to ES5 JavaScript code so developers can write code in ES6 which is more intuitive meanwhile clients consume transpiled ES5 code which actually implements the same logic with older syntax but better compatibility ([funny brefing on history of JavaScript versions](https://benmccormick.org/2015/09/14/es5-es6-es2016-es-next-whats-going-on-with-javascript-versioning/)). You can also use Babel to analyze your source code and acquire information. For example, [babel-plugin-react-intl](https://github.com/yahoo/babel-plugin-react-intl) is a tool for creating multi-language React Web application. It extracts all textual content written in JSX React Component `<FormattedMessage/>` into a JSON file which helps you internationalize your React application easily.

We don't have to touch the source code of a babel-plugin during most of time of development. However, to be able to make contributions to Babel community or debug a weird behavior at webapp or Node.js project, we have to understand Babel. It's not difficult! Let's understand this tool used by thousands of JavaScript developers every day with ♥️

<img src="/assets/img/posts/2017-10-16-exploring-babel-and-ast/babel_system.png">

## Babel is Not Scary. Three Things!
Babel is not scary. I personally had the fear for Babel months ago, because I thought I didn't take any compiler course at university so it would be super difficult for me to understand Babel. To resolve [a bug I encountered](https://github.com/yahoo/babel-plugin-react-intl/issues/125) during development, I was forced to check out some YouTube videos and tutorials about the fundamental of JavaScript compiler. Let's explore it together today with practical cases and 
code. I hope you will gain some insights about the magics happening behind [babel-plugins](https://babeljs.io/docs/plugins/).
John hopes this post could shorten the time you spend on understanding the fundamental stuff.

### 1. Parse
***Babel parses source code to AST which is an abstraction of your code for machine.*** Don't worry! To read an AST is NOT scary!  I agree that to understand how to turn code to an AST is probably scary ^_^

So what does it look like when parsing JavaScript? Using below ES6 class as an example:
```javascript
import React from 'react'; 

class HelloWorld extends React.Component{
	constructor() {
		super();
		this.HELLO_TEXT = 'Hello World!';
	}
	
	sayHello() {
		console.log(this.HELLO_TEXT)
	}
	
  	render() {
		return (
		  <h1> 
		    {this.HELLO_TEXT}
		  </h1>
		)
	}
}
```

Before reading subsequent AST examples, please note that parsing source code to AST is "contextless". For example, converting line #1 `import React from 'react'` to AST doesn't require access to the actual `react` package. The parser only abstracts your source code but doesn't do runtime evaluation. 

The assignment of `HELLO_TEXT` as `class property` looks like below in AST 
<img style="width: 600px" src="/assets/img/posts/2017-10-16-exploring-babel-and-ast/snapshot_AST_value_assignment.png">

The class method definition `sayHello()` looks like below in AST
<img style="width: 650px" src="/assets/img/posts/2017-10-16-exploring-babel-and-ast/snapshot_AST_class_method.png">

Nowadays, there are different versions of JavaScript ASTs transformed by different parsers. [babylon](https://github.com/babel/babylon) (by Babel) and [espree](https://github.com/eslint/espree) (by eslint) are two popular JavaScript parsers with sophisticated community support. If you understand one of them, the other will be smoothly understood because they are pretty similar. 

### 2. Transform
***Babel traverses AST to explore, analyse or modify AST programmatically***

The `visitor` pattern is very commonly used to traverse an AST. There are many AST node types you can visit in Babel. You don't have to memorize all of them, this is the list - [babel-types](https://github.com/babel/babel/tree/master/packages/babel-types#babel-types).

Each node `path` has many build-in functions for us to use. Again, we don't have to memorize them. This is the API - [babel-core API](https://npmdoc.github.io/node-npmdoc-babel-core/build/apidoc.html)

Example of **(a)** visiting `MemberExpression ` nodes and converting `console.log()` to `console.debug()` **(b)** visiting `JSXComponent` nodes and converting `<h1>` to `<Title>`:
```javascript
visitor: {
      MemberExpression(path) {
        if (path.node.object.name === "console" && path.node.property.name === "log") {
          path.node.property.name = "debug";
        }
      },

      JSXIdentifier(path) {
        if (path.node.name === "h1") {
          path.node.name = "Title";
        }
      }
    }
```

Result (this is also an exmaple of #3 Generate):
```javascript
import React from 'react'; 

class HelloWorld extends React.Component {
	constructor() {
      	super();
		this.HELLO_TEXT = 'Hello World!';
	}
	
	sayHello() {
		console.debug(this.HELLO_TEXT) // 'log()' is replaced by 'debug()'
	}
  
	render() {
		// <h1> is replaced by <Title>
		return (
		  <Title> 
		    {this.HELLO_TEXT}
		  </Title>
		);
	}
}
```
### 3. Generate
***Finally, Babel generates actual runtime code based on AST***

For example, if we transform an AST of above example code written in ES6 to an AST of code written in ES5, the output will be:
```javascript
// You're awesome if patient for reading below ES5 code. Feel free to skip it.
var _react = require('react');

var _react2 = _interopRequireDefault(_react);

var HelloWorld = function (_React$Component) {
  _inherits(HelloWorld, _React$Component);

  function HelloWorld() {
      _classCallCheck(this, HelloWorld);

      var _this = _possibleConstructorReturn(this, (HelloWorld.__proto__ || Object.getPrototypeOf(HelloWorld)).call(this));

      _this.HELLO_TEXT = 'Hello World!';
      return _this;
  }

  _createClass(HelloWorld, [{
      key: 'sayHello',
      value: function sayHello() {
        console.debug(this.HELLO_TEXT);
      }
  }, {
      key: 'render',
      value: function render() {
        return _react2.default.createElement(
          Title,
          null,
          this.HELLO_TEXT
        );
      }
  }]);

  return HelloWorld;
}(_react2.default.Component);
```

## Development/Debug Tool
[AST Explorer](https://astexplorer.net/#/gist/45ef5b4307ada5b7c88d09ea621ef2a7/038c7f557caf002119563a7016d9c855d01d12a6) is an integrated online tool that is very friendly for beginners as it requires almost 0 setup.

<img src="/assets/img/posts/2017-10-16-exploring-babel-and-ast/snapshot_AST_Explorer.png">

You can play around different AST parsers and write you own transform logic. The  AST and generated source code are shown immediately after updating source code.

## How is Babel applied in real projects?
It depends on your use case. It can be applied in the bundler of your build pipeline of a JavaScript project. It can also be applied in a `Node.js` script for code analysis purpose.

Sharing some my own understandings:

- babel plugins are usually  applied at bundling system such as Webpack (with [babel-loader](https://github.com/babel/babel-loader)) to resolve JavaScript version compatibility issue. You can usually find Babel configuration in `.babelrc` or `package.json`. Example:
```javascript
{
    "presets": [
        "es2015"
    ],
    "plugins": [
        "transform-object-rest-spread",
        "transform-runtime"
    ]
}
```

- For projects using babel for code analysis and information extraction, we usually invoke Babel APIs from `babel-core` module as it allows us to parse/transform/generate code programmatically and independently. 
Example in `Node.js`: 
```javascript
import * as babel from 'babel-core';
// Transform 
const transpiledCode = babel.transformFileSync('./helloWorld.js', {
  plugins: [
    ['transform-es2015-arrow-functions', { spec: true }],
    'transform-class-properties',
    'transform-object-rest-spread',
    'transform-runtime',
  ],
}).code;
```


## Some concerns we may have
- **If we use babel to transform ES6 code to ES5 code, will Babel pollute the stack trace of an 
`Error` object when debugging? It compiles my source code to some code written differently.** 

The answer is YES. **However**, you don't have to worry about debuggability. `babel-register` module automatically converts back transpiled code in stack trace to original source code with the help of [source-map-support](https://www.npmjs.com/package/source-map-support).

- **What's the difference between babel `preset` and `plugin`?**

`preset` is a collection of many `plugins`. It resolves the issue where people have to manually set up multiple plugins to achieve one goal. For example, to compile ES6 code to ES5 code, you will need all plugins shown below, yet preset `babel-preset-es2015` contains all of them in a single module:
```
check-es2015-constants
transform-es2015-arrow-functions
transform-es2015-block-scoped-functions
transform-es2015-block-scoping
transform-es2015-classes
transform-es2015-computed-properties
transform-es2015-destructuring
transform-es2015-duplicate-keys
transform-es2015-for-of
transform-es2015-function-name
transform-es2015-literals
transform-es2015-modules-commonjs
transform-es2015-object-super
transform-es2015-parameters
transform-es2015-shorthand-properties
transform-es2015-spread
transform-es2015-sticky-regex
transform-es2015-template-literals
transform-es2015-typeof-symbol
transform-es2015-unicode-regex
transform-regenerator
```

\- The End -

***Note: All opinions in this post are personal. All images, attachments and code in this post are original from [@John](http://www.zhuoran.li).***