+++
title = "Recreating the Marvel Intro with Python and Nuke"
date = 2018-12-10T15:07:59+05:30
tags = ["nuke", "python", "marvel", "vfx", "programming"]
categories = ["cool-stuff","python"]
+++

------

Let me start this one with a story. 

Once there was a kid who loved to play games, after a while, he wanted to make games of his own and tada a programmer was born. 

End of the story. 

Wasn't that a pretty lame one? It is the most common story of anyone who loves to code, well I hope you are not one among the people who chose to code just because the job openings looked delicious. Anyway let's continue, I always wanted to make a game of my own when I was in school and since I was a loner( at that time) I had to do everything myself, from designing the assets to writing code. Honestly, you don't expect a full blown AAA quality game from a high school kid who just started out but at least it made me learn something which changed my focus from programming to computer graphics, [Blender](https://www.blender.org/), an open source beast. Of course, setting up a development environment in Windows was difficult for a 7th-grade kid but playing with Blender was easy though making something cool with it was not. Anyways fast forward some years, I got to learn about multiple Visual Effects packages, mostly proprietary ones and a couple of steps which my fingers picked up while dancing over the keyboard.

**PS** : *The main content begins here*

Half a year ago, something struck my mind, I had a fever of creating the old marvel intro, why? I don't know, I am not even a great fan of Marvel Comics either but probably because it looked easy and eye-catchy. I set out to look for how-to-s and all I find is a bunch of After Effects tutorials, I know After Effects is the go-to program for doing that kind of Motion Graphics but being a Linux evangelist, I was not ready to give up so easily, Adobe you suck. ( Photoshop is nice but still )

BlackMagicDesign's [Fusion](https://www.blackmagicdesign.com/in/products/fusion/) 9 to rescue, it was easy to recreate the effect on Fusion but I had to do the same thing with a lot of pictures, given that a picture stays on the screen for around 3 to 4 frames and there were 25 frames a second, end of the day, a lot of work for just 3 seconds. Fortunately Fusion supported Python 2, Python 3 and Lua, was free too but unfortunately it can't find either of the python versions on my system and I was stuck with Lua, a scripting language which I don't know why decided to start its array indexes from 1, left me wondering for a night why my script was failing. Anyway, it was easy to make one thanks to the scripting manual which came with Fusion and the task being not so daunting. [Here](https://github.com/hellozee/scripts/blob/master/marvel.lua) is the final script which I wrote,

```lua
--[[
    Author: Kuntal Majumder
    Description: Lua script to create an animation sequence with pictures,
    similar to Marvel's old intro.
--]]

--[[ Getting the List of Loaders, if there are multiple of them,
     select the specific loaders and replace false with true --]]
loaderList = comp:GetToolList(false,"Loader")

--[[ Deselecting everything --]]
flow = comp.CurrentFrame.FlowView
flow:Select()

numberOfPictures = 0

for i,loader in ipairs(loaderList) do
    transform = comp:AddTool("Transform")
    
    --[[ Adding high quality motion blur --]]
    transform.MotionBlur = 1
    transform.Quality = 10    
    
    --[[ Adding the animation to the pictures --]]
    transform:AddModifier("Center","XYPath")
    transform.Center[0] = {0.5,1.5}
    transform.Center[3] = {0.5,0.5}
    
    --[[ Offsetting every picture by 4 frames compared to last picture --]]
    timespeed = comp:AddTool("TimeSpeed")
    timespeed.Delay = (i-1) * 4
    
    --[[ Connecting respective inputs and outputs --]]
    timespeed.Input = transform.Output
    transform.Input = loader.Output
    
    --[[ Arranging the merges properly --]]
    if i > 2 then
        --[[ One merge node is already there in the node graph which was
                     selected in the last iteration, so we connect its output
                     with the background of the current --]]
        table = comp:GetToolList(true,"Merge")
        prevMerge = table[1]
        flow:Select()
        merge = comp:AddTool("Merge")
        merge.Foreground = timespeed.Output
        merge.Background = prevMerge.Output
        flow:Select(merge, true)
    elseif i > 1 then
        --[[ Required nodes are added to the second picture so make new
                     merge node and connect the first picture's timespeed to it
                     which was selected last time --]]
        merge = comp:AddTool("Merge")
        table = comp:GetToolList(true,"TimeSpeed")
        prevTimeSpeed = table[1]
        merge.Foreground = timespeed.Output
        merge.Background = prevTimeSpeed.Output
        flow:Select(merge, true)
    else
        --[[ Required nodes added to the first picture, so no merges
                     are created, instead the timespeed node is selected --]]
        flow:Select()
        flow:Select(timespeed, true)
    end
    numberOfPictures = numberOfPictures + 1
end

--[[ Getting the last Merge node --]]
table = comp:GetToolList(true,"Merge")
toSaveMerge = table[1]

--[[ Adding a Saver node --]]
comp:Lock()
saver = comp:AddTool("Saver")
comp:Unlock()
saver.Input = toSaveMerge.Output

--[[ If the file location is predetermined we can enter the file location
     into the saver and render the whole comp instantly --]]

--[[
saver.Clip = '<file location>'
comp:Render(false,0,numberOfPictures * 4, 1,1)
--]]

```

