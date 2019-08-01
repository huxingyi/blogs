---
layout: post
title: Procedural 3D Model Generation in Dust3D
---

In this article, I will try to introduce you the **Procedural Generation** feature in [Dust3D](https://github.com/huxingyi/dust3d) using JavaScript.

![](https://blogs.dust3d.org/public/attachments/2019-08-01-procedural-3d-model-generation-in-dust3d/dust3d-procedural-tree.png)

About Dust3D
---------------

[Dust3D](https://github.com/huxingyi/dust3d) is a free and open-source software for quick making 3D model with texture and rig automatically generated. It supports Linux, MacOS, and Windows.

In case you never use this software before, Here is a short demo on how to make a model in this software in none procedural mode.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Day 111 Chair <a href="https://twitter.com/hashtag/10minuteseveryday?src=hash&amp;ref_src=twsrc%5Etfw">#10minuteseveryday</a> <a href="https://twitter.com/hashtag/Dust3D?src=hash&amp;ref_src=twsrc%5Etfw">#Dust3D</a><br><br>Model: <a href="https://t.co/6FnPgjFD0o">https://t.co/6FnPgjFD0o</a><a href="https://twitter.com/hashtag/gamedev?src=hash&amp;ref_src=twsrc%5Etfw">#gamedev</a> <a href="https://twitter.com/hashtag/indiedev?src=hash&amp;ref_src=twsrc%5Etfw">#indiedev</a> <a href="https://twitter.com/hashtag/lowpoly?src=hash&amp;ref_src=twsrc%5Etfw">#lowpoly</a> <a href="https://twitter.com/hashtag/3dmodeling?src=hash&amp;ref_src=twsrc%5Etfw">#3dmodeling</a> <a href="https://t.co/GRzIv73olZ">pic.twitter.com/GRzIv73olZ</a></p>&mdash; Jeremy HU (@jeremyhu2016) <a href="https://twitter.com/jeremyhu2016/status/1156667091451125760?ref_src=twsrc%5Etfw">July 31, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The progress of modeling is to put nodes on canvas. By modifying the radius and position of the nodes, and other settings, you control the shape of the generated model.

Procedural Generation using JavaScript
---------------

In [recent beta release](https://github.com/huxingyi/dust3d/releases/tag/1.0.0-beta.22), there is a new feature which allows you to generate nodes from JavaScript. It’s similar as web browser parse JavaScript to create HTML document. For example, the following JavaScript code will generate a paragraph in web browser,

    var paragraph = document.createElement("p");
    var node = document.createTextNode("This is text node under paragraph element.");
    paragraph.appendChild(node);
    document.body.appendChild(paragraph);

In Dust3D, you can create a node in a similar way,

    var component = document.createComponent();
    var part = document.createPart(component);
    var node = document.createNode(part);
    document.setAttribute(node, "x", 0.5);
    document.setAttribute(node, "y", 0.5);
    document.setAttribute(node, "z", 1.0);
    document.setAttribute(node, "radius", 0.2);

<sup>*Copy and paste the code to the script editor of Dust3D to run it*</sup>

This will generate a node on canvas, and then the node been further generated into a cube mesh.

![](https://blogs.dust3d.org/public/attachments/2019-08-01-procedural-3d-model-generation-in-dust3d/dust3d-procedural-cube.png)

There are two circles on the canvas, orange circle represent the front view, green circle represent the side view. And the small triangle is the model center anchor.

Dust3D Document Structure
--------------------------
From the code, you may noticed that there are component, part, node, and attributes. Let's explain a little bit here, for details you may need to check the [Dust3D Script Reference](http://docs.dust3d.org/en/latest/script_reference.html).

![](https://blogs.dust3d.org/public/attachments/2019-08-01-procedural-3d-model-generation-in-dust3d/dust3d-document-structure-ui.png)

<sup>*1. Document  2. Canvas  3. Nodes and Edges  4. Part 5. Component*</sup>

A document shows as a window in Dust3D, you draw nodes and connect nodes with edges on the canvas, all the connected nodes and edges grouped as parts. One document can have multiple parts. Each part belongs to a component.

Now let's make a more complex example to understand these concepts.

More Complex JavaScript Example
---------------

    function createNode(part, origin, radius)
    {
        var node = document.createNode(part);
        document.setAttribute(node, "x", origin.getComponent(0));
        document.setAttribute(node, "y", origin.getComponent(1));
        document.setAttribute(node, "z", origin.getComponent(2));
        document.setAttribute(node, "radius", radius);
        return node;
    }

    function createLine(fromPosition, fromRadius, toPosition, toRadius, segments)
    {
        var component = document.createComponent();
        var part = document.createPart(component);
        var previousNode = undefined;
        for (var i = 0; i <= segments; ++i) {
            var alpha = (i + 0.0) / segments;
            var origin = fromPosition.clone().lerp(toPosition, alpha);
            var radius = fromRadius * (1.0 - alpha) + toRadius * alpha;
            var node = createNode(part, origin, radius);
            if (undefined != previousNode)
                document.connect(previousNode, node);
            previousNode = node;
        }
        return part;
    }

    var fromPosition = new THREE.Vector3(0.5, 0.8, 1.0);
    var fromRadius = 0.3;

    var toPosition = new THREE.Vector3(0.5, 0.2, 1.0);
    var toRadius = 0.1;

    var segments = document.createIntInput("Segments", 3, 2, 10);
    console.log("Hey, we accept parameter from the UI input control! The segments is " + segments);

    var linePart = createLine(fromPosition, fromRadius, toPosition, toRadius, segments);
    document.setAttribute(linePart, "subdived", "true");

The above JavaScript code generates a cylinder, from the down right corner, you can see a Segments slider control, adjust the slider, the generated result will change according to the segments value you modified. You may need toggle the settings in view menu to see the wireframe, the actual generated segments may greater than the value you configured because of intermediate nodes generation.

![](https://blogs.dust3d.org/public/attachments/2019-08-01-procedural-3d-model-generation-in-dust3d/dust3d-procedural-cylinder.png)

Also, there is a text box above the slider, shows

    Hey, we accept parameter from the UI input control! The segments is 3

This is the console output. Yes, you can use `console.log` just as you use it in web browser.

Where to Go From Here?
-------------------------

If you have successfully tried the example code, now it's time to dive deeper by checking the [Dust3D Script Reference](http://docs.dust3d.org/en/latest/script_reference.html), to see a full API and attributes list. You can also check the Procedural Tree example from the Open Example menu which requires [1.0.0-beta.22](https://github.com/huxingyi/dust3d/releases/tag/1.0.0-beta.22) and above versions.

Dust3D is very young, any contributions are welcome, if you have any suggestions or want contribute a new feature please don't hesitate to raise a issue [here](https://github.com/huxingyi/dust3d/issues) or make a pull request.

Last, I use my Procedural Tree v3.0 to end this article, please enjoy your procedural generation and welcome to share your script and screenshot to [our forum](https://dust3d.discourse.group/).

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Day 108 Procedural Tree V3.0 <a href="https://twitter.com/hashtag/10minuteseveryday?src=hash&amp;ref_src=twsrc%5Etfw">#10minuteseveryday</a> <a href="https://twitter.com/hashtag/Dust3D?src=hash&amp;ref_src=twsrc%5Etfw">#Dust3D</a><br><br>This one take a long time to generate on my MacBook Pro.<br><br>Model: <a href="https://t.co/ld2Ef5aVRH">https://t.co/ld2Ef5aVRH</a><a href="https://twitter.com/hashtag/gamedev?src=hash&amp;ref_src=twsrc%5Etfw">#gamedev</a> <a href="https://twitter.com/hashtag/indiedev?src=hash&amp;ref_src=twsrc%5Etfw">#indiedev</a> <a href="https://twitter.com/hashtag/lowpoly?src=hash&amp;ref_src=twsrc%5Etfw">#lowpoly</a> <a href="https://twitter.com/hashtag/3dmodeling?src=hash&amp;ref_src=twsrc%5Etfw">#3dmodeling</a> <a href="https://twitter.com/hashtag/proceduralgeneration?src=hash&amp;ref_src=twsrc%5Etfw">#proceduralgeneration</a> <a href="https://twitter.com/hashtag/javascript?src=hash&amp;ref_src=twsrc%5Etfw">#javascript</a> <a href="https://twitter.com/hashtag/3d?src=hash&amp;ref_src=twsrc%5Etfw">#3d</a> <a href="https://t.co/EsS7yon25a">pic.twitter.com/EsS7yon25a</a></p>&mdash; Jeremy HU (@jeremyhu2016) <a href="https://twitter.com/jeremyhu2016/status/1155591189862600704?ref_src=twsrc%5Etfw">July 28, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
