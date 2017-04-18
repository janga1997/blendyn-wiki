# Rigid crank-slider

- - - 
*NOTE: This tutorial was realized using an older version of the mbdyn-blender
(Blendyn predecessor) add-on.  Thus, part of if might be outdated now and some
commands might have slightly changed. It will be updated soon, but in the
meantime, we're confident that you can find your way through the different bits! 
If you have troubles, please use the 
[Issues](https://github.com/zanoni-mbdyn/blendyn/issues) section to let us now.*
- - - 

## TUTORIAL 1. Rigid Crank Slider.
In this tutorial we will animate the slide-crank-piston models available at
[this link][2], or in the repository of the **Blender** add-on, in the
directory `tests/slidercrank`. We're going to go through the model building and
animation assuming that we'd like to model the dynamic behavior of the real
system, by following these steps:
- start from a CAD model of the mechanical system;
- tune the [MBDyn][1] model to fit the mechanical system;
- run the multibody simulation;
- set up a [Blender][6] model to visualize the results in a simple way;
- enhance the [Blender][6] model by importing the CAD files as meshes;
- render the animation. 

## Step 1: The CAD model
We're going to use a publicly available CAD model of a slider-crank-piston
mechanical assembly as our reference. I'm using the very nice model by
**thinkin3D** available here: [engine starter kit][3].  If you want to follow
this tutorial exactly step-by-step you can register a free account at
[GrabCAD][4] and download it for free. I suggest using the
`.stp` version, but you can download the one that suits the CAD software you're
most comfortable with. 

If you open the .stp file in [FreeCAD][5], you can see
that the CAD assembly is made of 12 parts. We want to export the parts that
we'd like to animate in a mesh format that [Blender][6]
can import and measure some geometrical and inertial parameters of the model. 

---
[![Slider-crank-piston CAD .stp model imported in FreeCAD][scfcad]][scfcad]
---

To measure volumes and moments of inertia we'll make use of the macro
[FCinfo][7], developed by **Mario52**. 

Load [FCinfo][7] and click on the crankshaft part: you'll get a lot of
information about its geometry, that you can export to a text file with the
**Save** button. For example, you can see that the total volume of the
crankshaft is about 99842&nbsp;mm<sup>3</sup> and that its moment of inertia with
respect to the FreeCAD *x*-axis is about 54859396&nbsp;mm<sup>5</sup>. The units of
the moment of inertia might confuse you, but remember that FreeCAD doesn't know
anything about the material the crankshaft is made of: therefore,
[FCinfo][7] outputs the moment of inertia divided by the density. We'll assume
that the crankshaft is made of SAE 4340 alloy steel (typically used for
crankshafts and rods). Its density is 7800 kg/m<sup>3</sup>. Thus we obtain a
moment of inertia J<sub>xx</sub> of 427,9&nbsp;·&nbsp;10<sup>-6</sup>&nbsp;kg&nbsp;m<sup>2</sup>,
and a mass of about 0.779&nbsp;kg. The last piece of information that we need is the
crank *length*, i.e.  the distance between the rotation axis of the crankshaft
and the center of the hinge that connects it to the rod. You can also perform
this measurement in FreeCAD (or any other CAD software) and find it to be about
19 mm.

The last thing that we want to do with the crankshaft is to output its model to
a mesh format for the import in [Blender][6]. To do so, click on the Crankshaft part,
go to File->Export and choose Mesh format. I've chosen to call in `crank.stl`.
Using the `.stl` extension will tell FreeCAD to export the file in
the STL format, which [Blender][6] can understand.

Repeat the process for the rod (which is composed of the `combo002`, `combo003`,
`combo004` and `combo005` parts in the FreeCAD model), for the piston
(`combo001`), that we'll assume is made of forged aluminum, with
2700&nbsp;kg/m<sup>3</sup> density, and for the wristpin (`combo`). You should
get the following table of parameters: 

Part | Mass [kg] | Length [m] | Moment of Inertia [kg m<sup>2</sup>]
-----|-----------|------------|-------------------------------------
Crankshaft | 0.779 | 0.019 | 427.9 · 10<sup>-6</sup>
Rod | 0.065 | 0.076 | 34.7 · 10<sup>-6</sup>
Piston + Wristpin | 0.078 | - (immaterial) |- (immaterial)

[FCinfo][7] also reports the position of the center of mass of the part. We
thus learn that the center of mass (CoM) of the crank is located, quite conveniently, 
approximately at the intersection between the rotation axis of the crankshaft
and its symmetry plane. The CoM of the rod is located along the line connecting
its two hinges centers, at a distance of circa 52 mm from the piston hinge
center.

The piston's length and moment of inertia play no role in this multibody
simulation, since the piston does not rotate during its motion.

(To be perfectly honest, the mass of the crankshaft is immaterial for the
simulation results, too. You may want to apply it anyway, though, for example
to investigate the effects of a crankshaft that is not perfectly balanced. Simply
offset the crank CoM from the crankshaft rotation axis.... But I'm going off
on a tangent, here.)

We have now exported all the parts that we need we have a collection of 4 `.stl`
files. My files are the following: 

- crank.stl
- rod.stl
- piston.stl
- wristpin.stl

It's time to simulate the [MBDyn][1] model and import the simulation results in
[Blender][6].

## Simulation and basic visualization
You can find the original [MBDyn][1] model [here][2]. To take into account the
inertial properties that we have estimated and to facilitate the visualization
in [Blender][6], you can use the slightly modified file `slidercrank.mbd`
that you can find in the `test` directory of the repository. 

To speed up the import of the results and enable additional features (like
plotting), you can uncomment the
```
output results: netcdf;
```
line in the `control data` section of the input file. See the [installation
instruction](https://github.com/zanoni-mbdyn/blendyn/wiki/Installation#optional-packages)
for optional packages for the details.

After running the simulation and following the steps in the above sections,
choose to automatically import all the nodes to the [Blender][6] scene by
clicking on `Add nodes to scene` button in the scene properties panel.
Simplified representations for joints can be added also, by selecting them in
the `MBDyn elements list` in the scene properties panel and click on `Add
element to the scene`, for example. You should end up with a scene similar to
the one in the picture below, when viewed from the positive *z*-axis:

---
[![Blender scene after automatic import][aimp]][aimp]
---

The MBDyn simulation was run with a 10<sup>-3</sup> s timestep for 10 seconds,
resulting in 10000 timesteps. We want to animate the results at 25 fps, so we
set 40 (1000/25) in the frequency parameter before importing the results with
the "Animate scene" button.

We now have a very simple animation of our model (that we could use to debug the 
[MBDyn][1] input file, for example). We'll use this collection
of Blender objects as the skeleton of our animated model. Our next step is now
to import the mesh files that we previously converted in [FreeCAD][5].

## Importing the CAD model meshes

First of all, click on a new layer in the Blender scene: we'll keep the
*dressed* model completely separated from the *skeleton* model that we have
automatically imported.

Now go to File->Import->Stl (`.stl`) and select the crankshaft file. Notice that
[FreeCAD][5] uses millimeters as defaults units, while we used meters in [MBDyn][1]. 
The mesh model that we have just imported has thus to be scaled down by a factor 
0.001. You'll get something similar to the following picture:

---
[![Crankshaft .stl mesh imported and scaled][scstl]][scstl]
---

You'll notice that the internal reference frame of the object used by blender
(the red, green and blue axes that appear when you select the object in Object
mode) is displaced quite a bit from the object mesh. We want this reference
frame (henceforth R.F.) to be coincident with the crank [MBDyn][1] node, that is
represented by the empty arrows object called `NODE_CRANK` in my scene.

First of all, let's place the internal Blender R.F. in a more convenient place
for us. Hit `Tab` to enter in edit mode and you'll notice that the mesh R.F. is
in the center of the mesh. Hit `Shift + S` and select "Cursor to Selected" to
move the 3D cursor of Blender to the center of the mesh R.F. Exit edit mode and
hit `Shift + Ctrl + Alt + C` and select "Origin to 3D Cursor". The object R.F.
center will be moved. Now you can set the location of the crank object to be (0,
0, 0) in the Transform panel, for convenience. 

We want the *z*-axis of the Blender R.F. to be aligned with the rotation axis of
the crankshaft, and its *x*-axis to point away from the counterweights. Rotate
the object by -90° about the *y*-axis and apply the rotation
with `Shift + A`. The mesh seems also slightly rotated about the *z*-axis, so I've
applied a further rotation of -1.8° about *z*.

Now we want to place the R.F. origin in the correct place with respect to the
mesh. Remember that we placed the [MBDyn][1] node associated with the crank
midway between the crank axis and the crankpin center. 

The way I accomplished this is as follows:

1. `Tab` into edit mode and select the faces on the outside edge of the crankshaft, as shown in the picture below

--- 
[![Select the vertices on the edge face of the crankshaft][vertssel]][vertssel]
---

2. hit `X` and select "Faces" to delete the faces inside the circle
3. select the vertices on the circumference again
3. hit `F` to fill the circle with an n-gon
4. hit `Alt + P` to triangulate the n-gon with a central vertex.
5. select the central vertex, hit `Shift + S` and select "Cursor to Selected"
6. `Tab` to exit edit mode and hit `Ctrl + Shift + Alt + C` and then select
   "Origin to 3D Cursor"
7. set the location of the object to 0 in *x* and 0 in *y*. **Leave *z* as it
   is**.
8. set the cursor location to 9.5 mm in *x*, 0 in *y* and 0 in *z*
9. hit again "Ctrl + Shift + Alt + C" and select "Origin to 3D Cursor"

You should now have something similar to what is depicted below:

---
[![Final configuration of the crank object][final]][final]
---
You can follow similar steps to place the Blender reference frames in the
correct positions with respect to the meshes. Now we want to assemble the meshes
and animate them.

## Assembling the meshes

Let's again start from the crank. Select the first layer, where the empties are
located, and select the `NODE_CRANK` empty object. Hit `Shift + S` and select
`Cursor to Selected`. Change layer and select the `crank` object. Hit again
`Shift + S` and this time select `Selection to Cursor`. Now the crank mesh is in
the correct position. Check the orientation of the `NODE_CRANK` empty: it says
0° about *x*, 0° about *y* and 180° about *z*. Apply the same rotation to the
`crank` object, and we're set. Check that the internal blender R.F. of the
`crank` and the `NODE_CRANK` empty are now aligned perfectly, by activating 
both the layers that we've worked on. 

Now deselect all by pressing `A`, select the `crank` object first and the
`NODE_CRANK` empty second (the order is important!) and then hit `Ctrl + P` and
choose `Set parent to object`. Now the movement of the `crank` object is tied to
the one of the `NODE_CRANK` object, that we already imported from [MBDyn][1]
results. If you play the animation, you should see the crank rotating about the
*z* axis. 

You can now repeat the process for the `rod` and `piston` objects. Notice that
you can parent the `wristpin` object to the `piston` object directly, since
no [MBDyn][1] node is associated to that component.

Your [Blender][6] scene should now look like this

---
[![Final configuration of the Blender scene][final]][final]
---

You can simply play back and forth the animation in Blender, or assign the
objects some materials and render the frames into a video file, like I did to
generate this .gif:

---
[![Animation of the rendered Blender model][anim]][anim]
---

Happy simulations!

  [1]: http://www.mbdyn.org
  [2]: https://www.mbdyn.org/?Documentation___Official_Documentation___Examples
  [3]: https://grabcad.com/library/engine-starter-kit-1
  [4]: https://grabcad.com/
  [5]: http://www.freecadweb.org/
  [6]: https://www.blender.org/
  [7]: http://www.freecadweb.org/wiki/index.php?title=Macro_FCInfo
  [scfcad]: images/tutorials/slidercrank/fc_asm_1.png "Slider-crank-piston CAD .stp model imported in FreeCAD"
  [aimp]: images/tutorials/slidercrank/sc_blend_ai.png "Blender scene after the automatic import of the MBDyn simulation results"
  [scstl]: images/tutorials/slidercrank/sc_blend_crank.png "Crankshaft .stl mesh imported and scaled"
  [vertssel]: images/tutorials/slidercrank/sc_blend_crank_n1.png "Select vertices on the edge face of crankshaft"
  [final]: images/tutorials/slidercrank/sc_blend_crank_n2.png "Final configuration of the crank object"
  [anim]: images/tutorials/slidercrank/sc-animation.gif "Animation of the rendered Blender model"