The script is really simple all it does it get all the image loaders from the node graph and attaches a `Transform` node which does the animation, adds `TimeSpeed` node which adds an offset of 4 seconds to the image based on its position and merges it with the rest. Tada, you have a marvel like animation ready in seconds. 

A couple days ago I landed at [The Foundry'](https://www.foundry.com/)s website which said they were offering [Nuke](https://www.foundry.com/products/nuke) for free to students up to a year. I have tried Nuke earlier but it was pretty costly and the non-commercial version was pretty limiting for learning but this time, I got a full-fledged copy of Nuke for me, thanks to The Foundry. And the first thing I did with it was to recreate the Marvel Intro animation and cause Nuke supported Python, it was really easy for me to do though I am not the best guy in the town when it comes to writing python, probably the worst one but a couple of extra control statements won't hurt the performance (I am not writing another CRUD app with Django at least). So with `Py-27` (smile if you get the reference), I went to fight the battle, a little did I know it will be over by a couple of hours. Thus the next day I went a mile ahead and made added a couple of more things, voila you have a robust & organized script which could generate flawless Marvel Intros from any set of images you throw at it. [Here](https://github.com/hellozee/nuke-scripts/blob/master/marvel.py) is the final version:

```python
"""
    Filename: marvel.py
    Author: Kuntal Majumder
"""

import nuke

def get_transform(height):
    """The transform node does the animation of dropping the image"""
    transform = nuke.nodes.Transform()
    transform['translate'].setAnimated()
    transform['translate'].setValue([0,height],time=1)
    transform['translate'].setValue([0,0],time=3)
    return transform

def get_reformat():
    """Resizes the image according to the project settings"""
    reformat = nuke.nodes.Reformat()
    reformat['resize'].setValue('fill')
    return reformat

def get_timeoffset(pos):
    """Shifts the image to the given position in the timeline"""
    timeoffset = nuke.nodes.TimeOffset()
    timeoffset['time_offset'].setValue(pos*4)
    return timeoffset

def manipulate_node(filename,pos):
    """The man who generates the node graph"""
    read = nuke.nodes.Read(file=filename,auto_alpha=True,premultiplied=True)
    reformat = get_reformat()
    reformat.setInput(0,read)

    """Crops the node if it is larger to avoid residue while it is off the screen"""
    crop = nuke.nodes.Crop()
    crop.setInput(0,reformat)
    transform = get_transform(read['format'].value().height())
    transform.setInput(0,crop)
    timeoffset = get_timeoffset(pos)
    timeoffset.setInput(0,transform)
    return timeoffset
    
def main():
    images = nuke.getFilename("Select Images",'*.png *.jpg *.jpeg',multiple=True)
    
    length = len(images)
    if length < 2 :
        nuke.warning("At least 2 images required to create the effect")
        nuke.message("At least 2 images required to create the effect")
        return

    merge = manipulate_node(images[0],0)
    i = 1
    
    while i < length:
        node = manipulate_node(images[i],i)
        merge = nuke.nodes.Merge(inputs=[merge, node])
        i += 1
    
    # A generic touch to make it similar to the original one,
    # a trick which really makes difference, have to play with
    # the shutter samples for more accuracy
    motionblur = nuke.nodes.MotionBlur()
    motionblur.setInput(0,merge)
    
    # For keeping track of the node graph if you have too many pictures
    motionblur.setSelected(True)

if __name__ == "__main__":
    main()

```

This is an upgraded version of previous script which I wrote for Fusion, the script asks for selecting the pictures with a file dialog and adjusts the size of the picture according to the project settings before attaching the `Transform` and `TimeOffset` nodes.

And to impress you all, the final output of it:

![Marvel Intro](https://media.giphy.com/media/dJQyGQcoy5E8NrXcMt/giphy.gif)

`:wq` for today
