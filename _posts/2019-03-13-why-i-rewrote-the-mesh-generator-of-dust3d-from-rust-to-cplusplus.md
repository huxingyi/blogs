---
layout: post
title: Why I rewrote the mesh generator of Dust3D from Rust to C++
---

Dust3D is a quick 3D modeling software. It automatically generates a
mesh from nodes drawn by the user. Most of the code is implemented in
C++ with Qt, including the UV unwrapper, rigger, pose and motion
editor etc, however, the core mesh algorithm was written in Rust.
Recently I have rewritten the Rust part. [The
codebase](https://github.com/huxingyi/dust3d) is pure C++ now.

<img src="https://pbs.twimg.com/media/D1MxDcTVsAAzKDK.jpg" width="300"
height="179">

<sup> (Screenshot of Dust3D, the three thumbnails in the lower right
corner are the preview of exported result in Godot, Unity, and
Blender) </sup>

I have been asked if I am going to migrate more of the C++ code in
Dust3D to Rust, and there is another author who has contributed many
excellent improvements on the Rust code, thanks
[anderejd](https://github.com/anderejd). I think I’d better explain a
little bit why I dropped the [Rust
implementation](https://github.com/huxingyi/meshlite) from Dust3D.

The mesh generator was originally implemented in pure C, then migrated
to Rust. Why did I switch to Rust? C is quite lacking in
infrastructure, but I was sick of different C++ trivial variations
across different platforms, it’s a pain to introduce a third party
library if you want your whole code to work on different systems with
different versions and brands of compiler. Rust has all the merits I
wanted, it’s easy to start, painless to include other libraries, and
most importantly, it’s memory safe. If you have ever been heart
attacked by core dumps, you will know how beautiful this is.

Given so many advantages, why I am switching back to C++? The most
beautiful thing about Rust is also a disadvantage. When you implement
an algorithm using C++, you can write it down without one second of
pause, but you can’t do that in Rust. As the compiler will stop you
from borrow checking or something unsafe again and again, you are
being distracted constantly by focusing on the language itself instead
of the problem you are solving. I know the friction is greater because
I am still a Rust learner, not a veteran, but I think this experience
stops a lot of new comers, speaking as someone who already conquered
the uncomfortable syntax of Rust, coming from a C/C++ background.

Another reason is the Rust ecosystem is still immature. As an indie
game developer I can see the situation is changing, there is a website
[Are we game yet?](http://arewegameyet.com/) that lists many neat
things in the Rust world, there is a data driven game engine written
in Rust called [Amethyst](https://www.amethyst.rs/), all these things
look really promising. But, there is no Qt, no CGAL etc, all these
frameworks and libraries have been developed for so many years and
maintained very high level of quality. I know there are some bindings,
but it’s not mature and not enough.
