---
layout: post
title: Dust3D on Raspberry Pi 3 Model B+
---

My friend Kevin Liang, who helped me 3D printed many cool Dust3D models, bought a [Raspberry Pi 3 Model B+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/), the first thing to do when he received this tiny size computer is to run [Dust3D](https://github.com/huxingyi/dust3d), the same tiny size 3D modeling software.  

![](https://blogs.dust3d.org/public/attachments/2019-07-09-dust3d-on-raspberry-pi-3-model-b-plus/dust3d-on-raspberry-pi-480.png)   

Unfortunately, the Travis CI generated AppImage file can not run on Pi's ARM CPU. But we can always build from source.

Most of the needed dev tools are out of the box on the default system, such as gcc, make. The Dust3D build instructions which written for Ubuntu, works like a charm on Pi. However, it always failed on the same file `nodemesh/combiner.cpp`, this file used CGAL library heavily. Every time, the machine dies on compiling this file, all system lose response. After power off, try, die, power off again, try, die again, several times, we found, out of memory is the root cause.

Googling keywords, "gcc low memory", the first answer by Colin lan King shows how to create large swap memory for linux. So we created 4G swap for Pi to replace the default 100M swap.

Finally, more than one hours building, we succeed running Dust3D on Raspberry Pi.

The following are the full commands to build Dust3D on a Raspberry Pi 3 Model B+ with default system.
```
; Prepare 4G virtual memory for building, the default 1G memory and 100M swap are not enough to build.
; (The following swap image creating script comes from Colin lan King)

$ dd if=/dev/zero of=swap.img bs=1M count=4096
$ mkswap swap.img
$ chmod 0600 swap.img
$ sudo chown root:root swap.img
$ swapon swap.img



; Install dependencies

$ sudo apt-get install qtbase5-dev
$ sudo apt-get install qttools5-dev-tools
$ sudo apt-get install libcgal-dev
$ sudo apt install cmake
$ wget https://github.com/CGAL/cgal/releases/download/releases/CGAL-4.13/CGAL-4.13.zip
$ unzip CGAL-4.13.zip
$ cd CGAL-4.13
$ mkdir build
$ cd build
$ cmake ../
$ make
$ sudo make install



; Build Dust3D

$ git clone https://github.com/huxingyi/dust3d.git
$ cd dust3d
$ qmake -qt=5 -makefile
$ make



; Run Dust3D

$ ./dust3d
```
