# Chapter 1 - Installation

___

*Chapter 2 and 3 can be done without any installation. You can use [repl.it](https://repl.it/languages/lua) as an alternative if you don't feel like installing software right away. But be sure to read the **A few more things** paragraph at the bottom.*

___

## LÖVE

Go to [love2d.org](https://www.love2d.org/).

You should download either the 32-bit or the 64-bit **installer**. This depends on your system type. If you don't know your system type, just go with 32-bit.

![](/images/book/1/download_love.png)

Open the installer. Click on *Next*. Click on *I agree*. Now you can decide where you install LÖVE. It doesn't matter where you install LÖVE, but make sure you remember the location because we need it in a moment. This folder will be referred to as the *Installation Folder*.

My installation folder will be `C:/Program Files/LOVE`.

Click on *Next*. Click on *Install*.

When LÖVE is done installing, click on *Finish*.

___

## Code editor

Now we need to install a text editor. We're going to use ZeroBrane Studio in this tutorial.

If you use **Visual Studio Code**, check out the [extra chapter](bonus/vscode) to learn how to run LÖVE in Visual Studio Code.

Go to [studio.zerobrane.com](https://studio.zerobrane.com/), and click on "Download".

![](/images/book/1/download_brane.png)

Here you get the option to donate to ZeroBrane Studio. If you don't want to donate click on ["Take me to the download page this time"](https://studio.zerobrane.com/download?not-this-time),

Open the installer, and install ZeroBrane Studio in your preferred folder.

![](/images/book/1/install_brane.png)

When ZeroBrane Studio is done installing, open it.

Now we need to make a Project Folder. Open you file explorer and create a folder wherever you like, and name it whatever you want. In ZeroBrane Studio, click on the "Select Project Folder" icon, and select the folder you just created.

![](/images/book/1/project_brane.png)


In ZeroBrane Studio, create a new file. `File` -> `New`, or use the shortcut `Ctrl + N`. 

Inside this file, write the following code:
```lua
function love.draw()
	love.graphics.print("Hello World!", 100, 100)
end
```

Go to `File` -> `Save`, or use the shortcut `Ctrl + S`. Save the file as `main.lua`.

Go to `Project` -> `Lua Interpreter` and select `LÖVE`.

Now when you press the F6, a window should open with the text "Hello World!". Congratulations, you're ready to start learning LÖVE. Whenever I tell you to *run the game* or *run the code* I'm telling you to press F6 to execute LÖVE.

In case nothing happens and the following text shows up: *Can't find love2d executable in any of the following folders*, you installed LÖVE somewhere where ZeroBrane Studio can't find it. Go to `Edit` -> `Preferrences` -> `Settings: User`. Put in the following:

```lua
path.love2d = 'C:/path/to/love.exe'
```

And replace `'C:/path/to/love.exe'` with the path to where you installed LÖVE. Make sure to use frontslashes (/).

___

## A few more things

Did you copy/paste the example code? I encourage you to type the code I show you yourself. That might seem like a lot of extra work, but by doing so it will help you memorize everything a lot better.

The one thing you don't need to type yourself are comments.

```lua
-- This line is a comment. This is not code.
-- The next line is code:

print(123)

--Output: 123
```

Every line starting with 2 minus-signs (--) is a *comment*. The computer ignores it, meaning we can type anything we want without getting an error. I can use comments to explain certain code better. When typing over the code you don't have to copy the comments.

With `print` we can send information to our *Output console*. This is the box at the bottom of our editor. **When you close the game**, it should say the text "123". I add the text `--Output:` to show you the expected output. This is not to be confused with `love.graphics.print`.

If you put the following code at the top of your `main.lua` you will see the prints right away. How this works is not important, basically you turn off that the program should wait to be closed before showing the prints.

```lua
io.stdout:setvbuf("no")
```

___

## Alternative text editors

* [Visual Studio Code](https://code.visualstudio.com/)
* [Sublime Text](https://love2d.org/wiki/Sublime_Text)
* [Atom](https://love2d.org/wiki/Atom)