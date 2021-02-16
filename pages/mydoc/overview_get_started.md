---
title: Get Started
sidebar: mydoc_sidebar
permalink: overview_get_started.html
folder: mydoc
---

## Overview

Oh boy, we first need a big bunch of stuff :)

*  Haxe
*  Hashlink
*  Heaps
*  Haxe libs
*  VSCode (optional, but recommended)

For convenience, this guide will mainly follow the same steps documented by Deepnight in his [Haxe + Heaps tutorial page](https://deepnight.net/tutorials/).

## Installing Haxe 
Haxe is a cool programming language that can compile to multiple platforms. It’s free and open-source.

Download the [latest Haxe installer](https://haxe.org/download/) and install it to a folder like **C:\Dev\HaxeToolkit**

Important: for the next sections of this tutorial, I’ll assume Haxe is installed in this folder.

After the setup, you should get 2 folders:

*  **C:\Dev\HaxeToolkit\haxe**: the compiler and all the standard libraries

Now open Command Prompt and type 

```haxe
haxe
```

You should get something like

{% include image.html file="haxe_version.png" alt="Haxe version" %}


## Installing Hashlink 
Hashlink (HL) is Haxe virtual machine. We use it to build cross-platform titles.

Download the [latest Hashlink build](https://github.com/HaxeFoundation/hashlink/releases) and extract it to a folder like **C:\Dev\HaxeToolkit\hl**


{% include note.html content="Add the Hashlink folder (ie: **C:\Dev\HaxeToolkit\hl**)  to your PATH environment variable ([how?](https://www.google.com/search?q=adding+path+in+windows))." %}


Now open Command Prompt and type 

```haxe
hl
```

You should get something like

{% include image.html file="hashlink_version.png" alt="Haxe version" %}

## Installing Heaps 
HeapsIO is a free open-source 2D/3D engine used in large game projects, like Dead Cells, Northgard or Evoland 2.

The engine is a library of Haxe (ie. an Haxelib) which can be installed easily using the bundled haxelib.exe tool.
Open Command Prompt and type 

```haxe
haxelib git heaps https://github.com/HeapsIO/heaps.git 
```

**Important**: we won’t use the default haxelib install heaps command here, because the official GIT version is much more up-to-date than the haxelib repo.

## Installing Haxe libs

Open Command Prompt and type 


**DirectX support in HashLink:**
```haxe
haxelib install hldx
```
**OpenGL/SDL support in HashLink:**
```haxe
haxelib install hlsdl
```
**deepnightLibs:**
```haxe
haxelib git deepnightLibs https://github.com/deepnight/deepnightLibs.git
```
**LDtk API:**
```haxe
haxelib install ldtk-haxe-api https://github.com/deepnight/ldtk-haxe-api.git
```

**CastleDB:**
```haxe
haxelib git castle https://github.com/ncannasse/castle.git
```



**You can check the installed libs by typing:**
```haxe
haxelib list
```


## VSCode (optional, but recommended)

VSCode is a nice IDE that features full Haxe integration if you install the dedicated extension. Out of the box, you’ll get code completion, easier project setup, debugging & much more.

Download the [latest VSCode installer](https://code.visualstudio.com/) and install it following the usual steps.
When you're up and running download the Haxe Extension Pack from VSCode built-in extension browser.

{% include image.html file="vscode_haxe_ext.png" alt="Haxe extension pack" %}


## Ready? Next stop, gameBase

Oki-dokie, let's move to [gameBase](gamebase_setup.html)