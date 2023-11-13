# Simple Path Tracer Documentation
Unreal Marketplace Link  
YouTube  

<br />
<br />

## Description
Simple Path Tracer is a C++ Plugin containing a set of functions for editing and drawing paths both in the editor and in runtime.  
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

<br />
<br />

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

![SPT_05](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/5067783b-38f0-4d1b-a77f-d4a083f8d7f7)

  
You can also create it, or classes inheriting from it, during the game.  

![SPT_06](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/a9567161-468e-4f83-9db1-eea010773325)

<br />
<br />

## Functions Description  
The plugin includes a total of 32 functions, below is a brief description and examples of use.

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

<br />

**SplitPath**  
Divides the path into two parts, at a specified distance.  

<br />
<br />

## Description of Blueprint Examples  
All examples are located in the plugin content folder.  
Blueprints whose name starts with "BPc_" are child classes of other blueprints, there are no logic changes, only changes to the class settings (different line thickness, different materials used, etc.).  
To find the blueprint that the BPc_ blueprint is based on, open it and click in the upper right corner:  

![SPT_07](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/225b8910-8b0a-4287-8560-8ed891113333)

List/**/

With the playne settings, you can customize their appearance and position them to coincide with the start and end of a path or curve

<br />
<br />

## Features and tips  
**Performance**
Performance is directly related to the number of points in your array.  
So the sequence of function calls matters, for example it is better to trim the path first and then round the corners.   
The sequence of functions also affects how it will look, experiment, just keep in mind that functions that add a lot of points are better called last.  

**UV utilization**
You only need to turn on UV if you want to use some texture on the path meshes, such as a dotted line. If you just use a pure color, UV is not necessary.  
Maximum performance can be achieved by disabling UV creation.  
UV creation significantly increases the amount of logic to be executed.  

**Removing seams at texture joints**
Seams at texture joints are UV related. There are many ways to remove seams, with their own advantages and disadvantages.   
Enabling the "Remove Seams On UV" option should solve all problems, but with this method the texture on the path segments may be deformed, the deformation can be corrected by adding rounded corners (screenshot).    
If "Remove Seams On UV" is enabled but "Rectangular UV" is disabled, the UV will follow the shape of the polygons, in some cases this approach gives better results. Seams can also appear if you have a Scale UV in the material other than 1.  

**SPT is designed to draw the path mainly in 2D**
The plugin can draw in 3D, but there are some peculiarities.  
If the path points are evenly spaced (X and Y coordinates are the same) a section of the path may not be displayed or may be rotated incorrectly, to solve this problem there is a function "Fix Vertical Path Points", it automatically adds an adjustable indentation along the path to avoid this problem.  
If you want to draw something in a different plane, you can draw a horizontal path and then just rotate the entire actor itself to the plane you want.  

If you do not use the function to round corners, when the angles between two path segments are very small 

If a section of the path is not displayed, it is likely that at that location in your point array, two consecutive points have the same or very close coordinates. You can fix this by using the "Merge Path Points" function, which finds and removes repeating points.

If necessary you can bake the path into a single mesh, this is a much more productive solution if you want to use SPT as static objects spaced out by the drop.
There are 2 main ways to bake a path.
first way, you can do it through the engine function, just run for UE4: for UE5:
The second way will bake only the path itself, without start and end placeholders, just select the SPT actor on the scene, select the procedural mesh, in its settings click and "Create Static Mesh" and choose where to save

**Texture Tile**
Sometimes you can observe such artifacts on the edges of polygons, when the texture becomes visible from the other edge of the polygon. To fix this, set the following parameters in the texture settings, this will disable texture tiling. So if this texture has been used elsewhere for tiling, it will stop repeating.

**Working with arrays**
You can also use Unreal functions to work with arrays.
For example the Reverse function will reverse the order of the points, this can be useful if it is important at which end of the path the path starts to be drawn (for example, if you want the path to remain static when the character moves along it).
The Remove Index function will help you to remove, for example, the first or the last point of the path, it can be useful if for some reason you don't need these points or they are in the way.
The "Get Vector Array Average" function will help you find the geometric center among all your points.

The brightness of the material can be increased or decreased by changing this parameter in the color selection: 


**Material Optimization**
For convenience and versatility, translucent mode and the 2 sided option are enabled by default in the materials.
If you don't need opacity switch it to Opaque mode, this will have a positive effect on performance.
If you are using SPT so that you never see the backside of path polygons, disable the 2 Sided option, this will also improve performance.

A procedural mesh is used to visualize the pathway.
In the Blueprint examples, a procedural mesh component has already been added to the Simple Path Trace Actor. It also has added placeholders for the start and end of the path.
This is a regular Blueprint Actor, you can freely remove or add any of your own components to it.

The data for the procedural mesh can be obtained using functions:

**Use in a sequencer**
There is a separate example for sequencer %example nym%


