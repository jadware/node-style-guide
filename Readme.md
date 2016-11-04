# JS Style Guide

This guide was originally created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of contents

### Formatting
* [Tabs for indentation](#tabs-for-indentation)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use semicolons](#use-semicolons)
* [80 characters per line](#80-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Skip braces for single-line](#skip-braces-for-single-line)
* [Opening braces go on the next line](#opening-braces-go-on-the-next-line)
* [Declare one variable per var statement](#declare-one-variable-per-var-statement)

### Naming Conventions
* [Do not universally use lowerCamelCase](#do-not-universally-use-lowercamelcase)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)

### Variables
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Use multi-line ternary operator](#use-multi-line-ternary-operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Design Patterns
* [No singletons or factories](#no-singletons-or-factories)
* [Use callbacks instead of promises](#use-callbacks-instead-of-promises)
* [Use dependency injection](#use-dependency-injection)
* [Refactor often](#refactor-often)

### Functions
* [Write small functions](#write-small-functions)
* [Don't repeat yourself](#dont-repeat-yourself)
* [Return early from functions](#return-early-from-functions)
* [Name your anonymous functions](#name-your-anonymous-functions)
* [Nested anonymous functions are OK](#nested-anonymous-functions-are-ok)
* [Method chaining](#method-chaining)
* [Use globals in scope](#use-globals-in-scope)

### Comments and Docs
* [Use slashes for comments](#use-slashes-for-comments)
* [Use jsdoc](#use-jsdoc)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)
* [Avoid alert](#avoid-alert)

### HTML
* [No grids](#no-grids)
* [Use semantic elements](#use-semantic-elements)
* [Use semantic names](#use-semantic-names)
* [Be minimal](#be-minimal)
* [Avoid nested divs](#avoid-nested-divs)

## Formatting

### Tabs for indentation

Use tabs for indenting your code and do not mix tabs and spaces.
If you already added spaces, change them to tabs.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### No trailing whitespace

Clean up any trailing whitespace in your JS files before committing.

### Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

### Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
```

### Skip braces for single-line

*Right:*

```js
if(true)
	console.log('winning');
```

*Wrong:*

```js
if(true)
{
	console.log('losing');
}
```

Also, notice the lack of whitespace before and after the condition statement.

### Opening braces go on the next line

Your opening braces go on the next line as the statement.

*Right:*

```js
if(true)
{
	console.log('winning');
	return true;
}
```

*Wrong:*

```js
if (true) {
	console.log('losing');
	return true;
}
```

Also, notice the lack of whitespace before and after the condition statement.

### Declare one variable per var statement

Declare one variable per var statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while(keys.length)
{
	var key = keys.pop();
	object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while(keys.length)
{
	key = keys.pop();
	object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## Naming Conventions

### Do not universally use lowerCamelCase

Variables, properties and function names should not universally use `lowerCamelCase`.
They should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

### Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
function BankAccount()
{
}
```

*Wrong:*

```js
function bank_Account()
{
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
var SECOND = 1 * 1000;

function File()
{
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File()
{
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Variables

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Always quote keys.

*Right:*

```js
var a = ['hello', 'world'];
var b =
{
	'good': 'code',
	'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
	'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if(a === '')
	console.log('winning');
```

*Wrong:*

```js
var a = 0;
if (a == '')
	console.log('losing');
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Use multi-line ternary operator

If the ternary operator can fit on a single line, do it.  Otherwise, split it up into multiple lines.


*Right:*

```js
var foo = (a === b) ? 1 : 2;
```

*Wrong:*

```js
var foo = (a === b)
	? 1
	: 2;
```

### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if(isValidPassword)
	console.log('winning');
```

*Wrong:*

```js
if(password.length >= 4 && /^(?=.*\d).{4,}$/.test(password))
	console.log('losing');
```

## Design Patterns

### No singletons or factories

Don't use singletons or factories.  They tend to hide dependencies, violate the [single responsibility principle] (https://en.wikipedia.org/wiki/Single_responsibility_principle),
and cause code to be tightly coupled which interferes with testing.
Also, they carry state around for hte lifetime of the application, which also interferes with unit testing.

Singletons solve one, and only one problem: resource contention.
If you're not specifically solving that problem, singleton is the wrong pattern.

### Use callbacks instead of promises

Generally, bias toward callbacks with a standard (err, result) signature.
Since jQuery uses promises, then they're acceptable in the front-end.
Avoid like the plague in anything that touches a database.

### Use dependency injection

Just read this: http://www.jamesshore.com/Blog/Dependency-Injection-Demystified.html

### Refactor often

Consider rewriting functions and algorithms after they are complete.
Aim to simplify, reduce duplication, and increase reusability.


## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Don't repeat yourself

Don't copy/paste code.  Abstract it away into a helper or utility function as needed.
Refactor code as needed to minimize the amount of lines it takes up.

### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val)
{
	if(val < 0)
		return false;

	if(val > 100)
		return false;

	return true;
}
```

*Wrong:*

```js
function isPercentage(val)
{
	if (val >= 0)
	{
		if (val < 100)
			return true;
		else
			return false;
	} else {
		return false;
	}
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val)
{
	var isInRange = (val >= 0 && val <= 100);
	return isInRange;
}
```

### Name your anonymous functions

Feel free to give your anonymous functions a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd()
{
	console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function()
{
	console.log('losing');
});
```

### Nested anonymous functions are OK

Nest anonymous functions when it keeps code simple.

*Right:*

```js
setTimeout(function tryConnect()
{
	client.connect(function afterConnect()
	{
		console.log('losing');
	});
}, 1000);
```

*Wrong:*

```js
setTimeout(function()
{
	client.connect(afterConnect);
}, 1000);

function afterConnect()
{
	console.log('winning');
}
```


### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
	.findOne({ name: 'foo' })
	.populate('bar')
	.exec(function(err, user)
	{
		return true;
	});
```

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user)
{
	return true;
});

User.findOne({ name: 'foo' })
	.populate('bar')
	.exec(function(err, user)
	{
		return true;
	});

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user)
{
	return true;
});

User.findOne({ name: 'foo' }).populate('bar')
	.exec(function(err, user)
	{
		return true;
	});
```

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb)
{
	// ...
}

var isSessionValid = (session.expires < Date.now());
if(isSessionValid)
{
	// ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb)
{
	// ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if(isSessionValid)
{
	// ...
}
```

### Use jsdoc

Documentation is absolutely necessary, and we use automated code quality analysis tools.
Full jsdoc reference can be found at: https://github.com/google/closure-compiler/wiki/Annotating-JavaScript-for-the-Closure-Compiler

## Miscellaneous

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
var a = [];
if (!a.length)
{
	console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function()
{
	return !this.length;
}

var a = [];
if (a.empty())
{
	console.log('losing');
}
```
### Avoid alert
Never, ever use the alert() function.  You can use console.log if you eventually remove it.  console.error and console.warn are acceptable.

## HTML

### No grids
Grids are not semantic, so do not ever use them.  No "column" classes or anything like that.  HTML should contain content and content structure, not layout.

### Use semantic elements
When possible, replace classes with the corresponding descriptive element.  For example, instead of a <div class="para">, use the <p> tag instead.

### Use semantic names
A common pitfall of class naming is to describe the layout with names like "left", "right", or "clearfix".  These are wrong for various reasons, and the best discussion of these is at the following article: https://css-tricks.com/semantic-class-names/

### Be minimal
Keep your HTML short and sweet.  Use CSS and pseudo-elements, when necessary, to 

### Avoid nested divs
Keep your HTML as flat as possible and use CSS to do the magic.  

*Wrong:*

```html
<div class="outer">
	<div class="inner">
		<div class="content">
			<p>information</p>
		</div>
	</div>
</div>
```

*Right:*

```html
<p>information</p>
```
