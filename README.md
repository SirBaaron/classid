# classid

## A small Python script to shorten ids and classes in html, css and js.

<br>

<b>Examaple:</b><br>
`python classid.py index.html style.css script.js some/other/dependencie.js`

This will shorten all ids and classes the script can find to the shortest possible string.

You can set ids/classes to ignore in an array in a file called `classid-ignore.json`.<br>
It is also possible to save the pairs of long + short classes/ids in `classid-pairs.json` by specifying the `--save-pairs` flag.

<br><br><br>
### Usage with JS:

If you want to also js, you have to import the script `classid.js` during production. (`<script src="classid.js"></script>`)
Whenever you use an id or class in javascript, you have to do it like the following: `classid("id or class")`. The function simply returns the string, but this tells the python script where ids and classes are. When being compressed, the whole term gets replaced by just the short id/class. Once shortened, you can safely remove `classid.js`.


<b>You don't have to edit your html or css before, just make sure its pretty-printed!</b>


Imagine the following snippets of code:
```html
<div id="foo" class="red border ripple"></div>
<div class="dangerzone">Watch out!</div>
```
```css
#foo.red {
  width: 100px;
  height: 100px;
}

.red, .dangerzone {
  background: red;
}

.border {
  border: 1px solid black;
}
```
```javascript
document.getElementById(classid("foo")).innerHTML = "Hello";
```
and the content of classid-ignore.json:
```json
["ripple"]
```
<br>
when shortened, they become:
```html
<div id="a" class="b c ripple"></div>
<div class="d">Watch out!</div>
```
```css
#a.b {
  width: 100px;
  height: 100px;
}

.b, .d {
  background: red;
}

.c {
  border: 1px solid black;
}
```
```javascript
document.getElementById("a").innerHTML = "Hello"
```
and the output of classid-pairs may be:
```json
{"foo": "a", "red": "b", "border": "c", "dangerzone": "d"}
```


<br><br>
<b>Notes:</b><br>
°This script is very basic, if you look for something with more features, have a look at [Google Closure Stylesheets]("https://github.com/google/closure-stylesheets")<br>
°Always have a backup of your files, as the script will change directly the source code!
