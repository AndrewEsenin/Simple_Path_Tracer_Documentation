# Simple Path Tracer Documentation
Unreal Marketplace Link  
YouTube  

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

![SPT_05](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/5067783b-38f0-4d1b-a77f-d4a083f8d7f7)

  
You can also create it, or classes inheriting from it, during the game.  

![SPT_06](https://github.com/AndrewEsenin/Simple_Path_Tracer_Documentation/assets/150374215/a9567161-468e-4f83-9db1-eea010773325)


## Functions Description:
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


**GetPathData**
Calculates the data for a regular path.  
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the Procedural Mesh to create a path in the editor or in rantime.


**GetVerticalPathData**
Calculates the data for a vertical path.  
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in rantime.

| Height | Height of the geometry |
| Offset | Offset the entire path vertically |


**GetDottedPathData**
Calculates data for a path consisting of individual polygons.   
Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in rantime.  

| Interval | distance between polygons |
| Length | Polygon length |
| Width | Width of the polygon |
| DotDirection | Allows you to rotate the texture direction by 90 degrees, takes values from 0 to 3 |
| AddLastDot | If true will create a point at the last point of the path |


**GetPathWithCornersOffsetData**
Calculates data for a path with indents in the corners. Returns arrays with vertex, triangle and UV coordinates, connect these arrays to the "Create Mesh Section" function of the procedural mesh to create a path in the editor or in rantime


**GetStartPathSegment**
This function will be useful if you want to attach some object to the beginning of the path and adjust its offset relative to the beginning of the path.
The function returns the parameters of the first segment of the path, the coordinates of the shifted point lying on the same line with the initial segment.
Use the StartOffset parameter to move the first point of the path along the first segment of the path.
Rotation allows you to rotate some object so that it is always rotated to the same place as the first part of the path.
Direction will help you find an additional displacement along the segment, perpendicular to it, or calculate another Rotation.


**GetEndPathSegment**
Same as GetStartPathSegment only for the last segment of the path.


**RoundingPathCorners**
Rounding the corners of the path.
The Radius parameter determines the strength of the rounding, and the Segments parameter determines how many polygons will be created at each corner.
With Segments = 1 it works like a chamfer, just cutting corners, Segments = 8-16 is enough to make smooth and rounded corners.
It is also handy to use with a small Radius and a value of 1 for Segments to trim very long sharp corners that can occur with sharp path turns.
bLoopPath in this case looping means that two rounded corners will be added between the first and last point of the path


**GetPathLength**
Returns the length of the path
Can be used to measure distance


**LimitPathByDistance**
Returns a path bounded by the given distance, all points that are outside the distance will not be included in the final array.
Can be used to limit the maximum length of the path you want to display.
It can also be used to animate gradually filling the path.


**LimitPathByPercent**
Same as LimitPathByDistance, but the value varies between 0 and 1, with 0 being the beginning of the path, 1 being the end of the path, and 0.5 being the middle of the path.
Handy to use if you don't know the length of your path, or only need to draw a certain percentage of the path.


**GetPointAlongPath**
Not to be confused with GetPointsAlongPath.
Returns the coordinates of a point at a given distance along the path.
It is convenient to use to move an object along the path or to bind to it.


**GetPointAlongPathPercent**
Same as GetPointAlongPath but changes the value from 0 to 1, 0 is the beginning of the path, 1 is the end of the path, 0.5 is the middle of the path.
Handy to use if you don't know the length of your path, or need to get the coordinates of the middle or part of the path as a percentage.


**MergePathPoints**
Merges path points that are closer together than MergedDistance.
If your path has consecutive points with the same coordinates, this function will remove them.
You can also use this function for optimization, if you have clusters of points along the path, you can combine them into one and then, for example, round the corners.

**OffsetPathPoints**
Shifts all waypoints outward or inward.
Convenient to use for shifting a closed boundary outward or inward.
Self-intersections are not taken into account, so large bias values may lead to unexpected results.


**SplitVectorArray**
A helper function that splits a Vector array into two: a Vector2D array and a Z coordinate array of each point.
Given the features of cycles in blueprints, this function just works much faster if you want to convert a Vector to Vector2D.


**CombineVectorArray**
The same as SplitVectorArray but in reverse, it combines it into one array.


**GetPointsAlongPath**
Not to be confused with GetPointAlongPath.
Returns an array of points along the path taken at a given distance from each other.
Handy to use if you need to set something up along the path at a certain distance.


**GetPointsAlongPathDirected**
Same as GetPointsAlongPath,but in this case it also returns the direction of each point.
It will be useful for 3D paths, when path segments can be directed up or down.


**FixVerticalPathPoints**
Function for correcting points that are vertically on top of each other (X and Y coordinates coincide), this function moves points away from each other along the path by a specified distance.


**FixVerticalPathPoints**
Makes the Z coordinate of all points in the path equal to the Height value.
Convenient if you need to align all points in a horizontal plane


**RemovePathPointsLyingOnLine**
If several points of your path lie on the same straight line, they will be deleted.
 Convenient to use to optimize your path before using more expensive functions such as corner rounding.


**AddPathCornersOffset**
Adds two points at a given distance to each corner of the path, the corner point itself is deleted.


**CombinePathsData**
Properly merges the vertexes, triangles, and UV coordinates of two paths.
 To avoid creating two procedural meshes, or to avoid creating two sections of a procedural meshes, you can merge the datum. Or to use the same material or to reduce the number of drogues.


**TrimPathFromStart**
Cuts the beginning of the path by the specified distance


**TrimPathFromEnd**
Trims the points at the end of the path by the specified distance


**RemoveSmallSegmentsCloseToEnd**
Deletes all closely spaced points that are at the end of the path.
Can be used to accurately position the end of the path.


**RemoveSmallSegmentsCloseToBothEnds**
Removes all closely spaced points located on both sides of the path.
Can be used to accurately position track ends.


**TrimPathComplex**
Cuts the path on both sides.


**GetQuadData**
Returns the data to create a unit square of the specified size.
Can be used to create more advanced start and end of path elements.
FindCornerMidDirection
Returns the unit vector of the midpoint of the angle formed by the three points, P2 the corner point.


**GetVertexColorData**
Returns an array of vertex colors for the dynamic mesh.
Used to create a color path and transparency.


**SplitPath**
Divides the path into two parts, at a specified distance.

  

