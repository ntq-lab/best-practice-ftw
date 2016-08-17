## 1. Always close your tags

#### Bad
```html
<li>Some text here 1
<li>Some text here 2
<li>Some text here 3
```

#### Good
```html
<li>Some text here 1</li>
<li>Some text here 2</li>
<li>Some text here 3</li>
```

## 2. Start with DOCTYPE

`DOCTYPE` is required for activing standard mode.

#### Bad
```html
<html>
...
</html>
```

#### Good
```html
<!DOCTYPE html>
<html>
...
</html>
```

## 3. Escape &, <, >, ", and ' with named character references

These characters should escape always for a bug-free HTML document.

#### Bad
```html
<h1>The "&" character</h1>
```

#### Good
```html
<h1>The &quot;&amp;&quot; character</h1>
```

## 4. Don't mix empty element format

Consistency is a key for readability.

#### Bad
```html
<img alt="HTML Best Practices" src="/img/logo.png">
<hr />
```

#### Good
```html
<img alt="HTML Best Practices" src="/img/logo.png">
<hr>
```

## 5. Don't mix character cases

It gives a consistency also.

#### Bad
```html
<a HREF="http://w3schools.com">W3schools</A>
```

#### Good
```html
<a href="http://w3schools.com">W3schools</a>
```

## 6. Omit boolean attribute value

#### Bad
```html
<a HREF="http://w3schools.com">W3schools</A>
```

#### Good
```html
<a href="http://w3schools.com">W3schools</a>
```

## 7. Add `title` element

A value for `title` element is used by various application not only a browser.

#### Bad
```html
<head>
	<meta charset="UTF-8">
</head>
```

#### Good
```html
<head>
	<meta charset="UTF-8">
	<title>HTML Best Practices</title>
</head>
```

## 8. Don’t use `base` element

An absolute path or URL is safer for both developers and users.

#### Bad
```html
<head>
	...
	<base href="/blog/">
	<link href="hello-world" rel="canonical">
	...
</head>
```

#### Good
```html
<head>
	...
	<link href="/blog/hello-world" rel="canonical">
	...
</head>
```

## 9. Specify document character encoding

UTF-8 is not default in all browsers yet.

#### Bad
```html
<head>
	<title>HTML Best Practices</title>
</head>
```

#### Good
```html
<head>
	<meta charset="UTF-8">
	<title>HTML Best Practices</title>
</head>
```

## 10. Write one list item per line

Looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong line is hard toooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo read.

#### Bad
```html
<ul>
	<li>General</li><li>The root Element</li><li>Sections</li>...
</ul>
```

#### Good
```html
<ul>
	<li>General</li>
	<li>The root Element</li>
	<li>Sections</li>
	...
</ul>
```

## 11. Don't use br element only for presentational purpose

`br` element is not for line breaking, it is for line breaks in the contents.

#### Bad
```html
<p><label>Rule name: <input name="rule-name" type="text"></label><br>
<label>Rule description:<br>
<textarea name="rule-description"></textarea></label></p>
```

#### Good
```html
<p><label>Rule name: <input name="rule-name" type="text"></label></p>
<p><label>Rule description:<br>
<textarea name="rule-description"></textarea></label></p>
```

## 12. Wrap form control with `label` element

`label` helps focusing form element.

#### Bad
```html
<p>Query: <input name="q" type="text"></p>
```

#### Good
```html
<p><label>Query: <input name="q" type="text"></label></p>
```

## 13. Omit `for` attribute if possible

`label` can contain some form elements.

#### Bad
```html
<label for="q">Query: </label><input id="q" name="q" type="text">
```

#### Good
```html
<label>Query: <input name="q" type="text"></label>
```
