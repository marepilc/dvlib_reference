# dvlib API Reference
## Quick Start
The *dvlib* offers you a set of functions you can use to draw on the canvas. If the canvas already exists and has an ID attribute, you can select the canvas using **selectCanvas** function. If there is no canvas yet you can create one using function **createCanvas** and change the default dimensions with the **resizeCanvas** function.

```ts
body = document.getElementsByTagName('body')[0];
createCanvas(body);
resizeCanvas(600, 300);
```

The quickest way to start coding is by cloning [dvlib_template](https://github.com/marepilc/dvlib_template) repository:

```
git clone --depth=1 https://github.com/marepilc/dvlib_template.git projectname
```
```
rm -rf !$/.git
```
```
cd projectname
```

and installing dependencies:

```
npm i
```

The template comes with a development server, therefore you can run the server with command:

```
npm start
```
and that's it! You can start coding.

## Principles
When the canvas is already available we can start drawing. To initiate the drawing process you have to call **dvStart** function. It takes four functions as arguments in the following order:

- **setup**
- **draw**
- **events**
- **loadAssets**

Because the functions are passed as arguments the function’s names are up to you.

1. Function **setup**. If it’s defined is called only once. You can use it for example to create objects declared as a global variables.
2. Function **draw**. It is called by default 60 times per second. 
3. In the function **events** you can define user interactions.
4. Function **loadAssets** is used to pre-loading assets to the visualization (data in JSON format and pictures).

Please bear in mind, that the canvas origin is located in the top-left corner.
 
 ![canvas origin](https://dvlib.org/images/canvasorigin.png?)
 
 To illustrate this, clone the [dvlib_template](https://github.com/marepilc/dvlib_template) repository, install dependencies (`npm i`), and change the *main.ts* file as shown below:
 
 ```ts
import { 
    createCanvas, dvStart, resizeCanvas, background, fill, 
    textSize, text, blue, mouse, addAsset, placeImage,
    assets, ImgOrigin 
 } from "dvlib";
 
 dvStart(setup, draw, events, loadAssets);
 
 let x: number;
 let y: number;
 
 function setup(): void {
    let body: HTMLElement = document.getElementsByTagName('body')[0];
    createCanvas(body);
    resizeCanvas(window.innerWidth, window.innerHeight);
 }
 
 function draw() {
    background('#2d2f2f');
    fill(blue);
    textSize(24);
    text('Click anywhere to place logo', 50, 50);
    placeImage(assets.logo, x, y, ImgOrigin.cc, 100, 100);
 }
 
 function events() {
    mouse.click = function () {
        x = mouse.x;
        y = mouse.y;
    }
 }
 
 function loadAssets() {
    addAsset({ id: 'logo', src: 'images/dvlogo.png'})
 }
 ```
 
When you start the server, you will see that the canvas is resized to the entire window, and mouse click results in placing the logo image at cursor position.
 
## Functions, Classes and Global Variables
**dvlib** offers bunch of useful functions for drawing on the canvas beautiful data visualizations. One function has to be called in evert program written with the *dvlib* - [dvStart](#dvStart).

### Main Functions
- [dvStart](#dvStart)
- [createCanvas](#createCanvas)
- [selectCanvas](#selectCanvas)
- [resizeCanvas](#resizeCanvas)
- [cursor](#cursor)

### Canvas Transformations
- [translate](#translate)
- [rotate](#rotate)
- [scale](#scale)

### Drawing functions
- [staticDrawing](#staticDrawing)
- [save](#save)
- [restore](#restore)
- [clear](#clear)
- [background](#background)
- [stroke](#stroke)
- [strokeWidth](#strokeWidth)
- [noStroke](#noStroke)
- [strokeCup](#strokeCup)
- [strokeJoin](#strokeJoin)
- [dashLine](#dashLine)
- [solidLine](#solidLine)
- [fill](#fill)
- [noFill](#noFill)
- [shadow](#shadow)

### Shapes
- [point](#point)
- [line](#line)
- [arc](#arc)
- [circle](#circle)
- [ellipse](#ellipse)
- [ring](#ring)
- [rect](#rect)
- [star](#star)
- [polygon](#polygon)
- [spline](#spline)
- [bezier](#bezier)

### Custom Shapes
You can draw on the canvas any shape you want by using the functions below:
- [beginShape](#beginShape)
- [endShape](#endShape)
- [closeShape](#closeShape)
- [moveTo](#moveTo)
- [lineTo](#lineTo)
- [bezierTo](#bezierTo)
- [quadraticTo](#quadraticTo)

### Colors
There are a few predefined colors in **dvlib**.

Color names: **light**, **dark**, **yellow**, **orange**, **green**, **red**, **blue**, and **magenta**.

![colors](https://dvlib.org/images/dvlibcolors.png?)

If color is an argument of the **dvlib** function, it can be passed in the following ways: 

```ts
fill('#567F98');  // as string in HEX code
fill(orange);  // as predefined constant
fill('#567F98', 0.5);  // as string in HEX code with opacity value
fill(0);  // as digit between 0 and 255 for the gray scale
fill(127, 28, 215);  // as digits between 0 and 255 dor red, green and blue value  
fill(127, 28, 215, 0.75);  // as digits between 0 and 255 dor red, green and blue value
                           // with opacity walue
```

Functions to work with colors:
- [blend](#blend)
- [randomColor](#randomColor)

### Assets
Functions to work with assets:
- [placeImage](#placeImage)

### Typography
Functions to work with text:
- [text](#text)
- [textSize](#textSize)
- [textWidth](textWidth)
- [textDim](#textDim)
- [textAlign](textAlign)
- [fontStyle](#fontStyle)
- [fontWeight](#fontWeight)
- [fontFamily](#fontFamily)
- [lineHeight](#lineHeight)
- [textOnArc](#textOnArc)
- [number2str](#number2str)
- [thousandSep](#thousandSep)

### Math and Data
##### Constants
- **`E`** --- `2.718281828459045`
- **`PI`** --- `3.141592653589793`
- **`TWO_PI`** --- `2 * PI`
- **`HALF_PI`** --- `PI / 2`
- **`PHI`** --- golden ratio (1 + &Sqrt;5) / 2

##### Trigonometric Functions
- `cos = Math.cos`
- `tan = Math.tan`
- `asin = Math.asin`
- `acos = Math.acos`
- `atan = Math.atan`
- `atan2 = Math.atan2`

##### Conversions
- [deg2rad](#deg2rad)
- [int](#int)
- [str](#str)
- [mm2px](#mm2px)
- [px2mm](#px2mm)
- [hexStr](#hexStr)
- [svg2img](#svg2img)

##### Other Functions
- [dist](#dist)
- [round](#round)
- [round2str](#round2str)
- `floor = Math.floor`
- `ceil = Math.ceil`
- [constrain](#constrain)
- [sq](#sq)
- `pow = Math.pow`
- `sqrt = Math.sqrt`
- `abs = Math.abs`
- [max](#max)
- [min](#min)
- [sum](#sum)
- [avg](#avg)
- [centile](#centile)
- [revCentile](#revCentile)
- [iqr](#iqr)
- [dataRange](#dataRange)
- [stdDev](#stdDev)
- [randomInt](#randomInt)
- [choose](#choose)
- [random](#random)
- [shuffle](#shuffle)
- [unique](#unique)
- [fibonacci](#fibonacci)
- `prnt` = `console.log`

##### Scales
- [linearScale](#linearScale)
- [ordinalScale](#ordinalScale)

##### Classes
- [Vector](#Vector)
- [Noise](#Noise)

### Global Variables
- **width** --- contains the width of the canvas in pixels.
- **height** --- contains the height of the canvas in pixels.
- **keyboard** --- instance of [Keyboard](#Keyboard) class.
- **mouse** --- instance of [Mouse](#Mouse) class.
- **animation** --- instance of [AnimationCtrl](#AnimationCtrl) class.
- **assets** --- an object which contains all the assets loaded withe the **loadAssets** function. The usage is described together with [dvStart](#dvStart) function.

#### dvStart
This function has to be called to initiate our program. **dvStart** takes four functions as arguments. Not all are required.
The first function should contain the code only for initialization. It is executed only once, thus should be used for setup actions only.
Second function is called 60 times a second, and is used for redrawing canvas with mentioned frequency. This function has to be always passed as a second argument, so if there is no need for setup function, *null* shall be passed instead.

```ts
dvStart(null, draw);
```

The third function passed to the **dvStart** define actions on specific events i.e on mouse click. Inside the **events** function you can redefine the following functions:
- `mouse.wheel(e: WheelEvent)`
- `mouse.down()`
- `mouse.up()`
- `mouse.click()`
- `mouse.dbClick()`
- `dV.keyUp(key: string)  //key is a KeyboardEvent.key i.e. 'Alt'`
- `dV.keyDown(key: string)`
- `window.onresize()`

Example:

```ts
window.onresize = function () {
    console.log('Window has been resized!');
}
```

The last function you can pass as an argument to the **dvStart** is **loadAssets** function. For every asset you want to load, you have to call **addAsset** function:

```ts
function loadAssets() {
    addAsset({ id: 'myPicture', src: 'path/myPicture.png'});
    addAsset({ id: 'data', src: 'path/data.json'});
}
```

All loaded assets will be available in the global object *assets*, i.e. `assets.myPicture`.

***Remember!***
Even if the arguments of **dvStart** are optional, the order is important. It means if you have to load assets to jour program, but you do not need handling the events, you have to call the function like shown below:

```ts
dvStart(setup, draw, null, loadAssets);
```

#### createCanvas
`createCanvas(target: HTMLElement, id?: string): void`
Function takes as an argument the HTMLElement and append to it the HTML Canvas. Additionally creates the instance of the **DV** class --- necessary for proper library functioning. Optionally the canvas ID can be set.

#### selectCanvas
`selectCanvas(id: string): void`
It is an alternative function to **createCanvas** in the situation, where <canvas\> element already exist in the *\*.html* file. You have to pass as an argument the canvas' \#id.

#### resizeCanvas
`resizeCanvas(w: number, h: number, canvas: HTMLCanvasElement): void`
Function changes dimensions of the canvas. The *canvas* argument is optional, and if not specifies the default canvas will be resized.

#### cursor
`cursor(cursorType: Cursor): void`
Function changes the cursor while hover over the canvas.
Available cursor types: 'default', 'auto', 'crosshair', 'pointer', 'move', 'eresize', 'neresize', 'nwresize', 'nresize', 'seresize', 'swresize', 'sresize', 'wresize', 'text', 'wait', 'help', 'progress', 'copy', 'alias', 'ctxmenu', 'cell', 'notallowed', 'colresize', 'rowresize', 'nodrop', 'verticaltext', 'allscroll', 'neswresize', 'nwseresize', 'nsresize', 'ewresize', 'none'.
Example:

```ts
if (mouse.x > width / 2) {
    cursor(Cursor.crosshair);
} else {
    cursor(Cursor.pointer);
}
```

#### Keyboard
Class with the following properties:
- `keyIsPressed: boolean`
- `altIsPressed: boolean`
- `shiftIsPressed: boolean`
- `ctrlIsPressed: boolean`
- `keyPressed: string | null` (i.e. 'Shift')

and with the following functions:
- `keyDown: (key: string) => void`
- `keyUp: (key: string) => void`

By default these functions do nothing. You can redefine them inside [events](#Principles) function.

#### Mouse
Class with the following prosperities:
- `isPressed: boolean`
- `x` --- current position on *x* axis.
- `y` --- current position on *y* axis.
- `px` --- previous position on *x* axis.
- `py` --- previous position on *y* axis.

and with the following functions:
- `wheel: (e: MouseWheelEvent) => void`
- `‌down: () => void`
- `up: () => void`
- `click: () => void`
- `dbClick: () => void`

By default these functions do nothing. You can redefine them inside [events](#Principles) function.

#### AnimationCtrl
Class with the following properties:
- `fps: number` --- frames per second.
- `currentFrame: number` --- current animation frame number.
- `isAnimating: boolean` --- can be used to check if animation is running.

and with the following functions:
- `start: () => void` --- starts the animation.
- `stop: () => void` --- stops the animation and reset the `currentFrame` property.

#### translate
`translate(x: number, y: number): void`
Function moves the canvas origin by `x` pixels in horizontal axis, and by `y` pixels in vertical axis.

#### rotate
`rotate(angle: number): void`
Function rotates the canvas clockwise by specified `angle` in radians. Canvas origin is used as a pivot point.

#### scale
`scale(x: number, y: number): void`
Function changes the canvas unit on horizontal and vertical axis.
Example:
```ts
scale(1, 2);  // from now everything on 'y' axis is doubled
```

#### staticDrawing
`staticDrawing(): void`
If this function is called inside the **setup** function, the **draw** function will be executed only once.

#### save
`save(): void`
This function saves the basic canvas attributes: stroke, fill, strokeWidth, strokeCup, strokeJoin, dashLine, shadow, font and textAlign.

#### restore
`restore(): void`
This function restores previously saved canvas attributes with the **save** function.

#### clear
`clear(): void`
Function erases entire canvas content.

#### background
`background(...args: any[]): void`
Function covers entire canvas with the specified [color](#Colors).

#### stroke
`stroke(...args: any[]): void`
Function sets the [color](#Colors) and opacity of the stroke. The second argument (number between 0 and 1) is optional. By default the stroke is fully opaque.

#### strokeWidth
`strokeWidth(size: number): void`
Function sets the stroke width in pixels.

#### noStroke
`noStroke(): void`
After function is called, the stroke is not drawn.

#### strokeCup
`strokeCup(style: StrokeCupStyle): void`
This function sets the cup style for the stroke. Available styles: butt, round, square.
Example:
```ts
strokeCup(StrokeCupStyle.square);
```

#### strokeJoin
`strokeJoin(style: JoinStyle, miterValue: number = 10): void`
This function sets the join style for the stroke. Available styles: bevel, round, miter.
Example:
```ts
strokeCup(JoinStyle.round);
```

#### dashLine
`dashLine(line: number, space: number, offset: number = 0): void`
This function changes the stroke style from solid to dashed. It takes as arguments the line length, space length, and optionally the offset.

#### solidLine
`solidLine(): void`
This function restores the solid style of the stroke.

#### fill
`fill(...args: any[]): void`
Function sets the [color](#Colors) and opacity of the shapes' fill. The second argument (number between 0 and 1) is optional. By default the fill is fully opaque.

#### noFill
`noFill(): void`
After function is called, the fill is not drawn.

#### shadow
`shadow(level: number, offsetX: number, offsetY: number, ...color: any[]): void`
Function defines shadow under the drawing shapes.

#### point
`point(x: number, y: number): void`
Function draws point on the canvas at `x` and `y` coordinates --- a square 1px by 1px.

#### line
`line(x1: number, y1: number, x2: number, y2: number): void`
Function draws a straight line from point `(x1, y1)` to point `(x2, y2)`.

#### arc
`arc(x: number, y: number, r: number, startAngle: number, endAngle: number, anticlockwise?: boolean): void`
Function draws an arc on the canvas. Center of the arc is at coordinates `x` and `y`. The `r` defines the radius, `startAngle` and `endAngle` define start and end angle. The arc is drawn clockwise by default.

#### circle
`circle(x: number, y: number, r: number): void`
Function draws a circle on the canvas at coordinates `x` and `y`. The `r` defines the radius.

#### ellipse
`ellipse(x: number, y: number, r1: number, r2: number, angle: number = 0): void`
Function draws an ellipse at coordinates `x` and `y`. The `r1` defines the radius on horizontal axis, and `r2` defines the radius on vertical axis. The `angle` parameter is optional and defines inclination of the ellipse.

#### ring
`ring(x: number, y: number, r1: number, r2: number, startAngle: number = 0, endAngle: number = TWO_PI): void`
Function draws a ring on the canvas. Center of the arc is at coordinates `x` and `y`. The `r1` defines inner radius, `r2` outer radius, `startAngle` and `endAngle` define start and end angle. The ring is drawn clockwise.

#### rect
`rect(x: number, y: number, w: number, h: number, r: number = 0): void`
The function draws a rectangle on the canvas. `x` and `y` defines  position of the top left corner. `w` and `h` defines width and the height of the rectangle.

#### star
`star(x: number, y: number, r1: number, r2: number, n: number = 5): void`
The function draws a star on the canvas. `x` and `y` defines  the center of the star. The `r1` defines inner radius, `r2` outer radius. By default the five-pointed star is drawn. This can be changed by the last argument `n`.

#### polygon
`polygon(x: number, y: number, r: number, n: number = 5): void`
The function draws a polygon on the canvas. `x` and `y` defines  the center of the polygon. The `r` defines its radius. By default the five-sided polygon is drawn. This can be changed by the last argument `n`.

#### spline
`spline(pts: number[], tension: number = 0.5, closed: boolean = false): void`
Function draws a spline through the the points `[x1, y1, x2, y2, ..., xn, yn]`. The `tension` parameter defines the tension of the spline. If you want to draw a closed spline, you have to call this function with all three arguments.
Example:
```ts
spline([50, 75, 100, 200, 300, 50], 0.5, true);
```

#### bezier
`bezier(x1: number, y1: number, cp1x: number, cp1y: number, cp2x: number, cp2y: number, x2: number, y2: number): void`
Function draws a bezier curve on the canvas where `x1` and `y1` defines position of the start point, `x2` and `y2` defines position of the end point, and `cp...` positions of the control points.

#### beginShape
`beginShape(x: number, y: number): void`
Function initiates the drawing of the custom shape, and moves the drawing position to point defied by `x` and `y`.

#### endShape
`endShape(): void`
Function commits the drawn shape.

#### closeShape
`closeShape(): void`
Function closes the current path and commit the drawn shape.

#### moveTo
`moveTo(x: number, y: number): void`
Function moves the current path point without drawing a line.

#### lineTo
`lineTo(x: number, y: number): void`
Function draws a straight line from the current path point to the position defined by `x` and `y`.

#### bezierTo
`bezierTo(cp1x: number, cp1y: number, cp2x: number, cp2y: number, x: number, y: number): void`
Function draws a bezier curve from the current path point to the point defined by `x` and `y`. `cp...` define positions of the control points.

#### quadraticTo
`quadraticTo(cpx: number, cpy: number, x: number, y: number): void`
Function draws a quadratic curve from the current path point to the point defined by `x` and `y`. `cpx` and `cpy` define positions of the control point.

#### blend
`blend(color1: string, color2: string, proportion: number): string`
Function blends two color together with defined `proportion` --- the number between 0 and 1. Function return blended color.
This function accepts the color arguments only as as string in HEX code without opacity value.
Example:
```ts
blend('#567F98', '#000000', 0.5);  // as string in HEX code
```

#### randomColor
`randomColor(): string`
Function returns randomly generated color.

#### placeImage
`placeImage(img: any, x: number, y: number, origin: ImgOrigin, w?: number, h?: number): void`
Function places an image (previously loaded with the [**loadAssets**](#Principles) function) on the canvas at `x` and `y` coordinates. `origin` defines the anchor position of the image.
- `ImgOrigin.lb` --- left bottom
- `ImgOrigin.rb` --- right bottom
- `ImgOrigin.cb` --- center bottom
- `ImgOrigin.lt` --- left top
- `ImgOrigin.rt` --- right top
- `ImgOrigin.ct` --- center top
- `ImgOrigin.lc` --- left center
- `ImgOrigin.rc` --- right center
- `ImgOrigin.cc` --- center center

Arguments `w` and `h` are optional, if there is a need to change the default image dimensions.
Example:
```ts
placeImage(assets.logo, x, y, ImgOrigin.cc, 100, 100);
```

#### text
`text(text: string, x: number, y: number): void`
Function place a `text` at coordinates `x` and `y`.

#### textSize
`textSize(size?: number): void | number`
Function changes the size of the text if called with `size` argument. If function is called without an argument, it returns the current text size.

#### textWidth
`textWidth(text: string): number`
Function returns the width of the text in pixels. Use only with the single line of text.

#### textDim
`textDim(text: string): {w: number, h: number}`
Function returns an object with the text dimensions.

#### textAlign
`textAlign(h: TextAlign, v?: TextBaseline): void`
Function defines an alignment of the text.
*TextAlign*
- `TextAlign.left`
- `TextAlign.right`
- `TextAlign.center`
- `TextAlign.start`
- `TextAlign.end`

*TextBaseline*
- `TextBaseline.top`
- `TextBaseline.hanging`
- `TextBaseline.middle`
- `TextBaseline.alphabetic`
- `TextBaseline.ideographic`
- `TextBaseline.bottom`

#### fontStyle
`fontStyle(style?: string): void | string`
Function sets the style of the font according to the *CSS property*.
Example:
```ts
fontStyle('small-caps oblique');
```

#### fontWeight
`fontWeight(weight?: string): void | string`
Function changes the font weight if called with `weight` argument. If function is called without an argument, it returns the current font weight.

#### fontFamily
`fontFamily(family?: string): void | string`
Function changes the font family if called with `family` argument. If function is called without an argument, it returns the current font family.
Example:
```ts
fontFamily('Courier New');
```

#### lineHeight
`lineHeight(height?: number): void | number`
Function checks or sets the line height for multiline text. The default value is `1.1`

#### textOnArc
`textOnArc(text: string, x: number, y: number, r: number, startAngle: number, align: TextAlign = TextAlign.center, outside: boolean = true, inward: boolean = true, kerning: number = 0): number`
Function places the `text` on arc and return an angle in radians at which the text takes on the arc.
Example:
```ts
let a = textOnArc('First text', 200, 200, 130, -HALF_PI, TextAlign.left);
textOnArc(' * Second text', 200, 200, 130, -HALF_PI + a, TextAlign.left);
```

#### number2str
`number2str(x: number, radix: number = 10): string`
Function convert number to string.

#### thousandSep
`thousandSep(x: number, sep: string): string`
Function adds the thousand separator to the number.

#### deg2rad
`deg2rad(v: number): number`
Function converts degrees to radians.

#### int
`int(s: string, radix: number = 10): number`
Function converts string to integer.

#### str
Function converts its argument to string.

#### mm2px
`mm2px(v: number): number`
Function converts millimeters to pixels.

#### px2mm
`px2mm(v: number): number`
Function converts pixels to millimeters.

#### hexStr
`hexStr(v: number): string`
Function converts number between 0 and 255 to HEX string.

#### svg2img
`svg2img(svg: string): HTMLImageElement`
Function converts SVG text into HTMLImageElement.

#### disc
`dist(x1: number, y1: number, x2: number, y2: number): number`
Function returns the distance in pixels between point `(x1, y1)` and `(x2, y2)`.

#### round
`round(x: number, decimal?: number): number`
Function returns rounded argument `x`. Argument `decimal` is optional and defines number of decimal places.

#### round2str
`round2str(x: number, decimal: number): string`
Function returns rounded argument `x` as a string. Argument `decimal` is optional and defines number of decimal places. Trailing zeros are preserved.

#### constrain
`constrain(v: number, l1: number, l2: number): number`
Function returns a number constrained to the limits specified by `l1` and `l2`.

#### sq
`sq(v: number): number`
Function returns a square of the value.

#### max
`max(numbers: number[]): number`
Function returns maximum value from the array of numbers.

#### min
`min(numbers: number[]): number`
Function returns minimum value from the array of numbers.

#### sum
`sum(numbers: number[]): number`
Function returns a sum of all elements in the array of numbers.

#### avg
`avg(numbers: number[]): number`
Function returns average value from the array of numbers.

#### centile
`function centile(data: number[], c: number): number`
Function returns centile from array of numbers.
Example:
```ts
centile([1, 3, 4, 5, 7, 7, 8, 9, 10], 90);
// returns a value on 90th percentile
``` 

#### revCentile
`revCentile(data: number[], n: number): number`
Function returns percentile on witch specific number (`n`) is in the array of numbers.

#### iqr
`iqr(data: number[]): number`
Function returns a difference between 75th and 25th centile.

#### dataRange
`dataRange(data: number[]): number`
Function returns the difference between maximum and minimum value from the array.

#### stdDev
`stdDev(data: number[], method: SDevMethod = SDevMethod.sample): number`
Function returns a standard deviation based on specified method: `SDevMethod.sample` (default) or `SDevMethod.population`.

#### randomInt
`randomInt(a: number, b: number): number`
function returns an integer number between `a` and `b` (incl. border values).

#### choose
`choose(items: any[]): any`
Function returns randomly chosen element from an array.

#### random
`function random(...args: number[]): number`
Function --- if called with arguments `random(a, b)` --- returns a random number between `a` and `b`. If called without arguments, returns random number between 0 and 1.

#### shuffle
`shuffle(items: any[]): void`
Function shuffle the array in place.

#### unique
`unique(items: any[]): any[]`
Function returns sorted array of unique array elements.

#### fibonacci
`fibonacci(n: number): number[]`
Function returns an array of Fibonacci numbers. `n` defines length of the array.

#### linearScale
`linearScale(dataMin: number, dataMax: number, resultMin: number, resultMax: number): (x: number) => number`
Function returns function which maps number on the linear scale.
Example:
```ts
let scale = linearScale(0, 8000, 0, 200);
prnt(scale(6230)); // prints in console 155.75
```

#### ordinalScale
`ordinalScale(d: any[], padding: number, resultMin: number, resultMax: number): (x: number) => number`
Function returns function which maps number on the ordinar scale.
Example:
```ts
let months = ['1Q', '2Q', '3Q', '4Q'];
let scale = ordinalScale(months, 10, 0, 200);
prnt(scale(3)); // prints in console 190 (3 is the index of the fourth element)
```
### Vector
`Vector(x: number, y: number)`
Class with the following properties:
- `x` --- horizontal coordinate
- `y` --- vertical coordinate
- `direction` --- vector direction
- `magnitude` --- vector magnitude
and the following functions to work with vectors:
- `set(x: number, y: number)` --- changes the `x` and `y` coordinates.
- `copy(): Vector` --- function returns a copy of the `Vector` object.
- `add(v: Vector): Vector` --- function add the vector `v` and returns as a new `Vector`
- `addInPlace(v: Vector): void` - function add the vector `v` in place.
- `sub(v: Vector): Vector` --- function subtract the vector `v` and returns as a new `Vector`
- `subInPlace(v: Vector): void` --- function subtract the vector `v` in place
- `mult(s: number): Vector` --- function multiply the vector by scalar `s` and returns as a new `Vector`
- `multInPlace(s: number): void` --- function multiply the vector by scalar `s` in place.
- `div(s: number): Vector` --- function divide the vector by scalar `s` and returns as a new `Vector`
- `divInPlace(s: number): void` --- function divide the vector by scalar `s` in place.
- `dot(v: Vector): number` --- function returns the dot product of two vectors.
- `norm(): Vector` --- function normalize the vector and return as a new one.
- `normInPlace(): void` --- function normalize the vector in place.
- `limit(limitScalar: number` --- function limits the vector magnitude.

### Noise
`Noise(min: number, max: number, noiseRange: number)`
Class is used to generate a random numbers which are within specified range to the previously generated number.
`noiseRange` is a number between 0 and 1.
Example:
```ts
let noise = new Noise(20, 80, 0.15);
let numbers: number[] = [];
for (let i = 0; 100; i++) {
    numbers.push(noise.value);
    // or noise.intValue if you want to generate integers
}
``` 
