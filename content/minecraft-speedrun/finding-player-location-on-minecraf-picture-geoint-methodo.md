---
title: "find player location in minecraft from picture"
date: 2024-06-17T12:37:42+02:00
draft: false
---

# 1 Project philosophy

In some case, speedrunners could watch a "secret" location from a specific seed on youtube video. In this case, they will need to find it to redo the speedrun method. In this tutorial, I will help you to find a speedrun location from a picture.

The target I will use will be the next below.

![image](/gogo-s-blog-cpe/minecraft-speedrun/finding-player-location-on-minecraf-picture-geoint-methodo/trees.png)


This project is a geoint methodology (tutorial) to find the coordinate (x,y) from a picture. The project consist to:
- 1: find the seed of the picture
- 2: find coordinate from picture on the seed

In this tutorial we will use math principles of triangulation (we use a compass on a map get the intersection of 2 points of a specific distance) and trigonometry (math on rectangle triangles).

This method has the disadvantage from "texture rotation"* to:
- be more complicated and more manual than minecraft specific methods because there is no tool to do that automatically.
- require some reverse engineering to have a map of the game. See [radare hack](https://gamehacking.academy/pages/5/08/).

But the geoint method to find coordinate from picture on the seed has the advantage to:
- work on ANY video game. Very agnostic.


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



# Chapter 2: locate the picture on the seed.


I need to measure the distance between 2 trees in order to get the location of that player using triangulation. 

#chapter 1, locating right tree distance from player:

First: locate Player -> trees right distance

from the left picture I see:
-a tree (hopefully tall as it is minecraft) -> 90% angle to the top
-a distance to the top of the tree of 11cubes (I could use h = d * tan(0) but lazy because minecraft is cube and we can count manually)
-a know aqngle to the top (I count 11 cubes from bot to top of the tree thanks to the amazing minecraft structyre). as the plyer is located to the ground I can read that the angle ground <-> top is 20%

then the distance between player and right tree is `11 cubes * tan(70)` = `30.22 cubes` of distance

#chapter 2, locating left tree distance from player::

Second locate Player -> left tree distance:


#chapter 3, regroup distance between two trees and player to find where the picture has been taken.