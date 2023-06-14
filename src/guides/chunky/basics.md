# Chunky Basics

Chunky is a free and open-source application that can generate realistic-looking images of your Minecraft worlds with path tracing.

---

One thing to note is that if the selection of the world to be rendered is very large, and you do not have much RAM available, then you may want to consider using [Avoyd](https://www.avoyd.com/), which can load very large worlds much more quickly than Chunky can, and in much less memory than Chunky can, at the sacrifice of block models and textures, the loss of which would likely be unnoticeable at great distances.

Another thing to note is that many controls in Chunky are not limited by the range of the slider. Values beyond the range of the slider can often be entered into the associated input field. Also, many controls are equipped with a tooltip that becomes visible when the cursor is hovered over the control.

This guide covers only the basics; see the [Chunky Manual](https://chunky-dev.github.io/docs/) for a full reference.

---

## Install Chunky

Follow the instructions on the installation page of the Chunky Manual, which is found [here](https://chunky-dev.github.io/docs/getting_started/installing_chunky/).

## Configure the Launcher

If this is a fresh installation of Chunky, then no versions of Chunky will be installed. Click `Check for update` to download the newest stable release of Chunky if the Launcher does not prompt you to download it automatically. If the update check succeeds, then you should be presented with the newest available stable release, which is *2.4.4* at the time of this writing.

The `Memory limit (MiB)` control configures the amount of memory that is allocated to Chunky, measured in mebibytes (MiB), or *megabytes*, as is more commonly said. By default, it is set to *1024*, so you can increase this based on the amount of free memory available on your system. Depending on your operating system, leave 2 to 4 gibibytes (gigabytes) free for your operating system, and more if you intend to use other applications while Chunky is running. If you are running Chunky on a system with 16 GiB of RAM and Windows 10 or Windows 11, then allocating up to 12 GiB (12 288 MiB) is safe.

If you run Minecraft in a non-default Minecraft directory, then set the `Minecraft directory` to the Minecraft directory that you use. Custom Minecraft launchers that use a different directory structure require some more work to allow Chunky to load your Minecraft files properly. If you use one, then leave the `Minecraft directory` setting alone. This issue will be returned to later.

Finally, click `Launch` to launch Chunky.

## Load Resource Packs

To load a resource pack, click `Edit resource packs`, which is located in the `Options` tab on the right-side control panel. In the 'Resource Packs' dialog box that opens, click `Add`, and then browse for a ZIP file, a JAR file, or a "pack.mcmeta" to load as a resource pack. Chunky does not support resource packs that use custom block models.

This step is required if you use a custom Minecraft launcher. Browse for the Minecraft "version.jar" that contains the Minecraft textures that you wish to use before loading any other resource packs.

Note that textures in resource packs that are higher in the list will override textures in resource packs that are lower in the list, in the same manner as Minecraft.

## Load a World

In the `Map view` tab on the right-side control panel, click `Change World`. You should see a list of worlds that Chunky detected in your Minecraft "saves" directory. If the list is blank, and you use a custom Minecraft launcher, then click `Change world directory`. Browse for the "saves" directory that the custom launcher uses to store the worlds. Select the world that you want to render from the list and then click `Load selected world`.

## Select Chunks

The `Map` tab in the center panel displays an interactive map of the Minecraft world that is loaded. Chunk selections are made from this panel. Selected chunks are highlighted in red. Clicking a chunk selects or deselects it, depending on its current state of selection. Hold [Shift] and left-click and drag on the map view to create a rectangular selection of chunks. Hold [Ctrl] + [Shift] and left-click and drag to create a rectangular "de-selection" of chunks. To clear the chunk selection, right-click on the map and then click `Clear selection`.

It should be noted that Chunky's default `PACKED` octree implementation has a chunk limit of about 400 000 chunks on most worlds. If you must load more chunks while keeping memory usage low, then you should install the [Octree plugin](https://chunky-dev.github.io/docs/plugins/plugin_list/#octree-plugin) according to the [plugin installation instructions](https://chunky-dev.github.io/docs/plugins/chunky_plugins/) and use one of the implementations that it provides; `DICTIONARY` and `DAG_TREE` specifically are good for reducing memory usage.

## Load Selected Chunks

Open the `Scene` tab on the left-side control panel. You may make changes to what entities are loaded into the scene with the `Load entities` control. If the world height and depth limits of your world are greater than the default height and depth limits, or you wish to render a smaller vertical slice of your world, then change the `Y min clip` and `Y max clip` to define the lower and upper limits, respectively, of the selection that you wish to render. Once that is done, click `Load selected chunks`.

## Scene Setup

Once the chunk loading process is complete, Chunky will automatically switch to the `Render preview` tab, where a preview of the selected chunks will be generated.

It should be noted that because Chunky is CPU-driven, generating a preview for larger canvas resolutions may require much time, and may make setting up the scene more difficult. In most cases, a small canvas size should be used during scene setup, and a larger one only used for the final render. In the `Scene` tab, set the `Canvas size` to a lower resolution, such as *400x400*, if it is not already set, and then press [Enter]. It is possible and recommended to test-render your scene while setting it up, to get an idea of the final result. This can be done by pressing `Start` and allowing it to render for a short time. These test renders will also benefit from a smaller canvas, as less time is required to path-trace a sample of a smaller canvas.

### Camera Setup

The camera movement controls are similar to the player movement controls in Minecraft. Use the [W], [A], [S], and [D] keys to move the camera one meter (one block) forward, left, back, and right, respectively. Use the [R] and [F] keys to move the camera one meter up and down, respectively. Use one of the movement keys while holding [Shift], [Ctrl], or [Ctrl] + [Shift] to multiply the camera movement by *0.1*, *100*, or *10*, respectively. Left-click and drag the preview to rotate the camera in the direction the cursor is dragged. Scroll the mouse wheel to zoom the camera.

The `Camera` tab in the left-side control panel contains controls for manipulating the camera. Of particular interest here may be the `Projection mode` control. `Parallel` projection is ideal for taking overhead shots of the scene. See [this page](https://chunky-dev.github.io/docs/reference/user_interface/chunky/render_controls/camera/#figure-3) of the manual for example renders of different camera projections. The `Depth of field` and `Subject distance` controls change the focus of the camera. To autofocus on a point in the scene, right-click on that point in the render preview and then click `Set target`. Then click `Autofocus` in the `Camera` tab.

### Lighting Setup

The `Lighting` tab in the left-side control panel contains controls for manipulating the lighting in the scene. Adjust the controls to your liking. The control names should be self-explanatory. There are several things to note, though: (a) the `Sky light` control only changes the amount of light that the scene receives from the sky; it does not change the apparent brightness of the sky; (b) emitters are blocks that are set to emit light; these can be enabled with the `Enable emitters` control (Note that emitters can greatly increase the amount of time required to eliminate noise in the render); (c) the `Emitter Sampling Strategy` control changes how emitters (blocks that are set to emit light) are sampled in an attempt to reduce noise, if emitters are enabled. See [this page](https://chunky-dev.github.io/docs/user_guides/introduction/next_event_estimation/#emitter-sampling-strategy-ess) of the manual for details about ESS and example renders; (d) the `Enable sunlight` control causes a noteworthy performance drop when enabled, so it should be disabled in scenes that do not receive sunlight; (e) the `Draw sun` control changes whether the sun texture is drawn in the sky; it has no effect on the sunlight itself; (f) when `Sun azimuth` is *0*, the sun is due East; and (g) the `Sun color` control only changes the color of the sunlight; the color of the sun texture itself is determined by the resource pack that is in use.

### Sky and Fog Setup

The `Sky & Fog` tab in the left-side control panel contains controls for manipulating the sky and fog in the scene. Use the `Sky mode` control to select the type of sky to use in your scene. `Skymap (panoramic)`, `Skymap (spherical)`, and `Skybox` allow you to use different types of skymaps as the sky in the scene. See [this page](https://chunky-dev.github.io/docs/user_guides/skymaps/) of the manual for information about the different types of skymap formats. Enabling `Transparent sky` will render the sky as transparent and allow you to layer a separate image behind the render to be used as the sky. The `Enable clouds` control will add Minecraft-style clouds to the scene. The shape of the clouds is determined by the loaded resource pack. The size and position of the clouds can be changed with the other cloud controls. The `Sky fog blending` control changes how much the fog color is blended with the sky. The blending is performed only when fog is enabled.

### Water Setup

The `Water` tab in the left-side control panel contains controls for manipulating the water in the scene. By default, the water in Chunky has a normal map applied; this can be disabled by enabling `Still water`. The `Water visibility` control changes the distance at which light traveling through water is absorbed. The `Water opacity` control changes the opacity of the surface of the water. By default, the color of water is taken from the biome that the water is in, but it can be changed to a custom water color with the `Use custom water color` control. The `Water world mode` control adds an infinite ocean around the scene. The ocean can be allowed to exist within the scene by disabling `Hide the water plane in loaded chunks`.

### Entities Setup

The `Entities` tab contains controls for manipulating entities in the scene. Here you can see a list of entities that Chunky loaded when `Load selected chunks` was used. Select an entity in the list to expose controls to manipulate its position and orientation. Use the `+` control to add players to the scene at the location of the current preview target, if any, or at the location of the camera. Use the `-` control to remove the selected entity from the scene.

### Materials Setup

The `Materials` tab contains controls for manipulating material properties of different blocks in the scene. Select any material in the list to change its properties. See [this page]() of the manual for information about the different material properties and their effects. In summary, `Emittance` changes the intensity of the light emitted by the material; `Specular` changes how mirror-like the material behaves, `IoR` determines how light refracts when it intersects the material. `Metalness` behaves identically to `Specular`, but reflected light is tinted according to the texture of the material. `Smoothness` is self-explanatory. Its effects are visible only in specular reflections.

### Postprocessing Setup

The `Postprocessing` tab contains controls for adjusting the final appearance of the image. The `Exposure` control changes the overall brightness of the image, and the `Postprocessing filter` control changes the tone mapping filter applied to the image.

### Advanced Setup

In most cases, you should not need to adjust the controls in the `Advanced` tab in the left-side control panel. If you intend to use your computer while Chunky is rendering, you should reduce the values of `Render threads` and `CPU utilization`, which control how much CPU power used is for rendering. Another control worth mentioning is `Ray depth`, which controls the maximum number of times a ray can bounce through the scene before being terminated. A value of 3 to 8 is typically enough for most scenes. Increasing the ray depth improves lighting accuracy, especially if the scene contains many refractive or reflective materials, at the cost of performance.

## Render

Once the scene has been set up to your liking, return to the `Scene` tab and set the `Canvas size` to a higher resolution, such as *1920x1080*. At the top-left of the window, set the name of the scene in the `Scene` input field, and then click the `Save` button, which uses a disk graphic. Finally, in the bottom-left of the window, set the `Target SPP` to a reasonable value for the scene. The `Target SPP` has a direct effect on render time. The greater the value of the `Target SPP`, the more time the render will require to be complete, but the less noise will be in the scene. For purely daylight renders, a `Target SPP` value between 32 and 1 024 is often enough. For daylight renders with emitters, a value between 4 096 and 16 384 is better. For scenes lit only by emitters, 16 384 SPP or greater is often required to reduce noise to an acceptable level.

To render the scene, click the `Start` button in the bottom-left of the window. Chunky will autosave the scene on the interval defined by the `Save snapshot once every X frames` control in the `Scene` tab, and will save a snapshot if `Save snapshot for each dump` is enabled. If at any point you must stop the render to continue later, then first click `Pause`, wait for the current sample to finish rendering, and then click the `Save` button. Once saving has completed, it is safe to close Chunky without losing any render progress. The scene along with its render progress can then be loaded at any time and the render continued. Once Chunky renders the scene to the `Target SPP`, it will save the scene and save a snapshot to the "snapshots" directory of the directory of your scene, which can be accessed by clicking `Open scene directory` in the `Scene` tab. If you must render further, click `Pause`, increase the `Target SPP`, and then click `Start`.

## Advanced

This section covers more advanced usage of Chunky.

### Downloading Snapshots

Snapshot builds of Chunky are built from the master branch. They contain the latest additions and bug fixes, but potentially the most new bugs. To download and use a snapshot build, open the Launcher, and set the `Release channel` in the `Advanced Settings` panel to `Snapshot`. Then click `Check for update`. Install the snapshot build and then click `Launch`.

In addition to snapshot builds, there are stable snapshot builds of Chunky, which are built from the 2.4.x branch. They contain only bug fixes and minor additions and are considered stable enough for general use. To download and use a stable snapshot build, set the `Release channel` to `Stable snapshot` and then click `Check for update`. Install the stable snapshot build and then click `Launch`.

### Downloading Pull Request Builds

Pull Request builds are built from development branches of Chunky. These branches may contain new features or bug fixes, as well as buggy or unfinished work. To download and use a pull request build, first set the `Update Site` to `https://chunky-pr.lemaik.de`. Then click `Reload`, which is next to the `Release channel` control. Set the `Release channel` to the pull request of which you want to download a build, and then click `Check for update`. The update check may fail for one of a few reasons, but if it succeeds, install the build and then click `Launch`.
