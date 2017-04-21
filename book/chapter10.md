#Chapter 10 - Libraries

A library is code that everyone can use to add certain functionality to their project.

Let's try out a library. We're going to use *tick* by *rxi*. You can find the library on [GitHub](https://github.com/rxi/tick).

Click on ``tick.lua`` and then on Raw, and [copy the code](https://raw.githubusercontent.com/rxi/tick/master/tick.lua).

Go to your text-editor, create a new file called ``tick.lua`` and paste the code.

Now we have to follow the instructions on the GitHub page. First we have to require it.

```lua
function love.load()
	tick = require "tick"
end
```

Notice how ``require`` doesn't have parantheses (). This is because when you only pass 1 argument, you don't have to use them. Now I recommend you still do use them for any other function, but with ``require`` it's common to leave them out. But in the end, it doesn't even matter.

Next we have to put tick.update(dt) in our updater.

```lua
function love.update(dt)
	tick.update(dt)
end
```

And now we're ready to start using the library. Let's make it so that a rectangle will be drawn after 2 seconds.

```lua
function love.load()
	tick = require "tick"

	--Create a boolean
	drawRectangle = false

	--The first argument is a function
	--The second argument is the time it takes to call the function
	tick.delay(function () drawRectangle = true end ,	2)
end


function love.draw()
	--if drawRectangle is true then draw a rectangle
	if drawRectangle then
		love.graphics.rectangle("fill", 100, 100, 300, 200)
	end
end


```
Did we just pass a function as an argument? Sure, why not? A function is a type of variable after all. As you can see, with this library we can put a delay on things. And like that there are tons of libraries with all kind of functionality.

Don't feel guilty for using a library. Why reinvent the wheel? That is, unless you are interested in learning it. I personally use about 10 libraries in my projects. They provide functionality that I don't understand how to make myself, and I'm simply not interested in learning it.

Libraries aren't magic. It's all code that you and I could've written as well. We'll create a library in the future to get a better understanding about them.

___

##Standard libraries

Lua has built-in libraries. These are called *Standard Libraries*. They are the functions that are build into Lua. ``print``, for example, is part of the standard library. And so is ``table.insert`` and ``table.remove``.

One important standard library we haven't looked at yet is the *math library*. It provides math functions, which can be very useful when making a game.

For example, ``math.random`` gives us a random number. Let's use it to place a rectangle on a random position whenever you press the spacebar.

```lua
function love.load()
	x = 30
	y = 50
end


function love.draw()
	love.graphics.rectangle("line", x, y, 100, 100)
end


function love.keypressed(key)
	--If space is pressed then..
	if key == "space" then
		--x and y become a random number between 100 and 500
		x = math.random(100, 500)
		y = math.random(100, 500)
	end
end
```

Now that we understand what libraries are, we can start using a class library.

___

##TL;DR
Libraries are code that gives us functionality. Anyone can make a library. Lua also has build-in libraries which we call the Standard Library.