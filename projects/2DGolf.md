---
layout: default
permalink: "/projects/2DGolf/"
title: "Golf in 2D"
---

<h1> Golf in 2D! </h1>

<h2> Introduction </h2>

This project features a 2D Golf game made using the open-source Godot engine. All gameplay functionality was written using GDScript (very similar in syntax to C#) and Godot's own API. This page details highlights of some of the elements included in the game prototype along with a breakdown of how certain features were implemented. Godot was chosen as it is open-source, community-driven and written with C++, a language that I am confident with. This allowed me to develop an insight into understanding the inner workings of a game engine, particularly with regards to the simulation of physics. I also created a fun game prototype out of it, of course!

<table style="margin-left:auto;margin-right:auto;width:50%">
	<tr>
	<td> <img src="https://azhb.github.io/website2DGolfSplash.png" alt="2D Golf" width="400px"></td>
	</tr>
</table>

<h2> Game Architecture </h2>

In the Godot engine, levels are composed of 'nodes'. Scripts are attached to nodes to implement functionality. Nodes can be parented to other nodes to form tree-like structures. In this way, the Godot engine uses both inheritance (attaching scripts to derive an inherited class) and composition (attaching nodes as children to other nodes) to create complex games. The image below demonstrates this concept - it is the default structure of nodes that makes up a basic level in 2D Golf. I always begin with this structure when implementing new levels. 

<table style="margin-left:auto;margin-right:auto;width:50%">
	<tr>
	<td> <img src="https://azhb.github.io/websiteGolf2DLevelTree.PNG" alt="Default Level Tree" width="200px"></td> <td> <img src="https://azhb.github.io/websiteGolf2DLevelTreeConcise.PNG" alt="Concise Level Tree" width="200px"></td>
	</tr>
	<tr>
		<td> Default Level Tree (Expanded) </td> <td> Default Level Tree </td>	
	</tr>
</table>

In the Godot engine, nodes communicate with each other using references obtained from the scene tree (by either navigating through the parent-child relationships or through hard-coded paths). It is crucial, then, that the scene tree for a level always uses the same structure so that the functionality programmed into nodes is reusable across levels.

<h4> Level Manager </h4>

The level manager is responsible for storing and manipulating all of the key level-specific data, including how many shots the player has left, how much time is left, the players score etc. It also communicates with the player manager and user interface. It has a child node called 'ruleset'. The ruleset node defines the nature of the level - Is there a time limit? Is there a limit to the number of shots? The player manager node has a common interface with the ruleset node, allowing new rulesets to be made by inheriting from the base ruleset node to add or change funcionality.

```gdscript
extends Node

##Scene References##
var interactables
var ruleset
var player_ui

##Internal variables##
var shots_left
var time_left
var timer

# Called when the node enters the scene tree for the first time.
func _ready():
	interactables = get_parent().get_node("Interactables")
	ruleset = get_node("Ruleset")
	player_ui = get_parent().get_node("UI/PlayerUI")
	timer = $Timer
	shots_left = ruleset.num_shots
	time_left = ruleset.time_limit
	if shots_left != INF:
		player_ui.update_shots(shots_left)
	#if time_left != INF:
	#	timer.start(1)
```
The code block above shows the initialization of the level manager, demonstrating how to get a reference to another node using string-paths from the root node of the leve (as in "UI/PlayerUI") and by navigating the parent-child tree (as in $Timer). Note that all class variables are public in Godot, so I opt to use the terminology 'internal' (to refer to variables modified by the class or its children within a script) and 'external' (to refer to variables that I have exposed to changes within the Godot editor).

<h2> Gameplay Features </h2>

This section will provide details on some of the many gameplay elements included in this prototype. The very basic level pictured below demonstrates the core gameplay mechanic and the user interface. There are far more interesting and varied features explored in this section!

<table style="margin-left:auto;margin-right:auto;width:50%">
	<tr>
	<td> <img src="https://azhb.github.io/website2DGolfBasicLevelEditor.PNG" alt="Basic level in editor" width="600px"> <img src="https://azhb.github.io/test.gif" alt="Basic level animation" width="600px"> </td> 
	</tr>
</table>

<h4> Static Objects </h4>

The majority of the level geometry is composed of static objects. These nodes have a Sprite (which includes functionality to render an image to the screen each frame) and a Collision Shape (which includes functionality to detect overlaps and collision within the physics engine). For nodes that have more complex shapes, the Collision Shape is replaced by a Collision Polygon. A Collision Polygon seperates the geometry of the shape (automatically or by hand) into distinct polygons to allow for efficient collsion detection. 

<table style="margin-left:auto;margin-right:auto;width:50%">
	<tr>
	<td> <img src="https://azhb.github.io/website2DGolfPrefab.PNG" alt="Prefab" width="200px"> <img src="https://azhb.github.io/website2DGolfPrefabTree.PNG" alt="Prefab Tree" width="200px"> </td> 
	<td> <img src="https://azhb.github.io/website2DGolfPrefabAdvanced.PNG" alt="Advanced Prefab" width="200px"> <img src="https://azhb.github.io/website2DGolfPrefabAdvancedTree.PNG" alt="Advanced Prefab Tree" width="200px"> </td>
	</tr>
	<tr>
		<td> Simple Geometry </td> <td> Complex Geometry </td>	
	</tr>
</table>

In order to rapidly prototype levels, I have implemented a collection of static object 'prefabs'. Some of these are implementing Collision Shapes and some are implementing Collision Polygons - it depends upon the complexity of their geometry.

<table style="margin-left:auto;margin-right:auto;width:50%">
	<tr>
	<td> <img src="https://azhb.github.io/website2DGolfPrefabLevel.PNG" alt="Prefabs" width="400px"></td>
	</tr>
</table>

<h4> Dynamic Objects </h4>

<h4>  </h4>

<h4> Interactive elements </h4>

All interactive elements share a common interface. All have setters and getters. Class doesnt call its own setter to not get stuck in loop.

<h4> Force Generators </h4>

<h4> Launchers </h4>

<h4> Physical Surface Properties </h4>

<h2> User Interface </h2>
