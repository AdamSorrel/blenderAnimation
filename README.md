# Blender procedure notes

## Changing rendering from GPU to CPU in EEVEE

1. Open `Performance` > `Compositor` and switch `CPU` to `GPU`. 

## Adding bloom

In blender 5.2.2, bloom is no longer available in render engine settings. 

1. Open compositing tab (up top).
2. Create a new compositing node (Shift + A).
3. Search for `Glare` and drop it onto the wire connecting `Render layers` and `Group output + Viewport`. 
4. In the `Glare` dropdown menu, change `Streaks` to `Bloom`
5. Return to 3D view and click on the drop down arrow next to the `Viewpoert shading options` (top right corner).
6. At the bottom of the resulting menu, there is an option `Compositor` which should be switched to `Always`.
7. Select object and go to the `Material settings`. Add a new material if needed.
8. In the `Material settings` > `Surface` > `Emission` increase the strength and adjust the colour of the desired emission.

## Adjusting `Blend mode` to `Alpha blend`

This option seems to have been removed in Blender 5. The original `Alpha blend` has been replaced by the option `Blended`. 

1. Open `Shader editor`
2. Go to the vertical menu value `Options` on the right side of the screen. 
3. Change `Render method` to `Blended`.

## Adding a spiral/wave

>[!NOTE] 
> For this to work, it is important to have the `Extra Curve Objects` and `Node wrangler` activated in `Edit`>`Preferences`>`Add-ons`

Based on a [Xan 3D video](https://www.youtube.com/watch?v=dHLFU7RQrFc&t=67s) and partially on [GC Figures video](https://www.youtube.com/watch?v=WteYqkxQG9I&t=541s).

1. `Shift + A`>`Curve`>`Spirals`>`Archemedian`
2. In the bottom corner open an object tab `Curve spirals`
3. Adjust the height, number of turns, and rotation.
4. The spiral is now 3D, to get a flat curve, scale [s] X [x] to 0. 
5. To add a dimension to the curve path, go to `Data` on the right side vertical panel, then `Geometry`>`Bevel`>`Depth` and adjust accordingly.
6. Add bloom as described above. 
7. Go to shader editor (you can drag a new window from the side) and add a new material and in the vertical menu `Options`>`Render method` select `Blended`. This will make the bloom and alpha look better.
8. `Shift + A`>search `Gradient texture` and connect *color* to *alpha* on the `Principal BSDF`.
9. Click on the `Gradient texture` and hit `Ctrl+T` (will only work if Node wrangler is activated). This will add two options. Reconnect `Texture coordinate` from General to UV to `Mapping` socket vector.
10. `Shift+A`> search `Color Ramp` and add it between the `Gradient texture` and the `Principal BSDF`. 
11. In the `Color Ramp` menu, add another active positios by the + button and change colors such that there is dark (black) going to a light color and back to dark. 
12. Position the active positions close together for a tight light streak. 
13. Now it is possible to move the light streak with the `Mapping` menu option `X`. 
  14. The `Color Ramp` combo box option `Linear` can be change to `Ease` for smoother looking light path.

>[!NOTE]
> To animate, it is necessary to have clicked on the `Mapping node` in the Shading editor. Adjust the value of X to the desirable starting position and press `I` to add a keyframe. Move forward and add another keyframe. These keyframes will only be visible when the `Mapping node` is highlighted. 

## Random jitter

Based on a [Xan 3D video](https://www.youtube.com/watch?v=7YAdC7scKH8).

1. Open both `Timeline edior` and `Graph editor` at the bottom strip. 
2. Highlight an object to animate and add a keyframe right clicking and selecting `Insert key frame with keying set` and select `Location`. 
3. On the `Graph editor` find a right side tab. If it is not visible, press `N`.
4. While the appropriate axis of movement (e.g. X) is selected, select a menu `Modifiers` in the right tab and add a `Noise` modifier. This might need to be done for each axis separately.
5. If the random jitter should change during animation, select `Restrict frame range` and choose the appropriate length of a given modifier. 
6. Multiple modifiers of the same type can be added with different frame ranges.
