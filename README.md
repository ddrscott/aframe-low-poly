You can view the demo pictured below at [aaalv.in/vr/low-poly-trees](http://alvinwan.com/vr/low-poly-trees).

<img width="1203" alt="screen shot 2018-11-24 at 11 32 11 pm" src="https://user-images.githubusercontent.com/2068077/48976744-31921d80-f041-11e8-8aa3-1959bc6fa65b.png">

# A-Frame Low Poly

[View the aframe low-poly demo &raquo;](http://alvinwan.com/aframe-low-poly/demo)

Low poly add-ons for a-frame virtual reality models. Take any existing a-frame
primitive, such as `a-sphere` and replace the prefix to obtain a low-poly
version, such as `lp-sphere`. For example, the below is a low-poly sphere
for a tree's foliage:

```
<lp-sphere position="0 0.6 0"
           color="#59810C"
           radius="1"
           segments-width="10"
           segments-height="10"
           amplitude="0.2"></lp-sphere>
```

To get started, include the minified javascript in your a-frame project.

```
<script src="https://cdn.jsdelivr.net/gh/alvinwan/aframe-low-poly@0.0.3/dist/aframe-low-poly.min.js"></script>
```

# Usage

## Low-Poly Attributes

Every low-poly object supports the following attributes. Modify the following attributes just like you would any other AFrame VR attribute:

**`max-amplitude: <x double> <y double> <z double>`**

**`min-amplitude: <x double> <y double> <z double>`**

Maximum and minimum amount of perturbation allowed for each vertex. The vertex will not be moved more or less than this amount away from the original position.

Example:

```
<lp-plane max-amplitude="1 0 0" min-amplitude="0.5 0 0"></lp-plane>
```

**`seed`**

Seed for random-number generator, allowing you to fix randomness during design.

> **`max-amplitude-difference: <x double> <y double> <z double>`** *coming soon*
>
> **`min-amplitude-difference: <x double> <y double> <z double>`** *coming soon*
>
> Maximum and minimum difference in perturbation between adjacent points. For now,
> use the curvature specification below to achieve a similar effect.

## Terrain

**`LowPolyTerrain.registerCurvature(componentName, function({x, y, z}, {xmin, ymin, zmin}, {xmax, ymax, zmax})`**

Allows you to specify curvature of the surface. Function that accepts the vertex's *original position* and outputs the vertex's new position. This is applied *before* customizable randomization. All random perturbations are applied to the vertex's new position.

Example:

```
LowPolyTerrain.registerCurvature('sine', function (vertex, min, max) {
    var py = (vertex.y - min.y) / (max.y - min.y);
    var z = Math.sin(py * 2 * Math.PI) + min.z;
    return {x: vertex.x, y: vertex.y, z: z}
});
```

## Projects

Projects that use `aframe-low-poly`:

- Ergo ([aaalv.in/ergo](http://alvinwan.com/ergo)): an endless runner game
- Tree Editor ([trees.aaalv.in](http://trees.alvinwan.com)): a simplistic low-poly tree editor
- Tree Carousel ([aaalv.in/vr/low-poly-trees](http://alvinwan.com/vr/low-poly-trees)): a demo carousel for low-poly trees
