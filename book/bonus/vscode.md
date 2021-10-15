# Visual Studio Code

Visual Studio Code is a code editor by Microsoft with lots of features. In this chapter we go over some extensions and tricks to optimize the editor for making LÖVE games.

[Install Visual Studio Code](https://code.visualstudio.com/)

## Extensions

Install the following extensions:

- [Lua by sumneko](https://marketplace.visualstudio.com/items?itemName=sumneko.lua)

- [Local Lua Debugger by Tom Blind](https://marketplace.visualstudio.com/items?itemName=tomblind.local-lua-debugger-vscode)

### Lua

As the marketplace says this extension gives you lots of useful features. We can also make it have LÖVE autocomplete.

Press `Ctrl + Shift + P` and look for and open `Preferences: Open Settings (JSON)`.

Add the following settings to the JSON:

```json
{
    "Lua.runtime.version": "LuaJIT",
    "Lua.diagnostics.globals": [
        "love",
    ],
    "Lua.workspace.library": [
        "${3rd}/love2d/library"
    ],
    "Lua.workspace.checkThirdParty": false,
}
```

### Local Lua Debugger

Add the folder where `love.exe` is located to your environment variables. In Windows search for `Edit the system environment variables`. At the bottom click on `Environment Variables`. In `System variables` search for and click on `Path`. Click `Edit...`. Click `New`. Type the path to the folder where your `love.exe` is located.

![Guide](/images/book/bonus/vscode/lovepath.gif)

Now we are going to add two launchers. Note that the following approach is not necessarily the *best*. This is a personal preference.

Go to Run and Debug (play button with a bug on the left). Click on `creat a launch.json file`.

Replace the contents of the new file with this:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lua-local",
      "request": "launch",
      "name": "Debug",
      "program": {
        "command": "love"
      },
      "args": [
        ".",
        "debug"
      ],
    },
    {
      "type": "lua-local",
      "request": "launch",
      "name": "Release",
      "program": {
        "command": "love"
      },
      "args": [
        ".",
      ],
    },
  ]
}
```

Add the following line at the top of your main.lua:

```lua
if arg[2] == "debug" then
    require("lldebugger").start()
end
```

You can press F5 to start the launcher. You can select which launcher you want to use in Run and Debug. You now have two ways to launch LÖVE:

- With **Debug** you can debug your game. In a Lua file click on the left of a line-number to create a *break point* (and click again to remove it). When your code is at this line the debugger will stop there, and allow you to examine variables. ![debugging](/images/book/bonus/vscode/debugging.png)
- With **Release** you don't have a debugger. The reason you keep these separated is so that you don't have to remember to remove the `lldebugger` line whenever you want to distribute the game.

We can improve the debugger by making it highlight an error when we get one. For this we will need to edit `love.errorhandler`. LÖVE catches the error to show the nice error screen, but we want it to actually throw an error.

At the bottom of `main.lua` add the following code:

```lua
local love_errorhandler = love.errhand

function love.errorhandler(msg)
	if lldebugger then
		error(msg, 2)
	else
		return love_errorhandler(msg)
	end
end
```
Now when you get an error in Debug mode Visual Studio Code will jump to the file and line of where the error occured and highlight it, along with the error message.

![error](/images/book/bonus/vscode/error.png)

You might notice that your game slows down a lot in Debug mode. Because of this I add another launcher called **Test**. Add this configuration to your `launch.json`:

```json
{
    "type": "lua-local",
    "request": "launch",
    "name": "Test",
    "program": {
        "command": "love"
    },
    "args": [
        ".",
        "test"
    ],
},
```

Change the lines where you require `lldebugger` to this:
```lua
local launch_type = arg[2]
if launch_type == "test" or launch_type == "debug" then
    require "lldebugger"

    if launch_type == "debug" then
        lldebugger.start()
    end
end
```
And add this line in your `love.errorhandler`.
```lua
local love_errorhandler = love.errhand

function love.errorhandler(msg)
	if lldebugger then
        lldebugger.start() -- Add this
		error(msg, 2)
	else
		return love_errorhandler(msg)
	end
end
```
This way you still get the highlighted error, but are not slowed down by the debug mode. You can also expand on this, like showing information. You can also expand on this, like showing debug information on screen when `launch_type == "test" or launch_type == "debug"`.

## Building

Now we want to make it easy to build our project. 

### makelove

We use the builder [makelove](https://github.com/pfirsich/makelove/).

1. Install [Python](https://www.python.org/downloads/) (if you do a custom installation make sure to install `pip`).
2. Open a terminal (e.g. Windows Powershell) and type `pip3 install makelove`.
3. In your game's folder (where you have your main.lua) create a file called `make_all.toml` and add the following:
```ini
name = "Game"
default_targets = ["win32", "win64", "macos"]
build_directory = "bin"
love_files = [
    "+*",
    "-*/.*",
]
```

### Tasks

Press `Ctrl + Shift + P` and look for and open `Task: Configure Task`. Select `Create task.json file from template`. Select `Others` (or any other, doesn't really matter). Replace the file's contents with this:
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Build LÖVE",
            "type": "process",
            "command": "makelove",
            "args": [
                "--config",
                "make_all.toml"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        },
    ]
}
```

Now in Visual Studio Code you can press `Ctrl + Shift + B` to run the task. This will create a `bin` folder, with inside folders that have `.zip` files inside of them.