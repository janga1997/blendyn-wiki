# Shell elements

Four-node shell elements `shell4` are currently imported as mesh faces, with
vertex hooked to the 4 objects associated with the [MBDyn][1] nodes the
element connects. 

- - - 
[![Shell4 element imported as mesh plane][shell4]][shell4]
- - - 

No attempt is made, at this stage, to visualize the effects of the node
rotations.

When `shell4` is selected in the `MBDyn elements list` panel in the Scene Properties
panel, a second dropdown menu is displayed, providing for the choice of importing the
elements joined as part of a single mesh object or as separated mesh objects.

- - - 
[![Shell4 import mode selection menu][shell4imp]][shell4imp]
- - - 

Please be aware that [Blender][2] is optimized to support relatively few, possibily very 
complex (i.e. having a large number of vertices) mesh objects. So if the number of 
shell elements in your model is high, you should probably import them in *batches* 
(possibily a single one, if the structure of your model allow it) by 
selecting the `Joined in single mesh` option. The elements will be imported as the (quad)
faces of a single mesh object called `shell4_MIN_MAX`, with `MIN` and `MAX` being, 
respectively, the `first element to import` and `last element to import` properties
shown in the sliders above the `Import elements by type` button.

  [1]: https://www.mbdyn.org/
  [2]: https://www.blender.org/
  [shell4]: images/elements/shell4.png "Shell4 element imported as mesh plane"
  [shell4imp]: images/elements/shell4_scene_panel.png "Shell4 import mode selection menu"
