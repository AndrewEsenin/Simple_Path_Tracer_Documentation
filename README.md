# Simple Path Tracer Documentation
Unreal Marketplace Link  
YouTube  
Support email: andrewesenin27@gmail.com  
Demo Project:
Playble Demo:
  
<!--ts-->
* [Description](#Description)
* [Quick Start](#Quick-Start)
* [Blueprint Examples](#Blueprint-Examples)
* [Functions Description](#Functions-Description)
* [Materials](#Materials)
* [Features and Tips](#Features-and-Tips)
* [Demo Project](#Demo-Project)
<!--te-->

<br />

## Description
Simple Path Tracer is a C++ Plugin containing a set of functions for editing and drawing paths both in the editor and in runtime.  
The plugin also includes ready blueprint examples that show how the plugin functions can be used.  
The plugin source code is also included in the asset.  

To draw a path, you just need an array of points.

The Blueprint examples use an array of spline points to draw the path. 
Spline is convenient to use to customize the appearance of the path, but the spline itself is not necessary, the path can be built through any array of points, for example, obtained as Navmesh Path or with the help of some of your algorithm.

You can download the [Demo Project](#Demo-Project), it contains many additional examples.  

<br />

## Quick Start
1. Install the plugin on your version of the engine.    

![SPT_01](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/f9ae88e2-fff4-47d3-abbf-eb3cb51c0896)


2. Activate the plugin (if not activated) and restart the engine.

![SPT_04](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/acf986ee-f28b-4521-a244-b64de086a1cc)


3. To access the Blueprint examples, do the following, 
for UE4: 

![SPT_02](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/8f4fe1f3-083c-49a8-bb95-a917946ea68c)

   for UE5:  

![SPT_03](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/d7a20114-106d-4b6d-81be-c21a7ff26787)


4. "Simple Path Tracer Actor" contains all the functions for editing and creating a path.  
You can create your own empty actor or use one of the ready-made examples.

![SPT_05](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/5067783b-38f0-4d1b-a77f-d4a083f8d7f7)

If you want to use Path Tracer in the editor, simply drag one of the ready-made examples onto the level and edit the spline.  
To quickly create points, hold Alt and drag:  

https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/8f0863f2-b76f-4612-ae97-04b5d8c074e7



If you want to use Path Tracer at runtime, you can do the following:
Create a new Path Tracer using the Spawn Actor from Class function, selecting one of the ready-made examples, and connect this node to the Begin Play event (for example in Player Controller).

![SPT_20](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/9192f9dc-d16d-4781-a9d2-f3fa75a39bed)

Now you can, for example, draw a path from the player character to the coordinates under the cursor like this:

![SPT_21](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/6de31749-3612-4c4c-b603-9796244ee5bd)

If you need to draw a path along your array of points, call the Draw Path function in any of the ready-made examples in the same way and connect your array of points to this function.

If you want to use Path Tracer with a sequencer, then ([read more here](#Sequencer)).   

<br />
<br />

## Blueprint Examples  
All main examples are located in the plugin content folder.  
You can find more exemples in [Demo Project](#Demo-Project).    

Look at how the examples are made to create the path you need, or use a ready-made example.  
To work in the Editor, the logic runs in the Construction Script, which is called every time the actor changes or moves (for example, when you edit a spline).  
  
Blueprints whose name starts with "BPc_" are child classes of other blueprints, there are no logic changes, only changes to the class settings (different line thickness, different materials used, etc.).    
  
To find the parent blueprint, open it and click in the upper right corner:  

![SPT_07](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/225b8910-8b0a-4287-8560-8ed891113333)
  
### Description  
All examples have similar code, but to improve readability, all examples were made in separate classes.  

| **Blueprint** | **Description**  |                                                       
|---------------|------------------|
| **BP_SPT_Master** | This example is identical to the **BP_SPT_Line**, the difference is that here the material parameters are included in the settings. It is useful for testing so as not to create a large amount of materials. |
|  |  |
|  |  |
|  |  |

In the Blueprint examples, a procedural mesh is used to visualize the path.

![SPT_15](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/cd60c490-3718-4a3f-aa26-8a8b7293a6ed)
  
It also has added plaens for the start and end of the path.  
This is a regular Blueprint Actor, you can freely remove or add any of your own components to it.

If you want to use Path Tracer at runtime, you can delete the Spline and Billboard components, and all associated logic, for optimization.  

![SPT_22](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/f9c25256-719e-43cf-9976-61ae1e93a4f2)

<br />

### Settings  
Drag the blueprint example to the level.   
On the detail panel you will find its settings:  
  
![SPT_16](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/15b29c0f-c0bd-4a94-8213-5974c6eca203)

The main parameters, may differ depending on the blueprint class.  
| **Parameter** | **Description**  |                                                       
|---------------|------------------|
| Align Spline Horizontal | This button aligns all spline points in the horizontal plane. Due to the way the construction script works, the visual path will not be updated, you need to click on the Update parameter or move the entire spline or actor. |
| Offset Spline Points To Actor Center | This button aligns the center of the actor to the center of the spline, useful if you have moved the spline points too far and the actor becomes awkward to move or rotate. Due to the way the construction script works, the visual path will not be updated, you need to click on the Update parameter or move the spline or the entire actor, after which you need to reselect the actor to update the movement gizmo. |
| Update | A cosmetic variable required to update an actor in the editor, changing it (like any other variable) causes the Construction Script to update. |
| Thickness | Half of the line thickness. |
| Corner Radius | The distance at which the corners will be rounded. |
| Corner Segments | Number of polygons in each corner. |
| Line Material | The material that will be applied to the main path mesh. |
| Enable Start Plane | Enables display of the start plane, the remaining parameters are responsible for the alignment of this plane. |
| Enable End Plane | Enables display of the end plane, the remaining parameters are responsible for the alignment of this plane. |
| Enable UV | Enables UV generation, needed to display a unique texture on the path mesh. |
| Scale UV | Changes the texture tiling along two axes, compresses or stretches the UV of the entire mesh. |
| Offset UV | Offsets the texture along two axes. |
| Remove Seams On UV | Removes texture seams between polygons. |
| Rectangular UV | Makes the UV of each polygon rectangular, if false UV will match the shape of the polygon. |

<br />

### UV  
You only need to turn on UV if you want to use some texture on the path meshes, such as a dotted line.   
If you just use a pure color, UV is not necessary.   
Maximum performance can be achieved by disabling UV creation.  

![SPT_19](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/172b7dcf-1ad9-4923-bd7f-81fb0819d3ee)

**Removing Seams**  
Seams at texture are UV related. There are many ways to remove seams, with their own advantages and disadvantages.   
Enabling the "Remove Seams On UV" option should solve all problems, but with this method the texture on the path segments may be deformed, the deformation can be corrected by adding rounded corners.     
If "Remove Seams On UV" is enabled but "Rectangular UV" is disabled, the UV will follow the shape of the polygons, in some cases this approach gives better results.   
Seams can also appear if you have a Scale UV in the material other than 1, if you need a scale, use the Scale UV parameter in the actor.  

<br />
<br />

## Functions Description  
The plugin includes a total of 32 functions, below is a brief description and examples of use.

Add functions screen /**/  

**Description of common parameters:**    
| **Parameter** | **Description**  |                                                                                   
|---------------|------------------|
| PathPoints | Array of path points. |
| bLoopPath | Loops the path. |
| Thickness | Half of the line thickness. |
| Offset | Offset vertexes from the center, offset works even if the path is not closed. |
| bEnableUV | Enables UV creation, enable if you want a unique texture on the meshes of your path, not just a color. |
| ScaleUV | Scale UV on two axes, use to, for example, make dashes more frequent or sparse. |
| OffsetUV | Shifts the UV, use to move the texture to the side or away from the center of the path meshes. |
| bRemoveSeamsOnUV | Removes texture seams between polygons. |
| bRectangularUV | Makes the UV of each polygon rectangular, if false UV will match the shape of the polygon. |

<br />

**GetPathData**  
Calculates the data for a regular path.  
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the Procedural Mesh to create a path in the editor or in runtime.

<br />

**GetVerticalPathData**  
Calculates the data for a vertical path.  
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in runtime.

| **Parameter** | **Description**  |                                                       
|---------------|------------------|
| Height | Height of the geometry. |
| Offset | Offset the entire path vertically. |

<br />

**GetDottedPathData**    
Calculates data for a path consisting of individual polygons.    
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in runtime.    

| **Parameter** | **Description**  |                                                                              
|---------------|------------------|
| Interval | Distance between polygons. |
| Length | Polygon length. |
| Width | Width of the polygon. |
| DotDirection | Allows you to rotate the texture direction by 90 degrees, takes values from 0 to 3. |
| AddLastDot | If true will create a point at the last point of the path. |

<br />

**GetPathWithCornersOffsetData**  
Calculates data for a path with indents in the corners.   
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in runtime.  

<br />

**GetStartPathSegment**  
This function will be useful if you want to attach some object to the beginning of the path and adjust its offset relative to the beginning of the path.  
The function returns the parameters of the first segment of the path, the coordinates of the shifted point lying on the same line with the initial segment.  
Use the StartOffset parameter to move the first point of the path along the first segment of the path.  
Rotation allows you to rotate some object so that it is always rotated to the same place as the first part of the path.  
Direction will help you find an additional displacement along the segment, perpendicular to it, or calculate another Rotation.  

<br />

**GetEndPathSegment**  
Same as GetStartPathSegment only for the last segment of the path.   

<br />

**RoundingPathCorners**  
Rounding the corners of the path.  
The Radius parameter determines the strength of the rounding, and the Segments parameter determines how many polygons will be created at each corner.  
With Segments = 1 it works like a chamfer, just cutting corners, Segments = 8-16 is enough to make smooth and rounded corners.  
It is also handy to use with a small Radius and a value of 1 for Segments to trim very long sharp corners that can occur with sharp path turns.  
bLoopPath in this case looping means that two rounded corners will be added between the first and last point of the path.  

<br />

**GetPathLength**  
Returns the length of the path.  
Can be used to measure distance.  

<br />

**LimitPathByDistance**  
Returns a path bounded by the given distance, all points that are outside the distance will not be included in the final array.  
Can be used to limit the maximum length of the path you want to display.  
It can also be used to animate gradually filling the path.  

<br />

**LimitPathByPercent**  
Same as LimitPathByDistance, but the value varies between 0 and 1, with 0 being the beginning of the path, 1 being the end of the path, and 0.5 being the middle of the path.  
Handy to use if you don't know the length of your path, or only need to draw a certain percentage of the path.  

<br />

**GetPointAlongPath**  
Not to be confused with GetPointsAlongPath.  
Returns the coordinates of a point at a given distance along the path.  
It is convenient to use to move an object along the path or to bind to it.  

<br />

**GetPointAlongPathPercent**  
Same as GetPointAlongPath but changes the value from 0 to 1, 0 is the beginning of the path, 1 is the end of the path, 0.5 is the middle of the path.  
Handy to use if you don't know the length of your path, or need to get the coordinates of the middle or part of the path as a percentage.  

<br />

**MergePathPoints**  
Merges path points that are closer together than MergedDistance.  
If your path has consecutive points with the same coordinates, this function will remove them.  
You can also use this function for optimization, if you have clusters of points along the path, you can combine them into one and then, for example, round the corners.  

<br />

**OffsetPathPoints**  
Shifts all waypoints outward or inward.  
Convenient to use for shifting a closed boundary outward or inward.  
Self-intersections are not taken into account, so large bias values may lead to unexpected results.  

<br />

**SplitVectorArray**  
A helper function that splits a Vector array into two: a Vector2D array and a Z coordinate array of each point.  
Given the features of cycles in blueprints, this function just works much faster if you want to convert a Vector to Vector2D.  

<br />

**CombineVectorArray**  
The same as SplitVectorArray but in reverse, it combines it into one array.  

<br />

**GetPointsAlongPath**  
Not to be confused with GetPointAlongPath.  
Returns an array of points along the path taken at a given distance from each other.  
Handy to use if you need to set something up along the path at a certain distance.  

<br />

**GetPointsAlongPathDirected**  
Same as GetPointsAlongPath,but in this case it also returns the direction of each point.  
It will be useful for 3D paths, when path segments can be directed up or down.  

<br />

**FixVerticalPathPoints**  
Function for correcting points that are vertically on top of each other (X and Y coordinates coincide), this function moves points away from each other along the path by a specified distance.  

<br />

**AlignPathPointsInHeight**  
Makes the Z coordinate of all points in the path equal to the Height value.  
Convenient if you need to align all points in a horizontal plane  

<br />

**RemovePathPointsLyingOnLine**  
If several points of your path lie on the same straight line, they will be deleted.  
 Convenient to use to optimize your path before using more expensive functions such as corner rounding.  

<br />

**AddPathCornersOffset**  
Adds two points at a given distance to each corner of the path, the corner point itself is deleted.  

<br />

**CombinePathsData**  
Properly merges the vertexes, triangles, and UV coordinates of two paths.  
 To avoid creating two procedural meshes, or to avoid creating two sections of a procedural meshes, you can merge the datum. Or to use the same material or to reduce the number of drogues.  

<br />

**TrimPathFromStart**  
Cuts the beginning of the path by the specified distance.  

<br />

**TrimPathFromEnd**  
Trims the points at the end of the path by the specified distance.  

<br />

**RemoveSmallSegmentsCloseToEnd**  
Deletes all closely spaced points that are at the end of the path.  
Can be used to accurately position the end of the path.  

<br />

**RemoveSmallSegmentsCloseToBothEnds**  
Removes all closely spaced points located on both sides of the path.  
Can be used to accurately position track ends.  

<br />

**TrimPathComplex**  
Cuts the path on both sides.  

<br />

**GetQuadData**  
Returns the data to create a unit square of the specified size.  
Can be used to create more advanced start and end of path elements.  

<br />

**FindCornerMidDirection**  
Returns the unit vector of the midpoint of the angle formed by the three points, P2 the corner point.  

<br />

**GetVertexColorData**  
Returns an array of vertex colors for the dynamic mesh.  
Used to create a color path and transparency.  

| **Parameter** | **Description**  |  
|---------------|------------------|  
| Enable Start Opacity | Enables transparency at the beginning of the path. |
| Start Distance | The distance at which the path will be transparent. |
| Enable End Opacity | Enables transparency at the end of the path. |
| End Distance | The distance at which the path will be transparent. |
| Enable UV | Enables UV creation, enable if you want a unique texture on the meshes of your path, not just a color. |
| Color Curve | Color gradient, the path will be colored in the colors of this gradient. |
| Unit Curve | If true, then the Color Curve colors will be taken in the range from 0 to 1, regardless of the path length. The beginning of the path to the 1st end of the loop will be colored in color 0. If false, the Color Curve will be taken from 0 to the maximum path length, useful if you want the path to change color only at a certain distance. |
| Hardness | Transparency blur strength. |
| Default Color | If Color Curve is not connected, this color will be used for the entire path. |  

<br />

**SplitPath**  
Divides the path into two parts, at a specified distance.  

<br />
<br />

## Materials  
The asset includes three main materials, which are located in the Materials > Masters folder.  
All other materials are instances of these 3 materials.  
| **Name** | **Description**  |  
|----------|------------------|  
| M_SPT | Main material with animations. |
| M_SPT_Translucent | Material that is used to create transparency at the beginning and end of the path. |
| M_SPT_Vertex | Material for creating multi-colored paths with transparency using vertex color. |
  
<br />
  
**Main Material Parametrs**  
  
![SPT_12](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/ce4e60c8-1b4a-4b11-8ebf-4cb1c272150e)  
  
| **Parameter** | **Description**  |  
|---------------|------------------|  
| Color | Material color. |
| Emissive | Glow strength. |
| Opacity | General material opacity. |
| Alpha | Opacity mask. |
| Alpha Contrast | Mask contrast, 0 - no effect, negative values invert the mask, larger values make the edges of the mask sharper. |
| ScaleUV_X | Texture tiling along the X axis. |
| ScaleUV_Y | Texture tiling along the Y axis. |
| Move Animation | Enables texture movement along the X or Y axis (or both). |
| Scale Animation | Enables texture scaling animation. |  

The animation parameters are responsible for the movement or scaling of the texture, see how you can use these parameters in examples of materials with animations.  
  
  
To increase the brightness of the glow, you can increase this value when changing the color of the material or adjust the Emmisive values   
(Also, the brightness of the glow may depend on the post-processing settings)  
  
![SPT_11](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/42d25663-759b-4d3b-9ea5-1512e1cb2d2a)  
  
  
**Visibility Through Objects**  
To make the path visible through other objects, enable this option in the material settings:  
  
![SPT_10](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/a640201d-6d6a-47ce-9297-289032150479)
  
  
**Material Optimization**  
For convenience and versatility, translucent mode and the 2 sided option are enabled by default for all materials.   
If you don't need opacity, switch it to Opaque mode, this will have a positive effect on performance.   
  
![SPT_08](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/a9e39b28-ba08-48b4-879e-670fd5fa90b2)
  
  
If you never see the backside of path polygons, disable the 2 Sided option, this will also improve performance.  
  
![SPT_09](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/950f9343-ea2b-4c3c-abd4-961b478897e8)
  
  
Materials can cause similar artifacts, when part of the texture from one side becomes visible from another.  
  
![SPT_13](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/5dd2c31a-e7a2-4d9d-ba3d-b8628cd32069)
  
This is due to texture repeating, you can turn it off in the texture settings, but the texture will no longer tile.  
  
![SPT_14](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/01797c37-5c8e-4946-af62-c761602993fd)
  
  
<br />
<br />

## Features and Tips  
### Migrate  
You can migrate assets from the Demo Project to your project as follows:  
1. Select the necessary assets.  
2. Select Migrate, all dependent assets that will also need to be migrated will be marked here. 
    
![SPT_18](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/b91ab1d3-5609-4a26-83ce-c1654b08bc47)
  
3. Select your project "Content" folder.  
  
<br />
  
**Performance**
Performance is directly related to the number of points in your array.  
So the sequence of function calls matters, for example it is better to trim the path first and then round the corners.   
The sequence of functions also affects how it will look, experiment, just keep in mind that functions that add a lot of points are better called last.  

**SPT is designed to draw the path mainly in 2D**  
The plugin can draw in 3D, but there are some peculiarities.    
If the path points are evenly spaced (X and Y coordinates are the same) a section of the path may not be displayed or may be rotated incorrectly, to solve this problem there is a function "Fix Vertical Path Points", it automatically adds an adjustable indentation along the path to avoid this problem.    
If you want to draw something in a different plane, you can draw a horizontal path and then just rotate the entire actor itself to the plane you want.    

**Disappearing path segments**  
If a segment of the path is not displayed, it is likely that you have two consecutive points that have the same or very close coordinates.  
You can fix this by using the Merge Waypoints function, which finds and removes duplicate points.   

**Creation Static Mesh**  
If necessary you can bake the path into a single mesh, this is a much more productive solution if you want to use SPT as static objects spaced out by the drop.
There are 2 main ways to bake a path. 
First way, you can do it through the engine function, just run for UE4: for UE5:
The second way will bake only the path itself, without start and end placeholders, just select the SPT actor on the scene, select the procedural mesh, in its settings click and "Create Static Mesh" and choose where to save

**Working with arrays**   
You can also use Unreal functions to work with arrays.
For example the Reverse function will reverse the order of the points, this can be useful if it is important at which end of the path the path starts to be drawn (for example, if you want the path to remain static when the character moves along it).
The Remove Index function will help you to remove, for example, the first or the last point of the path, it can be useful if for some reason you don't need these points or they are in the way.
The "Get Vector Array Average" function will help you find the geometric center among all your points.

**Path Tracer Toolkit**  
You can also check out my other Path Tracer Toolkit Asset (link)  /**/  
Path Tracer Toolkit is a 100% blueprint asset, and more focused on visual style, while this asset is more focused on optimization and customization.  
This asset will suit you if you need a more optimized solution, for example if you need to draw many paths or with many points.  
  
<br />
<br />

## Demo Project
Demo Project (for UE versions 4.6 - 5.3)  
link  /**/   

All gameplay logic in the Demo project is located inside the Demo_Player_Controller.

Before you can open the Demo Project you need to enable the plugin for your engine version ([read more](#Quick-Start)).   
You can migrate the entire level with examples or individual examples from Demo Project to your project using migrate ([read more](#Migrate)).  
