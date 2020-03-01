---
layout: post
title: New Features in Dust3D 1.0.0-rc.1
image: https://blogs.dust3d.org/public/attachments/2020-03-01-new-features-in-dust3d-1.0.0-rc.1/2020-03-01-new-features-in-dust3d-1.0.0-rc.1.png
---

[Dust3D](https://github.com/huxingyi/dust3d) is a 3D modeling software for indie developers to quick create video game characters. The are many new features been introduced in this release candidate version: [Dust3D 1.0.0-rc.1](https://github.com/huxingyi/dust3d/releases/tag/1.0.0-rc.1)

New Rig Generator
--------------------------
New rig system are more stable than the previous version, and is capable of handling uncombined meshes during the skinning and weighting processes. You can check the Cat example model from `File / Open Example` to see how to create a `run` motion which then could be exported as FBX and GLB for importing to [Unreal Engine](https://www.unrealengine.com/), [Unity](https://unity3d.com/), [Godot Engine](https://godotengine.org/) or other game engine.

![](https://blogs.dust3d.org/public/attachments/2020-03-01-new-features-in-dust3d-1.0.0-rc.1/dust3d-1.0.0-rc.1.pose-editor.png)

Remesh
--------------------------
The state of the art [Instant Meshes](https://github.com/wjakob/instant-meshes) is been introduced to remesh the model based on the poly count setting. It's native built-in, not invoked by command line. Choose the target poly count from component context menu you can get your model or component remeshed instantly.

![](https://blogs.dust3d.org/public/attachments/2020-03-01-new-features-in-dust3d-1.0.0-rc.1/dust3d-1.0.0-rc.1.remesh.png)

Cloth Simulation
--------------------------
An easy cloth simulating system based on Samer Itani's [FastMassSpring](https://github.com/sam007961/FastMassSpring) implementation.

![](https://blogs.dust3d.org/public/attachments/2020-03-01-new-features-in-dust3d-1.0.0-rc.1/dust3d-1.0.0-rc.1.cloth-simulation.png)

Spanish and Italian
----------------------
Thanks [MrAlexEsisteGia](https://github.com/MrAlexEsisteGia) for the Italian translation and [azagaya](https://github.com/azagaya) for the Spanish translation. Two new languages are been added.

UI Improvements
--------------------------
Thanks to Karl Robillard's contributions, the window size could be preserved between runs, and many useful shortcuts for menu items are been added.

_Join [mailing list](https://www.freelists.org/list/dust3d) and follow [twitter](https://twitter.com/jeremyhu2016) to get updates._
