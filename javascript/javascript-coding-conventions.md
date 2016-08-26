## 1. Use === instead of ==

The == comparison operator always converts (to matching types) before comparison.

#### Bad
```javascript
0 == ''; // true
1 == '1'; // true
1 == true; // true
```

#### Good
```javascript
0 === ''; // false
1 === '1'; // false
1 === true; // false
```

## 2. Don't Use Short-Hand

Technically, you can get away with omitting most curly braces and semi-colons. Most browsers will correctly interpret the following:

```javascript
if (someVariableExists)
	x = false;
```

However, consider this:

```javascript
if (someVariableExists)
	x = false;
	anotherFunctionCall();
```

One might think that the code above would be equivalent to:

```javascript
if (someVariableExists) {
	x = false;
	anotherFunctionCall();
}
```

Unfortunately, he'd be wrong. In reality, it means:

```javascript
if (someVariableExists) {
	x = false;
}

anotherFunctionCall();
```

## 3. Use JS Lint

```bash
"JSLint takes a JavaScript source and scans it. If it finds a problem, it returns a message describing the problem and an approximate location within the source. The problem is not necessarily a syntax error, although it often is. JSLint looks at some style conventions as well as structural problems. It does not prove that your program is correct. It just provides another set of eyes to help spot problems."
- JSLint Documentation
```

## 4. Place Scripts at the Bottom of Your Page

The primary goal is to make the page load as quickly as possible for the user. When loading a script, the browser can't continue on until the entire file has been loaded. Thus, the user will have to wait longer before noticing any progress.

#### Bad
```javascript
<html>
	<head>
		<script type="text/javascript" src="example.js"></script>
	</head>
	<body>
		<div></div>
	</body>
</html>
```

#### Good
```javascript
<html>
	<head>
	</head>
	<body>
		<div></div>
		<script type="text/javascript" src="example.js"></script>
	</body>
</html>
```
#### Other trick
In some cases, if you do not want to move script tag to bottom of page, consider to use async and defer attribute in script tag.

```
<script src="example.js" async></script>
<script src="example.js" defer></script>
```
To understand how to use async and defer, please read more: http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html

Note: defer attribute does not support <= IE9;

## 5. Leave unnessary logic outside of the `For` statement

When executing lengthy "for" statements, don't make the engine work any harder than it must.

#### Bad
```javascript
for(var i = 0; i < someArray.length; i++) {
	var container = document.getElementById('container');
	container.innerHtml += i;
}
```

#### Good
```javascript
var container = document.getElementById('container');
var length = someArray.length;
var i;

for(i = 0; i < length; i++) {
	container.innerHtml += i;
}
```

## 6. Use Parameter Defaults

If a function is called with a missing argument, the value of the missing argument is set to undefined.

Undefined values can break your code. It is a good habit to assign default values to arguments.

#### Bad
```javascript
function myFunction(object) {
	return object.name;
}

console.log(myFunction()); // => Uncaught TypeError: Cannot read property 'name' of undefined
```

#### Good
```javascript
function myFunction(object) {
	var newObject = Object.assign({}, object); // Note: This method not support on Intener Explorer. I recommended you should be use external libraries (Ex: lodash, object-assign...)

	return newObject.name;
}

console.log(myFunction()); // Undefined
```

## 7. Avoid globals

Global variables and function names are an incredibly bad idea. The reason is that every JavaScript file included in the page runs in the same scope. If you have global variables or functions in your code, scripts included after yours that contain the same variable and function names will overwrite your variables/functions.

#### Bad
```javascript
var current = null;
function init() {...}
function change() {...}
function verify() {...}
```

#### Good
```javascript
(function(exports) {
	var current = null;
	function init() {...}
	function change() {...}
	function verify() {...}

	// export to global
	exports.verify = verify;
})(window);
```

## 8. Use {} instead of new Object() and [] instead of new Array()

* Shorter and more readable
* Safer: literals will still work when the Array or Object constructors have been overridden

#### Bad
```javascript
function Array() {
	return 1;
}

var arr = new Array();
console.log(arr);
```

#### Good
```javascript
var arr = [];
console.log(arr);
```

* Faster

#### Bad
```javascript
var counter = 1e7;
var arr;

console.time('array time');
for (var i = 0; i < counter; i++) {
	arr = new Array();
}
console.timeEnd('array time'); // 132.071ms
```

#### Good
```javascript
var counter = 1e7;
var arr;

console.time('array time');
for (var i = 0; i < counter; i++) {
	arr = [];
}
console.timeEnd('array time'); // 40.505ms
```
