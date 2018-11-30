---
layout: post
title: The Game Asset Pipeline
---

*Make Game Ready Assets in a Blink using Dust3D*  

Table of Contents
---------------
1. [How to Make a 3D Model](#HowToMakeA3DModel)
2. [Import to Unity](#ImportToUnity)
3. [Import to Godot](#ImportToGodot)
4. [Further Edit in Other Tools](#FurtherEditInOtherTools)
5. [What's Next?](#WhatsNext)
6. [Want More?](#WantMore)

How to Make a 3D Model <a name="HowToMakeA3DModel"></a>
---------------
**Preparing Reference Sheet**  
<img align="right" src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/guitar-reference-sheet.png" width="256" height="128">
Prepare two pictures, one shows the `front view` and the other shows the `side view`, you can take photo of a real object, google it from internet or even draw it if you are an artist. No matter from what method you got the two pictures, make sure they are vertical equally aligned, and been combined before used in the Dust3D as a reference sheet.
In this article, I will use my own guitar as an example, I took two pictures using my mobile phone, and combine them in GIMP (A photoshop like software but free).

**Making Model**  
Open the reference sheet from last step in the Dust3D menu: `File / Change Reference Sheet...`
Now place nodes on the canvas, adjust the radius of the nodes according to the reference sheet. There is nothing complicated need to explain, when you play it, you can easily handle the process of modeling in Dust3D, and you can still refer to this video for detailed demonstration: [Make a 3D model from scratch using Dust3D](https://youtu.be/wQerDObDjOs).

**Choosing Materials**  
<img align="right" src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/pbr-material-editor-dust3d.png" width="293" height="263">
Pick colors for parts from the `eyedropper icon` of parts tree, you can also choose different materials for parts from there. Currently, `PBR` (Physically based rendering) is one of the most popular shading models of the game industry, Dust3D supports the `metal/roughness PBR` materials, you can google "PBR Roughness/Metallic" for better understanding of it.
Create material from the Materials tab. There are five texture types you can customize, if you don't understand what each type means, no worries, there are many free seamless PBR textures you can find in the internet (Keywords: "Free seamless PBR textures"), download the specified texture types from where it provided. In this article, We are going to use the [Scratched Gold 01](https://www.cgbookcase.com/textures/scratched-gold-01) and [Wooden Planks 04](https://www.cgbookcase.com/textures/wooden-planks-04) from cgbookcase.com, both are 1K Resolution.
<img align="right" src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/color-and-material-picker-dust3d.png" width="154" height="131">
Create two materials from the resources, and assign them to the neck and body of the guitar separately from the parts tree.

**Exporting**
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/main-ui-dust3d.png" width="696" height="414">
<img align="right" src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/export-preview-dust3d.png" width="481" height="234">
Phew, no manual UV unwrapping, it's done! We got a game ready asset.
Now, export it as FBX for Unity or glTF for Godot from the main menu: `File / Export...`.

Import to Unity <a name="ImportToUnity"></a>
---------------
Import the outcome "guitar.fbx" from Unity menu: Project / Assets / (Right Click) Import New Asset..., you can see the imported asset guitar, choose the Materials tab from the Inspector window,
Click the button on the right of label "Textures": Extract Textures... (If you ignore this step, there will be no materials applied on the model, just blank color), the popup "Select Textures Folder" dialog will ask you where to put the extracted textures, you can leave it as default path(Project Root / Assets) or create sub directory such as Materials.
With the current unity version (2018.2.17f1 Personal 64bit), there is a "NormalMap settings" dialog will popup during the importing, just click the "Fix now" and your asset is ready.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/import-to-unity-from-dust3d.png" width="696" height="414">
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/material-preview-in-unity-from-dust3d.png" width="696" height="414">

Import to Godot <a name="ImportToGodot"></a>
----------------
Drag the exported outcome with name "guitar.glb" to the left bottom area of the main window, right click the imported item "guitar.glb", choose "Open Scene(s)", there will be a popup dialog ask you to confirm, just click the "Open Anyway", now you can see the model showing in the scene view. Click the Mesh from "Scene / Scene Root" tree, then click the little guitar icon in the right bottom to preview the rendered model.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/preview-in-godot-from-dust3d.png" width="696" height="414">
You can also view the glTF file from online: https://gltf-viewer.donmccurdy.com/
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/preview-in-gltf-view-from-dust3d.png" width="696" height="414">

Further Edit in Other Tools <a name="FurtherEditInOtherTools"></a>
-------------------------
Dust3D is designed for easily making game ready assets, if you just want to make a base model in Dust3D and then further sculpt in another software such as Blender, that is totally fine, just export as OBJ format, this will make the exported result more quadified instead of triangulated.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/preview-in-blender-from-dust3d.png" width="696" height="414">

What's Next? <a name="WhatsNext"></a>
---------------
We have demonstrated how to make a game asset easily in Dust3D, but it's still, no animation.
Dust3D support pose and motion editing, let's see what we can get in the following steps, A fully animated running cycle of camel:
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/camel-run-motion-editor-dust3d.gif" width="200" height="105">
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/camel-run-in-unity-from-dust3d.gif" width="128" height="165">

**Rig**  
To make the model animated, in other animation authoring tools, such as Maya and Blender, usually you need to create bones for the model and paint weights for each bone to influent the vertices. There is no difference of the underlying animation theory between Dust3D and other tools, however, Dust3D takes the heavy burden of bones creating and weights painting for you as long as you tell the software the key positions of a body.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/rig-mark-dust3d.png" width="696" height="414">
Mark each limb and neck, and necessary joints, then choose the Rig Type as Animal, the auto-rigged result will show on the Rig window.

**Pose**  
The animation feature of Dust3D is an experiment to replicate the work of the motion-picture pioneer [Eadweard Muybridge](https://en.wikipedia.org/wiki/Eadweard_Muybridge). Let's first see how Eadweard did his wonderful work in 1878, image courtesy of Library of Congress Prints and Photographs Division and Nevit Dilmen:
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/The_Horse_in_Motion_high_res.jpg" width="220" height="135">
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/The_Horse_in_Motion-anim.gif" width="170" height="115">
From the above motion clip, we can see the key of motion is the keyframe, in Dust3D, one pose consists of one single or a serials of keyframes.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/pose-editor-dust3d.png" width="482" height="333">
Drag the nodes to adjust pose, just like modeling, the only difference is that you can not scale the radius of the node and there is no means of doing that.

**Motion**  
You can compose of poses and even sub motions as one motion.
<img src="/public/attachments/2018-11-29-the-game-asset-pipeline/images/items-list-of-motion-editor-dust3d.png" width="456" height="267">
Right click the interpolating buttons to adjust the bouncing setting, which was mentioned in David Rosen's GDC talk [An Indie Approach to Procedural Animation](http://www.gdcvault.com/play/1020583/Animation-Bootcamp-An-Indie-Approach) as `Spring Interpolation`.

Want More? <a name="WantMore"></a>
---------------
(TO BE CONTINUED)
