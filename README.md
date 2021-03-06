Scale and align an HTML element in the browser
===============================================
Use the function `scaleToWindow` to scale an HTML element to
the maximum size of the browser's window. `scaleToWindow` will also align the element for the best vertical or horizontal fit inside the browser window. For example, if you have an element that's wider than it is tall, it will be centered vertically inside the browser. If the element is taller than it is wide, it will be centered horizontally.

![Alignment](screenShot.png)

Here's how to use `scaleToWindow`:
```js
scaleToWindow(anyElement, borderColor);
```
(If you are using [Pixi](https://github.com/pixijs/pixi.js), supply the `renderer.view` as the element.)
The optional second argument lets you set the color of the browser's background that borders the element. You can supply any RGB, HSLA or Hexadecimal color value, as well as the any HTML color string, like “blue” or “red”. (If you don't supply this optional color, the border will be set to a neutral dark gray: #2C3539.)

The `scaleToWindow` function also returns the `scale` value that the
element is scaled to. You can find it like this:
```js
var scale = scaleToWindow(renderer.view);
```
This will give you a number, like 1.98046875, which tells you the
ratio by which the element was scaled. This might be an important value
to know if you need to convert browser pixel coordinates to the scaled
pixel values of the element. For example, if you have a `pointer`
object which tracks the mouse's position in the browser, you might
need to convert those pixel positions to the scaled element coordinates
to find out if the mouse is touching something in the element. Some general code like this will do the trick:
```js
pointer.x = pointer.x / scale;
pointer.y = pointer.y / scale;
```
Optionally, you might also want the element to rescale itself every
time the size of the browser window is changed. If that’s the case,
call `scaleToWindow` inside a window event listener:
```js
window.addEventListener("resize", function(event){ 
  scaleToWindow(anyelementElement);
});
```
For the best effect, make sure that you set the browser's default margins and
padding to `0` on all HTML elements. If you don't do this, most
browsers will add some padding around the element borders.  This bit of CSS will do the
trick:
```
<style>* {padding: 0; margin: 0}</style>
```
If you prefer, you can add this CSS style using JavaScript in your main program
like this:
```
var newStyle = document.createElement("style");
var style = "* {padding: 0; margin: 0}";
newStyle.appendChild(document.createTextNode(style));
document.head.appendChild(newStyle);
```

