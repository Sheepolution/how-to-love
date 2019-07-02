
# Chapter 15 - Distributing your game

___
*We use the code from the previous chapter*
___

You made a game, and you want to share it with others. You could make them install LÖVE on their computer, but that is not necassary.

First, we need to change the title and icon. For that we will use a config file.

Create a new file called conf.lua, and put in the following code

```lua
function love.conf(t)
	t.window.title = "Panda Shooter!"
	t.window.icon = "panda.png"
end
```

Save the file. Now when you run the game you'll see the game has the title "Panda Shooter!", and that the icon is the panda.

This is what the config file is for. LÖVE loads `conf.lua` before it starts the game and applies the configurations. For a full list of options check out the [wiki](https://love2d.org/wiki/Config_Files).

Now that our game has the correct title and icon, let's turn it into an executable.

First we need to package our game in a zip file. Go to the folder of your game, select all the files. Now right click, go to *Send to* and click on *Compressed (zipped) folder*. The filename is not important, but we need to change the extension to `.love` (by default `.zip`).

*Note: This part is Windows only. Go [here](https://www.love2d.org/wiki/Game_Distribution) to get info on building your game for other platforms.*

![](/images/book/15/compress.png)

**If you can't see file extensions**

Press ***Windows + pause/break***. In the upper-left corner of the new opened window click on ***Control Panel***. Now go to ***Appearance and Personalization***.

![](/images/book/15/control_panel.png)

Click on ***File Explorer options***.

![](/images/book/15/personalization.png)

A new window opens. Click on the tab ***View***. In ***Advanced options***, make sure that ***Hide extension for known filetypes*** is unchecked.

![](/images/book/15/folder_options.png)

I wrote a bat file that packages the game for you. Download [this zip file](https://drive.google.com/file/d/1xX49nDCI0UxjnwY3-h0f-kpdmHVmNqvz/view?usp=sharing), and unzip all the files in a folder.

Now move your `.love` file on top of `build.bat`. This creates a `.zip` file in the same folder. This is the file that you will want to share with people. They have to extract all the files in a folder and open the `.exe` file.

Now you need to find a place to share your game. Check out [itch.io](https://itch.io/).

For more information on building your game, check out the [LÖVE wiki page](https://www.love2d.org/wiki/Game_Distribution) for it. It also tells you how to build your game for other platforms.

___

## Castle

[Castle](https://castle.games/) is a client that allows you to easily share your LÖVE games. Check it out!

___

## Summary
With [conf.lua](https://love2d.org/wiki/Config_Files) you can configure things about your game like title and icon. Select all the files in the folder of your game, put them in a zip. Change the file's extension from `.zip` to `.love`. Download [this zip file](https://drive.google.com/file/d/1gaqhvQ9tuluml1W6GXHc4F0XPj1iSxR2/view?usp=sharing), and unzip all the files in a folder. Move your `.love` on top of `build.bat` to create a `.zip`. People will have to unzip all the files in a folder and open the `.exe` to play your game. We can also use Castle which is a client that allows us to share our LÖVE games.