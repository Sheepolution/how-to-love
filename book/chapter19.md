# Chapter 19 - Audio

We're going to add audio. This chapter is very short. That's because just like with a lot of things, the LÖVE API makes it very easy for us to add audio to the game.

Download these two files that we will be using in this tutorial:

[*sfx.ogg*](/images/book/19/sfx.ogg) and [*song.ogg*](/images/book/19/song.ogg)

Let's start with the song and make it so that it loops endlessly.
First we need to create the audio. We call this a *source* (the source of the audio). We can create the source with `love.audio.newSource(path)`. This function takes two arguments. First is the path to the file, second is what type of source it is. This can be either `"static"` or `"stream"`. Let me quote the LÖVE wiki: "A good rule of thumb is to use stream for music files and static for all short sound effects. Basically, you want to avoid loading large files at once."

So in our case we want to use `"stream"`, since it's a song.

```lua
function love.load()
    song = love.audio.newSource("path/to/song.ogg", "stream")
end
```

Next we want to play it. There are two ways to do it.

```lua
function love.load()
    song = love.audio.newSource("path/to/song.ogg", "stream")
    -- method 1
    love.audio.play(song)
    --method 2
    song:play()
end
```

There isn't really a difference between the two, and if there is it's not a difference that you will notice. So use whatever you prefer. I prefer the second method.

When you run the game the song should now play. But it doesn't loop. How can we fix this? I can tell you, but you should learn how to find these kind of things yourself. First, let's go to wiki page of the [Source](http://love2d.org/wiki/Source) object. Now we need to look for something that might help us loop the audio. Perhaps press Ctrl + F to search on the page, and then type "loop". 

Source:setLooping	Sets whether the Source should loop.

Got it! 

```lua
function love.load()
    song = love.audio.newSource("path/to/song.ogg", "stream")
    song:setLooping(true)
    song:play()
end
```

Okay nice, now we got looping background music. Next we want to add a sound effect. Let's make it so that the sound effect is played every time you press Space. We start with creating the new source.

```lua
function love.load()
    song = love.audio.newSource("path/to/song.ogg", "stream")
    song:setLooping(true)
    song:play()
    
    -- sfx is short for 'sound effect', or at least I use it like that.
    sfx = love.audio.newSource("sfx.ogg", "static")
end
```

Next we add the keypressed callback, and make the sound effect play every time we press "space".

```lua
function love.keypressed(key)
    if key == "space" then
        sfx:play()
    end
end
```

And we're done. Like I said, there isn't much to say about audio, and everything you want to learn you can easily look up yourself in the API documentation. For example, how to [set the volume](http://love2d.org/wiki/Source:setVolume), how to make the source [pause](http://love2d.org/wiki/Source:pause) or how to get the source's [position](http://love2d.org/wiki/Source:tell).

___

## Summary
The LÖVE API makes it very easy to add audio. We call an audio object a Source. Often we can figure out how to do something by looking through the API documentation.