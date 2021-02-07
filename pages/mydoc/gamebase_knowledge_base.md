---
title: Knowledge base
sidebar: mydoc_sidebar
permalink: gamebase_knowledge_base.html
folder: mydoc
---

{% include note.html content="The information below is mainly from Deepnight's tutorial [Using GameBase to create an Haxe+Heaps game](https://deepnight.net/tutorial/using-my-gamebase-to-create-a-heaps-game/) because I'm not going to reinvent the wheel :)" %}

## Overview

gameBase was intended to be simple to use but does **NOT** mean it's a simple project. There are a few important notions and a lot of moving parts to understand to be able to use its full potential.


## About “tmod”

```tmod``` is a value connected to the duration of the frame, and more precisely, the time elapsed between two consecutive game frames.

* **on 60 FPS, tmod is 1.0** (the “normal” value)
* on 30 FPS, tmod is 2.0
* on 120 FPS, tmod is 0.5

```tmod``` can be used to adjust values that are FPS dependent, such as velocities or accelerations.

The idea is:

*  if the game runs **slower** (ie. less than 60 FPS), all the movement increments should be higher, to compensate for the missing frames.
*  if the game runs **faster** (ie. more than 60 FPS), all the movement increments should be smaller to acknowledge the extra frames.

See [Delta time](https://en.wikipedia.org/wiki/Delta_timing) to learn more about this classic concept.


### Working without “tmod”
The ```dn.Process``` class has a ```fixedUpdate()``` which runs (or at least tries to run) at a fixed lower FPS, usually 30 or 24 FPS (check the **fixedUpdateFps** variable). The FPS of these fixed updates is guaranteed, within the realms of possibility.

The ```Entity``` class also has a similar ```fixedUpdate()``` which runs at the same fixed FPS as the **Game**.

A classic approach is to **do every gameplay-related things, like physics, or velocities inside the “fixed” updates**, and do everything else (rendering, particles, etc.) in “real FPS” updates.

This keeps the gameplay code quite simple, without having to rely on the tmod/delta time values.

You might think it would be an issue to have your gameplay code in a 30 FPS loop instead of 60 FPS or more, but bear with me: no one will notice. Dead Cells, which is known for its fast-paced action & gameplay actually uses 30 FPS loops for the gameplay elements. The render is done at 60 FPS.

**Important**: all the **controller** related checks should happen **inside the real FPS updates** because that’s the only way to catch a user input at the exact moment it happens. The fixed updates won’t catch these events, because these fixed updates don’t occur on every single frame.


## Classes & API

### Boot.hx: where everything starts
The first thing called in your code is in the Boot.hx method ```main()```. From here, we create a Main, which creates a Game.

### Loops
All the updates are called in the following order:

*  **Boot.hx** has an ```update()``` which takes care of low-level stuff. You shouldn’t do much here unless you have very specific needs.
*  **Main.hx** has an ```update()``` too, and is basically your global app main update. It also has a ```postUpdate()``` which happens after the update().
*  **Game.hx** also has an ```update()```, a ```preUpdate()```, a ```fixedUpdate()``` and a ```postUpdate()```. This is where your game related code will happen.

Note that **Boot** extends ```hxd.App``` which is the top-level app class in Heaps. I use a different class for Main and Game: ```dn.Process```.

```dn.Process``` class takes care of the updates, and each Process can have children processes, support pausing, have preUpdates, fixedUpdates, postUpdates and few other useful things.

The **philosophy** with GameBase is quite simple: all your future Processes should be either child of **Main** (any section of your app which is not the game, like an intro screen), or **Game** (if it’s part of the actual game).


### Important classes
All code files are in ```/src``` folder.

*  ```Main.hx```: the main app loop, see the ```update()``` method
*  ```Game.hx```: created every time a game is started, it also has an ```update()```
*  ```Entity.hx```: the most important thing after the Game. It’s the **base class for everything that moves** in the game (player, enemies, bullets, items, etc.). Everything except particles (see ```Fx.hx```). Read below for more explanations about the **Entity class**.
*  ```Level.hx```: your world, level, room, or whatever is your environment. Some games might have none of these, or multiple instances, it’s up to you.
*  ```Camera.hx```: a basic camera that can optionally track an Entity (say, the player)
*  ```Fx.hx```: a simple particle system
*  ```Lang.hx```: a neat way to automatically extract your texts directly from your code to generate PO files compatible with the popular GetText translation ecosystem. Check the [specific tutorial](https://deepnight.net/tutorial/part-4-localize-texts-using-po-files/) to see how it works.
*  ```Const.hx```: contains a set of constant values I use to tweak my game, like the standard FPS, your starting health points, or stuff like that.
*  ```Assets.hx```: a single class to access assets like tilesets or sounds. All your assets (art, sound, other data files) that are meant to be loaded/used by the game should be put in the ```/res``` folder. You can access them in your code using the ```hxd.Res.myAsset``` API.


### Misc classes
*  ```import.hx```: note the lowercase format of this file name, it allows to have global imports for every class of your app (see: [https://haxe.org/blog/importhx-intro/](https://haxe.org/blog/importhx-intro/) ). Neat.
*  ```tools/LPoint.hx```: a simple Point class that supports grid-based coordinates.
*  ```ui/Hud.hx```: a process of Game that can be used for any HUD (head-up-display, aka. interface) for your game, like gold, life, ammo, etc.
*  ```ui/Window.hx```: a simple pop-up object.
*  ```ui/Modal.hx```: same as Window, except it pauses the game while it’s open.


## The Entity class

### Philosophy
```Entity.hx``` uses the same “grid-based” logic as described in Deepnight's [Simple 2D engine](https://deepnight.net/tutorial/a-simple-platformer-engine-part-1-basics/) article. 

**Please note that it’s totally up to you to write a very different Entity system to suit all your needs.**

 Basically, all the 2D grid-based logic is here. Everything else in GameBase should fit any kind of game, be it a platformer, a match-3 puzzle, or a hidden object.


### Features
*  **Loops**: preUpdate, update, fixedUpdate and postUpdate
*  **Safe disposal** mechanic: just call the ```destroy()``` of an Entity to mark it as destroyed. It won’t be destroyed instantly, but only at the end of the current frame (the ```onDispose()``` is then automatically called), to avoid any null value in the course of the loops.
*  **Listing**: access Entity.ALL static array for a dynamic list of all existing entities. Note that some might be flagged as “destroyed” (see the previous point).
*  **Coordinates**: each entity uses a grid-based coordinate system. ```cx,cy``` are the grid coordinates, while ```xr,yr``` are the position inside a single cell. For example, cx=5 and xr=0.5 mean “in column 5, at 50% of the cell“. More explanations about this approach in Deepnight's [Simple 2D engine](https://deepnight.net/tutorial/a-simple-platformer-engine-part-1-basics/) article. 
*  **Velocities**: ```dx,dy``` are the current x/y speeds of the entity (added to coordinates on each frame). They also use “grid-based” values. So having dx=0.5 means “moving 50% of a cell on each frame“. ```dx,dy``` are multiplied on each frame with **frictions** which slow them down (if friction<1).
*  **Sprite**: the visual representation of an Entity is the variable ```spr```. It’s a ```dn.heaps.slib.HSprite``` class, which is a super-charged ```h2d.Bitmap```. Please note that the coordinates of this sprite are only updated during the ```postUpdate()```, it’s never updated nor manipulated outside of this loop. If you need the coordinates of the entity object, you should always refer to ```cx,cy``` + ```xr,yr```.