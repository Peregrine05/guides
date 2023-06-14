# Rendering a Minecraft title screen panorama in Chunky

This guide assumes that you already know how to set up and render a scene in Chunky.

---

The panorama that Minecraft displays on the title screen is in cubemap format, in which six separate images form the six faces of a virtual cube that covers the sky. The panorama can be changed through the use of a resource pack.

## Step 1: Set the canvas size

The canvas size must have an aspect ratio of *1:1*. Open the `Scene` tab and set the `Canvas size` to a resolution that gives the canvas an aspect ratio of *1:1*, such as *512x512*, or *1024x1024*.

## Step 2: Set up the camera

Open the `Camera` tab. Click `Load preset`, and then click `Skybox Front (North)`.

## Step 3: Render

Press `Start` and render the scene to the target SPP. Rename the saved snapshot to "panorama_0.png" to prevent it from being overwritten.

Repeat Steps 2 and 3 for the other Skybox presets, renaming each new snapshot after each render finishes according to the mapping below.

`Skybox Front (North)` -> "panorama_0.png"

`Skybox Right` -> "panorama_1.png"

`Skybox Back` -> "panorama_2.png"

`Skybox Left` -> "panorama_3.png"

`Skybox Up` -> "panorama_4.png"

`Skybox Down` -> "panorama_5.png"

## Step 4: Create a resource pack

Create a new directory somewhere on your computer. Inside, create a file called "pack.mcmeta". Write the following text to the file, editing the description as you desire. See [this Minecraft Wiki page](https://minecraft.fandom.com/wiki/Pack_format) for a list of pack formats. Write the appropriate pack format for the version of Minecraft on which you wish to use the pack.

```json
{
    "pack": {
        "pack_format": 13,
        "description": "Write the resource pack description here."
    }
}
```

Next to "pack.mcmeta", create the directories, "assets/minecraft/textures/gui/title/background". Copy the six panorama files into the "background" directory.

Add the files within the resource pack root directory to a ZIP archive. The "pack.mcmeta" should be in the root of the ZIP archive.

## Step 5: Use the resource pack

Move the ZIP archive to the "resourcepacks" directory of your ".minecraft" directory. In Minecraft, select the resource pack to be loaded. If everything is successful, the title screen panorama should now be your Chunky render.

---

I highly recommend installing the [Panorama Tweaker](https://modrinth.com/mod/panorama-tweaker) mod for Fabric. By default, the panorama view is aimed slightly downward, preventing some of the panorama from being seen. This mod allows for extensive customization of the panorama view.
