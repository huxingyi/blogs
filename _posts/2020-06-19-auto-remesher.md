---
layout: post
title: Auto Remesher
image: https://blogs.dust3d.org/public/attachments/2020-06-19-auto-remesher/auto-remesher-matrix.png
---

[Auto Remesher](https://github.com/huxingyi/autoremesher) is an automatic quad remeshing tool, and it will be integrated to [Dust3D](https://github.com/huxingyi/dust3d) once it has acceptable performance.

![](https://blogs.dust3d.org/public/attachments/2020-06-19-auto-remesher/auto-remesher-matrix.png)   

Why we need yet another remesh tool?
--------------------------

I posted a [Tweet](https://twitter.com/jeremyhu2016/status/1272850648204103681) about the status of the current open source quad remeshing libraries. From the replies I got, I guess I am not the only one who is not satisfied with the current status of auto retopology.

In this post, I am not going to talk about closed source options except [Quad Remesher](https://exoside.com/quadremesher/). It's the state of the art tool, with plugins work with almost all the mainstream 3D modeling software. I never try it by myself, only know it from the demos and the videos other people posted. The quality looks like is the best among all the options at the moment, I heard that Pixelogic bought it and integrated it to ZBrush as Zremesher many years ago.

Instant Meshes
--------------------------

The best open source alternative is [Instant meshes](https://github.com/wjakob/instant-meshes). It's superfast, with high quality quads generation. It's already been integrated to Dust3D. The main complaint is there are annoying holes left after remeshing.

Quadriflow
--------------------------

[Quadriflow](https://github.com/hjwdzh/QuadriFlow) is another nice option, the quality of the generated quads is slightly better than Instant meshes sometimes, but not always. Artifacts could still be generated as well. Since it's globalized optimization comparing to localized methods, it's much slower than Instant meshes.

OpenVDB volume to mesh
--------------------------

OpenVDB is a academy award winning library. [OpenVDB volume to mesh](https://www.openvdb.org/documentation/doxygen/VolumeToMesh_8h.html) is great for high dense quads generation. This method is fast and robust. But the quads generated have a blocky feeling when the poly count is low. BTW, OpenVDB has been introduced to the next release of Dust3D as the core supporting library for sculpting feature.

Constrained Mixed-Integer Solver
--------------------------

There is a golden piece which you normally don't hear people talk about it on the forums. But it appears on almost every paper related with quadrangulation. That's the [Constrained Mixed-Integer Solver](https://www.graphics.rwth-aachen.de/software/comiso/), you need an extra quad extraction tool to work together for remeshing though. The quads generated from this combination are beautiful, the main pitfall is it's too slow. I hope it can be optimized by introduce tbb or other parallel optimization.

Auto Remesher
--------------------------

Auto Remesher repository is the new bottle for old wine, [libigl](https://github.com/libigl/libigl/blob/48ac6aa0b5ef9286c95874042cfe68965bc94f29/include/igl/copyleft/comiso/miq.h) wrapper of Constrained Mixed-Integer Solver and the [libQEx](https://github.com/hcebke/libQEx) quad extraction. These two pieces were there for years, but there isn't an integrated tool which can be downloaded directly and work out of the box for remeshing, or there is but I cannot find it.

Benefits to Dust3D
--------------------------

[Dust3D](https://github.com/huxingyi/dust3d) start as a low poly quick modeling tool. Without adding new features, remesh function is not urgently needed, because the mesh is procedurally generated, we can avoid to generate bad quads. After voxel based sculpting feature been introduced, we need a good high poly to low poly quads converter without manual twist steps. I hope [this repository](https://github.com/huxingyi/autoremesher) could be a starting point and playground for meshing beautiful quads.

_Join [mailing list](https://www.freelists.org/list/dust3d) and follow [twitter](https://twitter.com/jeremyhu2016) to get updates._
