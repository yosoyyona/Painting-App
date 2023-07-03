# 3.0 Adding Images
<input type="file" accept="image/*" /> only accept images(any format)

```js
const fileInput = document.getElementById("file")
function onFileChange(event) {
  console.dir(event.target)
}
fileInput.addEventListener("change", onFileChange)
```
console.dir(event.target) -> files
JS on the brower cannot read the file
When the file selected, it is in the memory of the brower
To access it, use URL

```js
function onFileChange(event) {
  const file = event.target.files[0]
  const url = URL.createObjectURL(file) // to access to url of file
  console.log(url) // -> blob:http://127.0.0.1:5000/...
  const image = new Image() // = document.createElement("img")
  image.src = url
  image.onload = function() {
    ctx.drawImage(image, 0, 0, CANVAS_WIDTH, CANVAS_HEIGHT) // (image, x, y, width, height)
    fileInput.value = null
  }
}
```

# 3.1 Adding Text
```js
const textInput = document.getElementById("text")
function onDoubleClick(event) {
  const text = textInput.value
  ctx.lineWidth = 1
  ctx.strokeText(text, event.offsetX, event.offsetY)
}
canvas.addEventListener("dblclick", onDoubleClick)
```
The line width to draw is also changed
-> ctx.save() and ctx.restore()
strokeText only border of the letters -> fillText

```js
function onDoubleClick(event) {
  const text = textInput.value
  if(text !== "") {
    ctx.save() // save current state
    ctx.lineWidth = 1
    ctx.font = "80px serif"
    ctx.fillText(text, event.offsetX, event.offsetY)
    ctx.restore() // and restore the previous state
  }
}
```
- ctx.lineCap = "round" : to make the edge rounder

# 3.2 Saving Image
```js
const saveBtn = document.getElementById("save")
function onSaveClick() {
  const url = canvas.toDataURL() // canvas attribute - make URL of drawing
  const a = document.createElement("a") // do not putting in the website
  a.href = url
  a.download = "myDrawing.png" // anchor attribute - download(when clicked a tag)
  a.click() //fake link click
}
saveBtn.addEventListener("click", onSaveClick)
```

# 3.3 Recap 

# 3.4 CSS
Reset CSS - meyerweb.com/eric/tools/css/reset
@import "reset.css"; to styles.css
css - gap property: set the gap between rows and between columns

mouse hover -> color palette bigger
```css
.color-option {
  transition: transform ease-in-out .1s;
}
.color-option:hover {
  transform: scale(1.2);
}
button {
  all: unset; /* unset all properties */
}
```

# 3.5 Code Challenge

1. font family of text
ctx.font = '(bold) 48px fontName'
Loading fonts with the CSS Font Loading API
- let f = new FontFact('text', 'url(x)')
f.load().then(function() { })

2. font size of text

3. option for fil or stroke of text

4. option for stroke or fill of draw
- onMove, stopPainting -> ctx.fill()