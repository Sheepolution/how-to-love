#Chapter 4 - LÖVE

##What is LÖVE?
LÖVE is what we call a *framework*. Simply said: It's a tool that makes programming things easier.

LÖVE is made with *C++* and *OpenGL*, which are both considered to be very difficult. The source code of LÖVE is very complex. But all this complex code makes creating a game a lot easier for us.

For example, with ``love.graphics.ellipse()``, we can draw an ellipse. But this is the source code behind it:

```cpp
void Graphics::ellipse(DrawMode mode, float x, float y, float a, float b, int points)
{
	float two_pi = static_cast<float>(LOVE_M_PI * 2);
	if (points <= 0) points = 1;
	float angle_shift = (two_pi / points);
	float phi = .0f;

	float *coords = new float[2 * (points + 1)];
	for (int i = 0; i < points; ++i, phi += angle_shift)
	{
		coords[2*i+0] = x + a * cosf(phi);
		coords[2*i+1] = y + b * sinf(phi);
	}

	coords[2*points+0] = coords[0];
	coords[2*points+1] = coords[1];

	polygon(mode, coords, (points + 1) * 2);

	delete[] coords;
}
```

You might not understand this code above at all, and that's exactly why we use LÖVE. It takes care of the hard parts of gameprogramming, and leaves the fun part for us.

___

##Lua

Lua is the programming language that LÖVE uses. Lua is a programming language on its own, and is not made by or for LÖVE. The creators of LÖVE simply chose Lua as the language for their framework.

So what part of what we code is LÖVE, and what is Lua? Very simple: Everything starting with ``love.`` is part of the LÖVE framework. Everything else is Lua.

These are functions part of the LÖVE framework:
```lua
love.graphics.circle("fill", 10, 10, 100, 25)
love.graphics.rectangle("line", 200, 30, 120, 100)
```

And this is simply Lua:
```lua
function test(a, b)
	return a + b
end
print(test(10, 20))
--output: 30
```
If it's still confusing to you, that's okay. It's not the most important thing right now.

___


##How does LÖVE work?

___

*You're required to have LÖVE installed at this point. Go back to [Chapter 1](1) if you haven't already.*
___

LÖVE calls 3 functions. First it calls love.load(). In here we create our variables.

After that it calls love.update() and love.draw(), repeatedly in that order.

So: love.load -> love.update -> love.draw -> love.update -> love.draw -> love.update, etc.

Behind the scenes, LÖVE calls these functions, and we to create them, and fill them with code. This is what we call a *callback*.

LÖVE is made out of *modules*, love.graphics, love.audio, love.filesystem. There are about 15 modules, and each module focusses on 1 thing. Everything that you draw is done in love.graphics. And anything with sound is done in love.audio.

For now, let's focus on love.graphics.

LÖVE has a [wiki](https://www.love2d.org/wiki/Main_Page) with an explanation for every function. Let's say we want to draw a rectangle. On the wiki we go to  [``love.graphics``](https://www.love2d.org/wiki/love.graphics), and on the page we search for "rectangle". There we find [``love.graphics.rectangle``](https://www.love2d.org/wiki/love.graphics.rectangle).

[![](/images/book/4/rectangle.png "love2d.org/wiki/love.graphics.rectangle")](https://www.love2d.org/wiki/love.graphics.rectangle)

This page tells us what this function does and what arguments it needs. The first argument is mode, and needs to be of the type DrawMode. We can click on [``DrawMode``](https://www.love2d.org/wiki/DrawMode) to get more info about this type.

[![](/images/book/4/drawmode.png "love2d.org/wiki/DrawMode")](https://www.love2d.org/wiki/DrawMode)

DrawMode is a string that is either "fill" or "line", and controls how shapes are drawn.

All following arguments are numbers.

So if we want to draw a filled rectangle, we can do the following:
```lua
function love.draw()
	love.graphics.rectangle("fill", 100, 200, 50, 80)
end
```

Now when you run the game, you'll see a filled rectangle.

___

##TL;DR
LÖVE is a tool that makes it easier for us to make games. LÖVE uses a programming language called Lua. Everything starting with ``love.`` is part of the LÖVE framework. The wiki tells us everything we need to know about how to use LÖVE.