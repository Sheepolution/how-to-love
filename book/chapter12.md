# Chapter 12 - Images

Creating and using images is a very easy task in LÖVE. First we need an image. I'm going to use this image:

![](/images/book/12/sheep.png)

Of course, you can use any image you like, as long as it's of the type *.png*. Make sure the image is in the same folder as your `main.lua`.

First we need to load the image, and store it in a variable. For this we will use `love.graphics.newImage(path)`. Pass the name of the image as a string as first argument. So if you have a 

```lua
function love.load()
	myImage = love.graphics.newImage("sheep.png")
end
```
You can also put your image in a subdirectory, but in that case make sure to include the whole path.

```lua
myImage = love.graphics.newImage("path/to/sheep.png")
```

Now our image is stored inside `myImage`. We can use `love.graphics.draw` to draw our image.

```lua
function love.draw()
	love.graphics.draw(myImage, 100, 100)
end
```

And that is how you draw an image.

___

## .draw() arguments

Let's take a look at all the arguments of `love.graphics.draw()`. All arguments besides the image are optional.

**image**

The image you want to draw.

**x** and **y**

The horizontal and vertical position of where you want to draw the image. 

**r**

The **r**otation (or angle). All angles in LÖVE are radians. I'll explain more about radians in another chapter.

**sx** and **sy**

The **x**-**s**cale and **y**-**s**cale. If you want to make your image twice as big you do

`love.graphics.draw(myImage, 100, 100, 0, 2, 2)`

 You can also use this to mirror an image with

`love.graphics.draw(myImage, 100, 100, 0, -1, 1)`

**ox** and **oy**

The **x**-**o**rigin and **y**-**o**rigin of the image.

By default, all the scaling and rotating is based on the top-left of the image.

![](/images/book/12/origin1.png)

This is based on the *origin* of the image. If we want to scale the image from the center, we'll have to put the origin in the center of the image.

`love.graphics.draw(myImage, 100, 100, 0, 2, 2, 39, 50)`

![](/images/book/12/origin2.png)

**kx** and **ky**

These are for shearing (which doesn't have a **k** at all so I'm not sure what to make of it).

With it you can skew images.

![](/images/book/12/shear.png)

`love.graphics.print`, which we used before to draw text, has these same arguments.

x, y, r, sx, sy, ox, oy, kx, ky 

Again, all these arguments except **image** can be left out. We call these *optional arguments*.

You can learn about LÖVE functions by reading the [API documentation](https://love2d.org/wiki/love.graphics.draw).

___

## Image object

The image that `love.graphics.newImage` returns, is actually an object. An [Image](https://love2d.org/wiki/Image) object. It has functions that we can use to edit our image, or get data about it.

For example, we can use `:getWidth()` and `:getHeight()` to get the width and height of the image. We can use this to put the origin in the center of our image.

```lua
function love.load()
    myImage = love.graphics.newImage("sheep.png")
    width = myImage:getWidth()
    height = myImage:getHeight()
end

function love.draw()
	love.graphics.draw(myImage, 100, 100, 0, 2, 2, width/2, height/2)
end
```

___

## Color

You can change in what color the image is drawn with `love.graphics.setColor(r, g, b)`. It sets the color for everything you draw, so not only images but rectangles, shapes and lines as well. It uses the [RGB-system](https://en.wikipedia.org/wiki/RGB_color_model). Although this officially ranges from 0 to 255, with LÖVE it ranges from 0 to 1. So instead of (255, 200, 40) you would use (1, 0.78, 0.15). If you only know the color using the 0-255 range, you can calculate the number you want with `number/255`. There is also the fourth argument `a` which stands for alpha and decides the transparency of everything you draw. Don't forget to set the color back to white if you don't want the color for any other draw calls. You can set the background color with `love.graphics.setBackgroundColor(r, g, b)`. Since we only want to call it once, we can call it in `love.load`.

```lua
function love.load()
    myImage = love.graphics.newImage("sheep.png")
    love.graphics.setBackgroundColor(1, 1, 1)
end

function love.draw()
	love.graphics.setColor(255/255, 200/255, 40/255, 127/255)
	love.graphics.setColor(1, 0.78, 0.15, 0.5)
	-- Or ...
	love.graphics.draw(myImage, 100, 100)
	-- Not passing an argument for alpha automatically sets it to 1 again.
	love.graphics.setColor(1, 1, 1)
	love.graphics.draw(myImage, 200, 100)
end
``` 

![](/images/book/12/color.png)

___

## Summary

We load an image with `myImage = love.graphics.newImage("path/to/image.png")`, which returns an Image object that we can store in a variable. We can pass this variable to `love.graphics.draw(myImage)` to draw the image. This function has optional arguments for the position, angle and scale of the image. An Image object has functions that you can use to get data about it. We can use `love.graphics.setColor(r, g, b)` to change in what color the image and everything else is drawn.
