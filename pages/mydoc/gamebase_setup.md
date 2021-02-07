---
title: Setup
sidebar: mydoc_sidebar
permalink: gamebase_setup.html
folder: mydoc
---

## Overview

[gameBase](https://github.com/deepnight/gameBase) offers a minimal set of classes and tools to get started quickly making your own game. It’s completely open source and easy to adapt to your needs. 

It's not that easy (for me at least) to provide a bird's-eye view of the entire gameBase in a few words, but for now let'sa say that

*  It uses a grid based logic: the level, for example, is a grid of empty cells (where the player can walk) and wall cells.
*  It uses haxe [deepnightLibs](https://github.com/deepnight/deepnightLibs), general purpose libs Deepnight uses on his projects.

## Requisites

Firt we need Haxe and Heaps installed. If you don't have them please follow [this guide](overview_get_started.html).

## Get gameBase

gameBase is a public [gitHub repository](https://github.com/deepnight/gameBase).
To get it you can
*  Use template button
*  Fork it on your github and then clone it on your computer
*  Clone it directly on your computer
*  Download the code archive on your computer

Bottom line you need the code stored locally on your computer, how you do it really depends on your working pipeline.
If you don't have a gitHub account and you just want to check it out, just download and extract the zip somewhere.

{% include image.html file="gamebase_download.png" alt="gameBase download" %}


## Test gameBase with Haxe

### Compiling

Open a command prompt and go to the folder where gameBase was cloned or decompressed.



#### DirectX for HashLink VM 
```haxe
haxe hl.dx.hxml
```
{% include note.html content="This should generate a __client.hl__ in your /bin folder." %}


#### Javascript (WebGL)
```haxe
haxe js.hxml
```
{% include note.html content="This should generate a __client.js__ in your /bin folder." %}


### Running

To run gameBase, execute one of these commands

#### DirectX for HashLink VM 
```haxe
hl bin\client.hl
```



#### Javascript (WebGL)
```haxe
start js.html
```

In both cases you should see something like this

{% include image.html file="gamebase_firstrun.png" alt="gameBase first run" %}




## Test gameBase with VSCode (recommended)

VSCode is the recommended way to work with gameBase, and the main advantage in my opinion is being able to work in debug mode.

If you plan to debug WebGL (Javascript) content, you’ll need one of the following extensions for VScode:

*  Firefox: [Firefox debugger extension](https://marketplace.visualstudio.com/items?itemName=firefox-devtools.vscode-firefox-debug)
*  Chrome: [Chrome debugger extension](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)

### VSCode haxe configuration

Don’t forget to change the HXML used for code completion before trying to run or debug gameBase. Check the bottom left corner of VSCode and you should see a gear icon with the Haxe label. Next to it there's the haxe configuration VSCode will use.

{% include image.html file="vscode_haxe_config.png" alt="VSCode haxe config" %}

Click on it and VSCode will present different options

{% include image.html file="vscode_haxe_config2.png" alt="VSCode haxe config" %}

Select one of the debug HXML, like 

* **hl.debug.hxml** (if you like to work with DirectX) 
* **js.debug.hxml** (if you like to work with WebGL).

### Running

How hit F5 to run a debug session. If you choose to work with DirectX you should see something like this

{% include image.html file="gamebase_firstrun_vscode.png" alt="gameBase first debug run using VSCode" %}


## That's not a game!

Yeah, I know. One step at a time :)
We'll get there, but first we need to get a little [knowledge base](gamebase_knowledge_base.html).

Trust me, it will be handy in the future.