# Beam elements

Beam elements are imported as 3D curves, representing the reference line of the
finite volume elements. An additional button labeled `Import profile (Selig)` is
activated for every beam element in [Blender][1]'s `Data Properties` panel. It
allows the automatic import and assignment of a cross-section profile to the beam
curve.

## 3-node beams
The reference line for a 3-node beam is a curve of degree 2 in space, passing by
the three points defined with respect to the 3 nodes that the beam element
connects. To represent it in an accurate and flexible way in [Blender][1], a
[NURBS][2] order 3, degree 2 curve is used. 

The curve control polygon is made of 4 vertices and 3 sides. The first and last
control points define the begin and end point of the curve, and are directly
connected to the [Blender][1] objects the relative [MBDyn][3] nodes are
associated to. The two internal control points are instead associated to two
new objects, spawned when the element is imported to the scene. You will notice
them in the Scene Outliner in the top right part of the [Blender][1] interface,
having the same name of the curve object with `_M1` and `_M2` appended. They are
by default hidden from the 3D view. 

The position of the two intermediate vertices is automatically computed during
the animation of the scene. However, it will not be recomputed automatically
when you move the object belonging to the middle node in the scene. You can
update the visualization of the curve by hitting the `Update configuration`
button in the Data Properties panel. 

- - - 
[![beam panel in data properties][beampan]][beampan]
- - - 

When a beam element is imported, a group is created containing all the objects
that belong to that element: the curve object, the two objects hooked to the
intermediate control points and the three node objects.
- - -
[![beam group in scene outline][group]][group]
- - - 

### Cross-section profile import
The `Import profile (Selig)` button allows the user to load a plain text file
with the following format:

```
<Section profile name>
X[1]	Y[1]
X[2]	Y[2]
X[3]	Y[3]
...
```
where `<Section profile name>` is a tag that will be used to identify the
section profile, `X[n]` and `Y[n]` the Cartesian coordinates of the `n`-th point
on the section. An example is given in the [helicopter blade flapping analysis
tutorial][4]. 

The profile is loaded as a 2D polygonal curve in the first empty layer of the
Scene, if such an empty layer is found. Otherwise, the curve is created in the
current layer. Notice that by default [Blender][1] assumes that the section
profile object, which in [Blender][1] terminology is called [bevel object][5],
lives in the *x-y* plane, and that the curve develops along the *z* axis, so you
can consider the *z* axis of the section profile as the local tangent axis of
the curve. As usual with [bevel objects][5], scaling and moving the object's
local axes results in the scaling and re-positioning of the section profile on
the curve. 

Notice that the Selig file format is extremely general and can thus be used to
import any kind of cross-section profile, not just airfol profiles (as the name
would suggest).

## 2-node beams
2-node beam elements are imported as a straight line connecting two points
belonging to two different objects, to which [MBDyn][3] nodes are connected.
The same indications just mentioned for 3-node beams (apart from, obviously, the
`Update configuration` operator) apply to 2-node beams as well.

Also in this case a group is created, holding the curve object and the two
objects associated with the nodes the beam element connects.
  [1]: https://www.blender.org/
  [2]: https://www.blender.org/manual/modeling/curves/introduction.html
  [3]: https://www.mbdyn.org/
  [4]: https://github.com/zanoni-mbdyn/blendyn/wiki/Tutorial-2-Helicopter-Blade-Flapping-Analysis 
  [5]: https://www.blender.org/manual/modeling/curves/introduction.html#curve-properties
  [beampan]: images/elements/beam_data_panel.png "beam panel in data properties"
  [group]: images/elements/beam_group.png "beam group in scene outline"
