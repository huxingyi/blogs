---
layout: post
title: Auto Remesher 1.0 Beta Released
image: https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1.png
---

Since the [Initial commit](https://github.com/huxingyi/autoremesher/commit/1ae07f946ede291ca0e3915f4650aa8323091ae5) of [Auto Remesher](https://github.com/huxingyi/autoremesher) from 18 Jun 2020, near three months have been passed, and I am confident to move this repository out of alpha stage, and release the first beta, you can download it from [here](https://github.com/huxingyi/autoremesher/releases).

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1.png)

Auto Remesher is mainly been developed for [Dust3D](https://github.com/huxingyi/dust3d), and is aim to be an automatic quad retopology tool and library which could be very easy to remesh a triangulated model to a quad mesh. You can check this post for [how this repository been originated](https://blogs.dust3d.org/2020/06/19/auto-remesher/).

How it works?
--------------------------
Auto Remesher expect a triangulated mesh as input, with or without boundaries. First we uniformly remesh it by [OpenVDB](https://www.openvdb.org/), and [CGAL](https://www.cgal.org/).

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-preprocessing.png)
_This 3D model by Artec Group inc. (www.artec3d.com) is licensed under the Creative Commons Attribution 3.0 Unported License._

The uniform remeshed result is then been parameterized by [QuadCover](http://alice.loria.fr/index.php/software/4-library/75-geogram.html) method. It project all the triangles to a grid system. After that, all the connections could be extracted by tracing the intersections of isoline and the edges of triangles. The following images show each of the steps.

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-parameterization.png)
_Parameterization UV using QuadCover_

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-quadcover.png)
_Show model with parameterization texture, in MeshLab_

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-connections.png)
_Connections extracted from parameterization_

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-edges.png)
_Edges extracted from connections_

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/auto-remesher-beta1-quads.png)
_Quads extracted from edges_

In the first several alpha releases, we tried [MIQ](https://github.com/libigl/libigl/blob/48ac6aa0b5ef9286c95874042cfe68965bc94f29/include/igl/copyleft/comiso/miq.h) method. It works on the same way of parameterization as QuadCover, and could generate more even quads, but trade with more computation time, especially on complex meshes.

Relative Height
-------------------------

During the development of Auto Remesher, we create a new method called [Relative Height](https://twitter.com/jeremyhu2016/status/1296672423052361729), although it's not been used any more in this repository, it may be useful for other things.

![](https://blogs.dust3d.org/public/attachments/2020-09-11-auto-remesher-1.0.0-beta.1-released/relative-height.jpg)

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Agree, I changed the original model color as the same as the marked one. Very cheap lighting trick.<a href="https://twitter.com/hashtag/RelativeHeight?src=hash&amp;ref_src=twsrc%5Etfw">#RelativeHeight</a> <a href="https://t.co/9NF06veHXr">https://t.co/9NF06veHXr</a> <a href="https://t.co/9BZHYI6dc8">pic.twitter.com/9BZHYI6dc8</a></p>&mdash; Jeremy HU (@jeremyhu2016) <a href="https://twitter.com/jeremyhu2016/status/1297136925350875137?ref_src=twsrc%5Etfw">August 22, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

[Jake Rice](https://twitter.com/TearsOfJake) did some interesting test as linked below.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I tried modifying the Sidefx Labs Mesh Sharpen tool to use the relative height instead of curvature. The left has been sharpened with mean curvature, and the right, sharpened with relative height. Relative height seems to do a way better job of preserving edge flow!!! <a href="https://t.co/EcyKxsCzmH">pic.twitter.com/EcyKxsCzmH</a></p>&mdash; Jake Rice (@TearsOfJake) <a href="https://twitter.com/TearsOfJake/status/1296940568258334720?ref_src=twsrc%5Etfw">August 21, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Thanks everyone who helped to test and provide invaluable suggestions.

_Join [mailing list](https://www.freelists.org/list/dust3d) and follow [twitter](https://twitter.com/jeremyhu2016) to get updates._
