---
layout: post
title: Non-destructive Painting in Dust3D
image: https://blogs.dust3d.org/public/attachments/2020-04-19-non-destructive-painting-in-dust3d/non-destructive-painting-480.png
---

Implementing the next coming feature, Non-destructive Painting, is one of the most exciting moments of coding [Dust3D](https://github.com/huxingyi/dust3d). Dust3D is a 3D modeling software, featuring a semi-auto generation workflow of 3D assets making.

![](https://blogs.dust3d.org/public/attachments/2020-04-19-non-destructive-painting-in-dust3d/non-destructive-painting-480.png)   

What's Non-destructive Painting? The painting result, including the colors and the positions of the colors, are mesh independent, and are been stored in a voxel grid.

When new paint action committed, the mouse position will be converted to a voxel cell, color info will be updated to that cell, and based on the current brush size, neighboring voxel cells will be updated with a gradient color as well. The final mesh color calculation is similar with the painting process, the only difference is that, paining is updating to voxel cell, mesh coloring is fetching from voxel cell.

Imaging your house been split to 100x100x100 cells, every brush you draw in the space, will lit one or more cells. You are not painting in a 2D space, but in real 3D. There is a voxel editor called MagicaVoxel, is modeling in this way.

In Dust3D software, you are not allowed to edit vertex position directly, because all the vertices, quads, triangles are generated automatically, based on the nodes on the canvas you drawn. Any node or edge between nodes been changed, the mesh will be regenerated. The traditional vertex painting will not work on this workflow, unless you lock the generated mesh. Once you lock the mesh generation, you lose the chance to modify the mesh topology by nodes.

By introducing this 3D space painting, you are free to change the nodes even after the painting is finished.

Here is the demonstration of painting a banana mesh in Dust3D, and the next video shows how Non-destructive works.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Demo non-destructive workflow, painting keeps after mesh changed. <a href="https://twitter.com/hashtag/Dust3D?src=hash&amp;ref_src=twsrc%5Etfw">#Dust3D</a> <a href="https://t.co/zdEmrefv8K">pic.twitter.com/zdEmrefv8K</a></p>&mdash; Jeremy HU (@jeremyhu2016) <a href="https://twitter.com/jeremyhu2016/status/1251766197546135552?ref_src=twsrc%5Etfw">April 19, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This feature will be available in Dust3D 1.0 RC 7 soon.

_Join [mailing list](https://www.freelists.org/list/dust3d) and follow [twitter](https://twitter.com/jeremyhu2016) to get updates._
