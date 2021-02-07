---
title: First steps
sidebar: mydoc_sidebar
permalink: ldtk_first_steps.html
folder: mydoc
---

{% include note.html content="This guide was written working with LDtk 0.7.2. Subsequent versions may (and will) be different." %}

## Overview

[LDtk](https://ldtk.io/) is a 2D level/world editor based on Deepnight's experience creating Dead Cells (**that** one) and participating at game jams.

{% include image.html file="ldtk_logo.png" alt="LDtk logo" %}

It's a relatively new project, but with great potential and a growing [Discord](https://ldtk.io/go/discord) community eager to test, improve, create and discuss.

### All features
Easy to use
Modern UI with a strong focus on ease-of-use and quality-of-life features.

**Universal and agnostic**

As long as your favorite game engine can read JSON, you can read data created in LDtk. The file format is simple and well documented 🙂

**Customizable layers**

Integer grid layers, Tile layers and Entity layers support

**Auto-layers**

Paint your collision map and see the grass, textures and all the small details being drawn automatically!

**World editor**

Just press a single key to zoom out to world mode! Pick a layout among “grid-vania“, “linear“, or “free” and reorganize all your levels using plain old simple drag-n-drop.

**Entities**

Fully customizable Entity with custom properties (ex: you can have a “Mob” entity, with a “hitPoints” field, which is an Integer limited to [0,10] bounds).

**Enums**

You can define an enumeration (ex: an “ItemType” enum with “Money“, “Ammo“, “Gun” values) and use this enum in your entity custom fields.

Enums can even be imported and synced directly from Haxe source code files!

**HTML5 and WebGL**

LDtk is built around modern web standards.

**Auto-updated**

You get notified as soon as a stable update is released and it’s up to you to install it when you’re ready, with a single click.

{% include image.html file="ldtk_demo.gif" alt="LDtk demo" caption="Every UI details were carefully designed to make the process of creating levels as smooth as possible." max-width="600" %}
{% include image.html file="ldtk_word_view.gif" alt="LDtk autolayer demo" caption="Choose your world layout among “Grid-vania”, “linear”, or “free” and reorganize all your levels using plain old simple drag-n-drop." max-width="600"%}

## Setup

[Download for free](https://deepnight.itch.io/ldtk/), or name your price if you love the man!

The install process is quite easy, chop chop.


## Demo level

Let's get our hands dirty, to better understand how LDtk works and prepare a demo level for our game.

### The tileset

In this demo we'll be using the beautiful [Inca game assets](https://kronbits.itch.io/inca-game-assets) by [Kronbits](https://kronbits.itch.io/).

{% include image.html file="ldtk_demolevel_tileset.png" alt="Inca game assets" max-width="600" %}

Download **tileset.zip** and extract the file **inca_front.png**. We won't use the others for now.

### Our working folder

If you followed this guide from the [beginning](gamebase_setup.html) you should have a gameBase folder like this

{% include image.html file="gamebase_folder.png" alt="gameBase folder" max-width="600" %}

Double click on ```/res``` and create a new folder ```world```.
Inside ```/world``` create a new folder ```assets```.

<pre>
+---res
|   \---world
|       \---assets
</pre>

Copy/move the **inca_front.png** inside ```/assets``` and then open LDtk.

### Our first world

Once LDtk is open feel free to check the included Samples, and then when you're ready to continue hit the **New** button

{% include image.html file="ldtk_new_world.png" alt="LDtk new world" max-width="600" %}

Navigate to your ```/gameBase/res/world``` folder and save the new map as ```world.ldtk```.

{% include image.html file="ldtk_new_world_save.png" alt="LDtk new world - save file" max-width="600" %}

Next LDtk will present you a brand new empty level.

{% include image.html file="ldtk_new_world_empty.png" alt="LDtk new world - empty level" max-width="600" %}

### Project settings

{% include image.html file="ldtk_new_world_project_settings_button.png" alt="LDtk new world - Project settings button" max-width="600" %}


LDtk has a few settings we could play with, but at the moment we'll stick with the defaults, plus backups.. because s#%t happens :)

{% include image.html file="ldtk_new_world_project_settings.png" alt="LDtk new world - Project settings" max-width="600" %}


### World settings

{% include image.html file="ldtk_new_world_world_settings_button.png" alt="LDtk new world - World settings button" max-width="600" %}

In here we can change the world layout, the level size and other details, but right now we are only going to change the ```Level identifier``` from Level to **Level1**.

{% include image.html file="ldtk_new_world_world_settings.png" alt="LDtk new world - World settings" max-width="600" %}

### Tilesets

{% include image.html file="ldtk_new_world_tilesets_button.png" alt="LDtk new world - Tilesets button" max-width="600" %}

*  Click on ```CREATE TILESET``` and add the **inca_front.png** previosly saved in ```/gameBase/res/world/assets```

{% include image.html file="ldtk_new_world_tileset.png" alt="LDtk new world - Tileset" max-width="600" %}

And as you can see from the warning in red, now we need a few layers to work with.

### Layers

{% include image.html file="ldtk_new_world_layers_button.png" alt="LDtk new world - Layers button" max-width="600" %}

#### TILES layer

First, we need to be able to reference the tileset we're going to use.

*  Click on ```CREATE LAYER``` 

{% include image.html file="ldtk_new_world_layers_select.png" alt="LDtk new world - Layers types" max-width="600" %}

*  Select ```TILES``` and accept the default values. As you can see the TILESET is already selected.

{% include image.html file="ldtk_new_world_layers_tiles.png" alt="LDtk new world - Tiles layer" max-width="600" %}

#### INTGRID layer

{% include note.html content="This layer will be used to **paint** our main level elements." %}

Next, we need an INTEGER GRID layer. This will include the bulk of our level and most of the collision tiles, such as floor and walls.

*  Click on ```CREATE LAYER``` 

{% include image.html file="ldtk_new_world_layers_select.png" alt="LDtk new world - Layers types" max-width="600" %}

*  Select ```NTEGER GRID``` and 

*  Change the ```LAYER IDENTIFIER``` into **Collisions**
*  Change the ```GRID VALUES``` label for #0 into **Walls**
*  Change the ```GRID VALUES``` color into this nice orange **FFB700**
*  Select the **Inca_front** for ```AUTO-LAYER TILESET```

{% include image.html file="ldtk_new_world_layers_intgrid.png" alt="LDtk new world - Intgrid layer" max-width="600" %}

{% include note.html content="**What was that for?** We just told LDtk that when we will use the **Inca front** tileset to paint our elements inside the **Collisions** layer. This will be clearer later." %}



#### AUTO-LAYER layer

{% include note.html content="This layer will be used by LDtk to automatically place some decorations inside our level." %}

This is not strictly needed, but it's fun and it will give us a more complete experience with LDtk.

Click on ```CREATE LAYER``` 

{% include image.html file="ldtk_new_world_layers_select.png" alt="LDtk new world - Layers types" max-width="600" %}

Select ```AUTO-LAYER``` and 

*  Change the ```LAYER IDENTIFIER``` into **Decorations**
*  Select **Collisions** for ```AUTO-LAYER SOURCE```  
*  Select the **Inca_front** for ```AUTO-LAYER TILESET```

{% include image.html file="ldtk_new_world_layers_autolayer.png" alt="LDtk new world - Autolayer layer" max-width="600" %}


### INTGRID Rules

We should be almost ready, right?
Go back to the LDtk main window, select ```Collisions``` and try to paint inside the level grid.

{% include image.html file="ldtk_new_world_no_intgrid_rules.png" alt="LDtk new world - No intgrid rules" max-width="600" %}

Nothing happens! Don't worry, you did nothing wrong :)

Hit ```R``` on your keyboard and see what happens.

{% include image.html file="ldtk_new_world_no_intgrid_rules_renderoff.png" alt="LDtk new world - No intgrid rules render off" max-width="600" %}

LDtk is indeed drawing on the grid, but we didn't told it what rules to follow, so it's not rendering anything. Let's fix this quickly, but first hit ```R``` on your keyboard again.

*  Click on the ```RULES``` button, near **Collisions**
*  Then click on the ```+ GROUP``` button and name it **G_Walls**

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls.png" alt="LDtk new world - Intgrid rules gwalls group" max-width="600" %}

*  Now click on the ```+``` on **G_Walls**

Here is where the magic happens
{% include image.html file="ldtk_new_world_intgrid_rules_gwalls2.png" alt="LDtk new world - Intgrid rules gwalls" max-width="600" %}
but we need first to understand how it works.

*  The grid on the bottom right represent the cell subject to this rule and the cells around it
*  The cell with the white dotted border is our primary target
*  The ```3x3``` above the grid represent the number of neighbour cells around the target
*  ```Random tiles```, is where we select one or more tiles to be rendered according to this rule

Sounds complicated? It really is not. Let's play with it and create our first basic rule.

*  Click on the tile icon 

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls3.png" alt="LDtk new world - Intgrid rules gwalls select tile" max-width="600" %}

*  Select a 16x16 tile we'll use as basic brick for floor, walls and ceiling

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls4.png" alt="LDtk new world - Intgrid rules gwalls select tile brick" max-width="600" %}

*  And then click on our target cell at the center of the grid

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls5.png" alt="LDtk new world - Intgrid rules gwalls select tile brick complete" max-width="600" %}

Since we did not select any neighbour cells, the dropdown will automatically revert to the basic ```1x1``` selection, meaning that LDtk will render that tile every time we draw a yellow Walls cell.

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls6.png" alt="LDtk new world - Intgrid rules gwalls 1x1" max-width="600" %}

Looks good? Well, to be honest it's not be best rule to use, because of course it won't check its surroundings and it will pile bricks over bricks, but we'll do better later.

What we can do now is create a rule for the corner stones.

*  Click again on the ```+``` on **G_Walls**
*  Select a ```16x16``` corner stone tile
*  Using the ```3x3``` grid instruct LDtk to use it when the target cell has one **Walls** cell below and one on the right

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls7.png" alt="LDtk new world - Intgrid rules gwalls corner stone" max-width="600" %}

Nice, that's progress :)

Now, what we can do is create another three rules for the other corner stones, or do some magic with mirrors.

*  On the corner stone rule click on ```X``` and ```Y``` to use this rules even when X and Y are flipped

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls8.png" alt="LDtk new world - Intgrid rules gwalls corner stone flips" max-width="600" %}

Unfortunately this tile look weird when flipped, because of the lights baked into it. In this case it's better to do it the hard way.

*  On the corner stone rule click on ```X``` and ```Y``` to remove the flipping
*  Create or clone the corner stone rule to fit the other three corners

{% include image.html file="ldtk_new_world_intgrid_rules_gwalls9.png" alt="LDtk new world - Intgrid rules gwalls corner stones" max-width="600" %}

Much better, huh?


### AUTO-LAYERS Rules

Select the **Decorations** layer and the first thing you will notice is that you can't draw on the grid. That's because the job of this layer is to draw tiles automatically following specific rules, not different from those created in the INTGRID layer.

These tiles won't have collisions in game, so you can use this feature to put random stuff in the level, like plants, rocks, lamps or signs.
In this case we don't have many tiles to work with, so we'll place random decorative bricks on top of the existing floor and ceiling.

{% include note.html content="We could for example move the corner stone rules in this layer." %}

*  Click on the ```RULES``` button, near **Decorations**
*  Then click on the ```+ GROUP``` button and name it **Floor and ceiling**
*  Click on the ```+``` on **Floor and ceiling**
*  Click on the tile icon and this time select a bunch of ```16x16``` tiles, while pressing ```CTRL``` on your keyboard

{% include image.html file="ldtk_new_world_autolayer_rules_floorceiling.png" alt="LDtk new world - Autolayer rules 32x16" max-width="600" %}

*  On the grid click on the center target cell
*  And right click on the cells right above and below the target cell

{% include image.html file="ldtk_new_world_autolayer_rules_floorceiling2.png" alt="LDtk new world - Autolayer rules 32x16" max-width="600" %}

We just instructed LDtk to place randomly those tiles **only if** there are no cells of the type **Walls** above and below that cell.
But as you can see that rule, as it is, is overwriting all our nice default bricks on the floor and on the ceiling. Let's fix this adding some more randomness.

*  Change the ```%``` value from 100 to 20, so this rule will be applied only one fifth of the times
*  Change the ```X module``` from 1 to 2, so the rule will be applied every 2 columns, avoiding two adjacent decorative tiles 

{% include image.html file="ldtk_new_world_autolayer_rules_floorceiling3.png" alt="LDtk new world - Autolayer randomness" max-width="600" %}

We're done with the level design for now, but we also need a **hero** and an **item** to interact with.

### Entities

Entities are all those dynamic objects that are in the level, but not part of the level itself. Our **hero** is an entity, a coin is an entity, an enemy is entity.

In this case we'll do something simple:

*  A ```Hero```, because we would like to play this game
*  An ```Item```, that could be a **Diamond** or a **Heart**

#### Items enum

Since we want an ```Item``` entity that can be **Diamond** or **Heart**, let's create an ```Enum``` to be able to pick.

{% include image.html file="ldtk_new_world_enums_button.png" alt="LDtk new world - Items enum" max-width="600" %}

*  Click on ```CREATE ENUM``` button
*  Name the ```ENUM IDENTIFIER``` **Items**
*  Click on ```ADD VALUE``` and create **Diamond** and **Heart** values 

{% include image.html file="ldtk_new_world_entities_itemsenum.png" alt="LDtk new world - Items enum values" max-width="600" %}

#### Hero entity

{% include image.html file="ldtk_new_world_entities_button.png" alt="LDtk new world - Entity button" max-width="600" %}

*  Click on ```CREATE ENTITY``` button
*  Name the ```ENTITY IDENTIFIER``` **Hero**
*  Change ```EDITOR VISUAL``` shape to **Ellipse** 
*  Change ```MAX PER LEVEL``` to 1 and **move the last one instead of adding** when max is reached.

{% include image.html file="ldtk_new_world_entities_hero.png" alt="LDtk new world - Hero entity" max-width="600" %}

#### Item entity

{% include image.html file="ldtk_new_world_entities_button.png" alt="LDtk new world - Entity button" max-width="600" %}

*  Click on ```CREATE ENTITY``` button
*  Name the ```ENTITY IDENTIFIER``` **Item**
*  Change ```EDITOR VISUAL``` color to **FF0000** 
*  Click on  the ```+ FIELD``` button and select ```Enum```, then select ```Items```
*  Change values in ```DISPLAY IN EDITOR``` to **Show value only** and **Above**

{% include image.html file="ldtk_new_world_entities_item.png" alt="LDtk new world - Hero entity" max-width="600" %}

### Entities layer

{% include image.html file="ldtk_new_world_layers_button.png" alt="LDtk new world - Layers button" max-width="600" %}

*  Go back to ```Layers``` tab
*  Click on ```CREATE LAYER``` 

{% include image.html file="ldtk_new_world_layers_select.png" alt="LDtk new world - Layers types" max-width="600" %}

*  Select ```ENTITIES``` and accept the default values. 

Now your project should look like this

{% include image.html file="ldtk_new_world_entities_complete.png" alt="LDtk new world - Entities" max-width="600" %}

You should also be able to place first your Hero

{% include image.html file="ldtk_new_world_entities_hero_placed.png" alt="LDtk new world - Entities hero placed" max-width="600" %}

and then your items

{% include image.html file="ldtk_new_world_entities_items_placed.png" alt="LDtk new world - Entities items placed" max-width="600" %}

