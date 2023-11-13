# Simple_Path_Tracer_Documentation
This is the Documentation for the Unreal Engine plugin. 
WIP
Store Link

## Description
Simple Path Tracer is a C++ Plugin containing a set of functions for editing and drawing paths both in the editor and in rantime.  
The plugin also includes ready blueprint examples that show how the plugin functions can be used.

To draw a path, you just need an array of points.

The Blueprint examples use an array of spline points to draw the path. 
Spline is convenient to use to customize the appearance of the path, but the spline itself is not necessary, the path can be built through any array of points, for example, obtained as Navmesh Path or with the help of some of your algorithm.

You can download the demo level (for UE versions 4.6 - 5.3)  
link
The demo level provides many additional examples.  
Before you can open a demo level you need to enable the plugin for your engine version (read more).  
You can migrate the entire level with examples or individual examples to your project using migrate (read more).  

Path Tracer Toolkit is more focused on visual style, while Simple Path Tracer is more focused on optimization and customization.  
Simple Path Tracer will suit you if you need a more optimized solution, for example if you need to draw many paths or with many points.  
If necessary, you can use both toolkits together, e.g. to use the SPT to PTT path editing functions or to use PTT to SPT path markers.  

## Quick Start
Install the plugin on your version of the engine.  
Activate the plugin (if not activated) and restart the engine.  
![SPT_01](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/f9ae88e2-fff4-47d3-abbf-eb3cb51c0896)

Check if the plugin is enabled from Edit > Plugins.
![SPT_04](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/acf986ee-f28b-4521-a244-b64de086a1cc)

To access the Blueprint examples, do the following, 
for UE4: 
![SPT_02](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/8f4fe1f3-083c-49a8-bb95-a917946ea68c)

for UE5:  
![SPT_03](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/d7a20114-106d-4b6d-81be-c21a7ff26787)

Download the demo level for more examples.  

Create a "Simple Path Tracer Actor" actor, or use one of the ready-made examples.
"Simple Path Tracer Actor" contains all the functions for editing and creating a path.
You can also create it, or classes inheriting from it, during the game.
