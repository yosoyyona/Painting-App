# 1.0 The Power of Canvas
canvas API(focused 2D graphics, but 3D too) - WebGL API

# 1.1 Our First Drawing
```js
const canvas = document.querySelector("canvas")
const ctx = canvas.getContext("2d") // get painting brush, the context(ctx)

// in JS too
canvas.width = 800;
canvas.height = 800;

ctx.fillRect(50, 50, 100, 200)
```

# 1.2 Paths
```js
ctx.rect(50, 50, 100, 100) // rectangular path
ctx.stroke() // draw line
```

```js
ctx.rect(50, 50, 100, 100)
ctx.fill() // fill the closed path

ctx.beginPath() // <-- added
ctx.rect(150, 150, 100, 100)
ctx.fillStyle = "red" // previous path changed to red -> add beginPath()
ctx.fill()
```

# 1.3 moveTo and lineTo
```js
ctx.moveTo(50, 50) // moving painting brush
ctx.lineTo(150, 50) // drawing the line
ctx.stroke()
ctx.lineTo(150, 150)
ctx.lineTo(50, 150)
ctx.lineTo(50, 50)
ctx.fill()
```

# 1.4 Drawing Project I
House
```js
ctx.fillRect(200, 200, 50, 200)
ctx.fillRect(400, 200, 50, 200)
ctx.fillRect(200, 200, 200, 20)

ctx.lineWidth = 2
ctx.fillRect(300, 300, 50, 100)

ctx.moveTo(200, 200)
ctx.lineTo(325, 100)
ctx.lineTo(450, 200)
ctx.fill()
```

# 1.5 Drawing Project II
Person
```js
ctx.fillRect(210, 200, 20, 120)
ctx.fillRect(350, 200, 20, 120)
ctx.fillRect(250, 200, 80, 160)
ctx.fillRect(250, 370, 30, 180)
ctx.fillRect(300, 370, 30, 180)
ctx.arc(290, 160, 30, 0, 2 * Math.PI)
ctx.fill()

ctx.beginPath()
ctx.fillStyle = "white"
ctx.arc(275, 155, 8, Math.PI, 2 * Math.PI)
ctx.arc(305, 155, 8, 0, 2 * Math.PI)
ctx.fill()
```