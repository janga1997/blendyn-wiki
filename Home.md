Welcome to the **Blendyn** wiki!  

![Blendyn Logo](https://raw.githubusercontent.com/wiki/zanoni-mbdyn/blendyn/images/blendyn_logo_subtitle_big.png)

**Blendyn** is a postprocessing tool that helps creating 3D animations from 
multibody simulation result files.

**Blendyn** was formely known as **mbdyn-blender**: what would have been 
version 1.5.0 of **mbdyn-blender** was renamed **Blendyn**.

**Blendyn** is a [Blender][1] add-on, written in
Python, that allows to import the output of the
[free](http://www.gnu.org/philosophy/free-sw.html), general purpose multibody solver
[MBDyn][2] developed at the [Department of Aerospace Science and Technology](http://www.aero.polimi.it/) of [Politecnico di Milano
University](http://www.polimi.it/). [MBDyn][2] does not
come with a built-in graphical pre- or post-processor, as it is able to process
text-only input files and generates either text or binary (in
[NetCDF](http://www.unidata.ucar.edu/software/netcdf/) format) output. The
purpose of the **Blendyn** add-on is to exploit the numerous features of
the 3D graphics software [Blender][1] to post-process
[MBDyn][2] output data. The add-on is, therefore, strictly
a post-processor, but the goal is to make it as useful as possible also during
the model definition phase.

Viewed from the perspective of the [Blender][1] user, **Blendyn** is an add-on
that provides the ability to animate a 3D model in a totally physics-based way,
provided one has a strong motivation in learning how to build an [MBDyn][2]
model for this purpose :)

Please note that in the current state, the add-on is not complete,
especially regarding the visualization of [MBDyn][2]
*elements*, i.e. algebraic joint, deformable components,
aerodynamic/hydraulic/electrical systems, and so on. Any feedback, help, feature
request is welcomed but please be aware that the project is currently maintained
by a single developer (yes, that would be me). So...

---
> *Patience is the calm acceptance that things can happen in a different order
> than the one you have in mind.*
>
>                                                            David G. Allen
---

# **Blendyn** Change Log

## [1.0.0]
**Blendyn** is born! Would-have-been version 1.5.0 of **mbdyn-blender** has officialy been
renamed **Blendyn** (version 1.0.0) and given a sleek new logo!

Changes with respect to **mbdyn-blender** version [1.4.0]

### Added
- Support for Eigenanalysis results visualization
- Support for revolute hinge, revolute pin, cardano hinge, cardano pin, clamp,
  spherical hinge, spherical pin, total joint, total pint joint elements
- Plotting of variables autospectra

### Changed
- Re-written animation function with great speed improvements
- Menu panel organization modified: the addon menu in the View3D toolbar now is
  under the "MBDyn" tab
- Cleaned code naming conventions

### Fixed
- Lots of small bugs!

# **mbdyn-blender** Change Log
NOTE 1: this changelog has been added upon the release of version 1.3
	of the addon. Previous changes are untracked.

## 2017-01-17
The Projects has been Renamed **Blendyn** and given a sleek new logo!

## [1.4.0] - 2016-05-09

### Added
- Support for beam2, beam3, shell4 elements
- Support for NetCDF output
- Plotting tools
- Visualization of simulation time
- Range import for nodes
- Ability to import all elements of a ceirtain type together
- Operator to load cross-section profiles for rod and beam elements
- Wiki page with tutorials
- Input [MBDyn](https://www.mbdyn.org) files for tutorials models in tests/ directory

### Changed
- Re-written animation function
- String labels are now searched and loaded from the .log file
- Menu panels re-styling with some labels changed, etc...
- Written *skeleton* .py files for some elements 
  (to be completed in future versions)

### Fixed
- Various small bugs in element import

## [1.3.1] - 2015-12-30

### Added
- Selection of Blender object to be used for automatic import of nodes

### Changed

### Fixed
- Bug in the import of orientation when matrix output is selected for
  nodes;
- Bug in re-parsing the log file after a model update;
- Bug in the loading of an empty .mov file;

## [1.3.0] - 2015-12-10

### Added
- Automatic import for all MBDyn nodes at once;
- selection of labels file with basename different from the results'
  file basename;
- visualization of MBDyn nodes list in the Scene Properties panel;
- basic documentation in README (to be extended greatly).

### Changed
- Basic MBDyn model structure import has been rewritten and it is 
  now based entirely on the .log file of the simulation output, thus
  easing the visualization of models that fail during the assembly 
  phase;
- element list in the Scene Properties panel is now shown as a UI 
  List, with the same layout of the nodes list;
- the nodes list in the Object Properties panel now shows an "ADD"
  button to import for nodes that are not yet imported in the scene;
- the element import has been structured in the code: the addition
  of an element support to the addon can now be done in an organized
  way;

### Fixed
- Bug in setting the correct rotation parametrization for nodes;
- Various error and warning messages appearance


  [1]: https://www.blender.org/
  [2]: https://www.mbdyn.org/
  [logo]: images/blendyn_logo_subtitle_big.png "Blendyn: power MBDyn with blender graphics; power blender with MBDyn physics!"
