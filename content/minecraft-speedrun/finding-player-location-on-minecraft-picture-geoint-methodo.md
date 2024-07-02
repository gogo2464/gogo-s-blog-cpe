---
title: "find player location in minecraft from picture"
date: 2024-06-17T12:37:42+02:00
draft: false
---

# 1 Project philosophy

In some case, speedrunners could watch a "secret" location from a specific seed on youtube video. In this case, they will need to find it to redo the speedrun method. In this tutorial, I will help you to find a speedrun location from a picture.

The target I will use will be the next below.

![image](/gogo-s-blog-cpe/minecraft-speedrun/finding-player-location-on-minecraf-picture-geoint-methodo/image.png)


This project is a geoint methodology (tutorial) to find the coordinate (x,y) from a picture. The project consist to:
- 1: find the seed of the picture
- 2: find coordinate from picture on the seed

In this tutorial we will use math principles of triangulation (we use a compass on a map get the intersection of 2 points of a specific distance) and trigonometry (math on rectangle triangles).

This method has the disadvantage from "texture rotation" to:
- 1: be more complicated and more manual than minecraft specific methods because there is no tool to do that automatically.
- 2: require some reverse engineering to have a map of the game. See [radare hack](https://gamehacking.academy/pages/5/08/).

But the geoint method to find coordinate from picture on the seed has the advantage to:
- 1: work on ANY video game. Very agnostic.


So as the method is transposable to any other video game, fell free to run a radarehack and to reuse this method for the game you want.

If you want a minecraft specific method, please refer to the method of "texture rotation":

```
One of the main and most reliable methods of getting coordinates from a screenshot/video is through any visible texture rotations.
By "texture rotations", we mean the fact that some blocks (like grass or stone) have their textures randomly rotated or flipped based purely on the coordinate of that block, not on the seed. This means that, even without knowing anything about the world itself, the coordinates can still be found quite easily. In theory, you could make your own random world, and if you arrived at the right coordinates, the texture rotations there would look the same as in the screenshot, despite none of the terrain being the same. In practice however, this would take an unimaginably long time to do manually, so there are tools to help with this process.

__How to find coordinates using texture rotations:__
1) To start off with, you have 2 options. Either you can mark and write down the rotations you see in the screenshot manually (relative position of each block + a number assigned to each distinct rotation), or make a recreation of the screenshot in a random world, align yourself with it (type `!!perspective` to see the tools you can use for this), and then use a special resourcepack that can help you identify the rotations in the image (link and tutorial below).
2) When you have the rotations identified, plug the data into the tool linked below to get the coordinates!
The tool + tutorial: <https://github.com/19MisterX98/TextureRotations>

Note: The texture rotation algorithm has changed a few times during the game's development. There were no texture rotations up until beta 1.8, which introduced lilypads with rotations. Other blocks like grass or stone didn't have any rotations until release 1.8.
Also note that while bedrock edition also uses texture rotations, they are different from Java, and aren't supported by the tool above.
```

Let's start!

# Chapter I: find the seed of the picture.

About the infos I have, this seed is `-4768153338510111112` and the version is `1.20.2`.

# Chapter II: locate the picture on the seed.

I need to measure the distance between 2 hight objects in order to get the location of that player using triangulation. Sadly I need to have the height of at least one object!

Then I suggest to watch the cloud. In Minecraft, the cloud height is alway the same.

# Chapter 1, getting cloud height in minecraft `1.20.2`

# Chapter 1.1, the method:

According to the chat gpt prompt:

```
how to get the eight of a mountain from a picture for geoint when the distance from photographer to mountain base is unknow
ChatGPT
```

```
When the distance from the photographer to the mountain base is unknown, estimating the height of the mountain from a photograph can still be accomplished using a reference object in the image and principles of similar triangles. Here's a detailed step-by-step approach tailored for geospatial intelligence (GEOINT):
Step-by-Step Approach

    Select a Reference Object:
        Choose an object within the same plane as the mountain (e.g., a tree, building, or person) whose height (HrefHref​) is known.

    Measure Apparent Heights in the Photograph:
        Measure the pixel height of the reference object (PrefPref​).
        Measure the pixel height of the mountain (PmountainPmountain​).

    Calculate the Height Ratio:
        Determine the ratio of the pixel heights:
        Height Ratio=PmountainPrefHeight Ratio=Pref​Pmountain​​

    Estimate the Height of the Mountain:
        Multiply the height ratio by the known height of the reference object:
        Hmountain=Height Ratio×HrefHmountain​=Height Ratio×Href​

Detailed Example
Step 1: Select a Reference Object

    Assume you have a tree in the photo that is known to be 10 meters tall (Href=10 metersHref​=10 meters).

Step 2: Measure Apparent Heights in the Photograph

    Measure the pixel height of the tree: Pref=50 pixelsPref​=50 pixels.
    Measure the pixel height of the mountain: Pmountain=400 pixelsPmountain​=400 pixels.

Step 3: Calculate the Height Ratio

Height Ratio=PmountainPref=40050=8Height Ratio=Pref​Pmountain​​=50400​=8
Step 4: Estimate the Height of the Mountain

Hmountain=Height Ratio×Href=8×10 meters=80 metersHmountain​=Height Ratio×Href​=8×10 meters=80 meters
Additional Techniques
Using Multiple Photographs (Photogrammetry)

    Capture Multiple Images:
        Take photos from different angles around the mountain.

    Use Photogrammetry Software:
        Input the photos into software like Agisoft Metashape or Pix4D.
        The software generates a 3D model and provides accurate height measurements.

Using Digital Elevation Models (DEMs)

    Acquire a DEM:
        Obtain a DEM of the area from sources like the USGS.

    Identify Coordinates:
        Use GPS to determine the coordinates of the photographer's location and the mountain peak.

    Extract Elevation Data:
        Extract the elevation at the photographer's location and the mountain peak.

    Calculate the Height Difference:
    Hmountain=Elevation at Mountain Peak−Elevation at Photographer’s LocationHmountain​=Elevation at Mountain Peak−Elevation at Photographer’s Location

Conclusion

When the distance to the mountain base is unknown, using a reference object within the same plane in the photograph is a practical method for estimating the mountain's height. For more accurate and detailed measurements, consider using photogrammetry or DEMs, which leverage advanced geospatial intelligence techniques to provide precise height calculations.
```

# Chapter 1.2, guess cloud height (Href)

The cloud height in 1.20.2 is already documented in [this wiki](https://minecraft.fandom.com/wiki/Cloud) to be 128 cubes.

Href = 128 cubes.

# Chapter 1.3, find pixel height of the reference object (Pref):

- 1: download GIMP
- 2: Open the image above with GIMP
- 3: Select the measure tool and read `335,2` pixels (see below).
![image](/gogo-s-blog-cpe/minecraft-speedrun/finding-player-location-on-minecraf-picture-geoint-methodo/gimp.png)


Then the pixel height of the reference object (here the cloud) is `284,2` pixels.


Pref = `284,2` pixels.

# Chapter 1.4, find montain height (Pmountain):

- 1: download GIMP
- 2: Open the image above with GIMP
- 3: Select the measure tool and read `133,8` pixels (see below).
![image](/gogo-s-blog-cpe/minecraft-speedrun/finding-player-location-on-minecraf-picture-geoint-methodo/gimp-montain.png)

Then the pixel height of the reference object (here the cloud) is `133,8` pixels.


Pref = `133,8` pixels.

# Chapter 1.5, find calculate ratio (Height Ratio):

height ratio = Pmontain / Pref
height ratio = `133,8` pixels / `284,2` pixels
height ratio = `0,470` pixels

`height ratio = 0,470 pixels`

# Chapter 1.6, find montain height (Hmountain):

Hmountain = Height Ratio * Href

height montain = Hmountain
height montain = 0,470 * 128
height montain = 60,16 cubes

`height montain = 60,16 cubes`


# Chapter 2, finding left montain distance from player





# Chapter 2, locating right montain distance from player:




# Chapter 2, locating right montain distance from player:


First: locate Player -> trees right distance

from the left picture I see:
- a tree (hopefully tall as it is minecraft) -> 90% angle to the top
- a distance to the top of the tree of 11cubes (I could use h = d * tan(0) but lazy because minecraft is cube and we can count manually)
- a know aqngle to the top (I count 11 cubes from bot to top of the tree thanks to the amazing minecraft structyre). as the plyer is located to the ground I can read that the angle ground <-> top is 20%

then the distance between player and right tree is `11 cubes * tan(70)` = `30.22 cubes` of distance

or `11 / tan(20) = 30.22225161`. Same result is now verified.

# Chapter 3, locating left tree distance from player.

Second locate Player -> left tree distance:

# Chapter 4, regroup distance between two trees and player to find where the picture has been taken.



# Chapter IV 

And... the position is: (-224, 72, -84) !!!!!! TADA !!!!