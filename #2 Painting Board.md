# 2.0 Painting Lines
mouse click -> draw a line
```js
function onClick(event) {
  ctx.lineTo(event.offsetX, event.offsetY)
  ctx.stroke()
}
canvas.addEventListener("click", onClick)
```
mouse move -> draw a line
```js
function onMove(event) {
  ctx.beginPath()
  ctx.moveTo(0, 0)
  const color = colors[Math.floor(Math.random()*colors.length)]
  ctx.strokeStyle = color
  ctx.lineTo(event.offsetX, event.offsetY)
  ctx.stroke()
}
canvas.addEventListener("mousemove", onMove)
```

# 2.1 Mouse Painting
mouse click and drag
```js
let isPainting = false;

function onMove(event) {
  if(isPainting) {
    ctx.lineTo(event.offsetX, event.offsetY)
    ctx.stroke()
    return
  }
  ctx.moveTo(event.offsetX, event.offsetY)
}

const startPainting = () => { isPainting = true }
const stopPainting = () => { isPainting = false }

canvas.addEventListener("mousemove", onMove)
canvas.addEventListener("mousedown", startPainting)
canvas.addEventListener("mouseup", stopPainting)
```
mouse down 상태로 canvas 나가서 up하고 다시 canvas 들어오면 계속 그려짐
(canvas에서 stopPainting 함수가 실행되지 않아서)
=> 2가지 해결 방법
- canvas.addEventListener("*mouseleave*", stopPainting) : 이벤트리스너 추가하기
- *document*.addEventListener("mouseup", stopPainting) : 범위 변경하기

# 2.2 Line Width
```html
<input id="line-width" type="range" min="1" max="10" value="5" step="0.1" />
```
depending on the step, the moving of cursor is different, the smaller the smoother

```js
const lineWidth = document.getElementById("line-width")
ctx.lineWidth = lineWidth.value

function onLineWidthChange(event) {
  ctx.lineWidth = event.target.value
}
lineWidth.addEventListener("change", onLineWidthChange)
```
Add <ctx.beginPath()> in stopPainting function!

# 2.3 Paint Color Part I
```html
<input id="color" type="color" />
```
```js
const color = document.getElementById("color")

function onColorChange(event) {
  ctx.strokeStyle = event.target.value
  ctx.fillStyle = event.target.value
}
color.addEventListener("change", onColorChange)
```

# 2.4 Paint Color Part II
premaid color palette
attribute <data- > whatever data we want to use in JS
```html
<div class="color-option" style="background-color: #ffb8b8" data-color="#ffb8b8"></div>
```

- "colorOptions.forEach()" is not a function, becuase it is a *array-like object, html collection* so it has to be written inside of Array.from()
- onColorClick function - console.dir(event.target) check! => dataset.color

```js
const colorOptions = Array.from(document.getElementsByClassName("color-option"))

function onColorClick(event) {
  const colorValue = event.target.dataset.color
  ctx.strokeStyle = colorValue
  ctx.fillStyle = colorValue
  color.value = colorValue
}

colorOptions.forEach(color => color.addEventListener("click", onColorClick))
```

# 2.5 Filling Mode
button -> drawing to filling
```js
const modeBtn = document.getElementById("mode-btn")

let isFilling = false;

function onModeClick() {
  if(isFilling) {
    isFilling = false
    modeBtn.innerText = "Fill"
  } else {
    isFilling = true
    modeBtn.innerText = "Draw"
  }
}

function onCanvasClick() {
  if(isFilling) {
    ctx.fillRect(0, 0, 800, 800)
  }
}

canvas.addEventListener("click", onCanvasClick)
modeBtn.addEventListener("click", onModeClick)
```

# 2.6 Eraser
```js
const eraseAllBtn = document.getElementById("erase-all-btn")
const eraseBtn = document.getElementById("erase-btn")

function onEraseAllClick() {
  ctx.fillStyle = "white"
  ctx.fillRect(0, 0, CANVAS_WIDTH, CANVAS_HEIGHT)
}

function onEraseClick() {
  ctx.strokeStyle = "white"
  isFilling = false
  modeBtn.innerText = "Fill"
}

eraseAllBtn.addEventListener("click", onEraseAllClick)
eraseBtn.addEventListener("click", onEraseClick)
```

# 2.7 Recap

