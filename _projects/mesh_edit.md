---
layout: page
title: Mesh Edit
description: CS 184 - Computer Graphics and Imaging
img: assets/img/mesh_edit/teapot.png
importance: 1
category: Graphics
---

In this project:
- Evaluating Bezier curves and surfaces with de Casteljau subdivision
- Implementing mesh operations: edge flips and splits
- Upsampling meshes with loop subdivision

## Section I: Bezier Curves and Surfaces
### Part 1: Bezier Curves with 1D de Casteljau Subdivision

de Casteljau’s algorithm is a recursive method for evaluating Bezier curves. Given $$t$$, a parameter
that varies from zero to one, and $$n$$ control points, one iteration of de Casteljau’s algorithm will
calculate the next $$n - 1$$ intermediate control points by using linear interpolation between every
pair of consecutive control points. Given two control points $$p_{0}$$ and $$p_{1}$$ and a value for $$t$$, we can calculate the weighted average as
$$(1 - t) \cdot p_{0} + t \cdot p_{1}$$

This sequence shows six levels of Bezier curve evaluation, from the original control points down to the final evaluated point and the complete Bezier curve.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level0.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level1.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level2.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level3.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level4.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_level5.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bcurve_full.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Part 2: Bezier Surfaces with Separable 1D de Casteljau

Given an $$n \times n$$ grid of control points, we can use the separable application of
de Casteljau’s algorithm along the two different axes to evaluate the points of a
Bezier surface.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/bsurface.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Utah teapot.
</div>

## Section II: Triangle Meshes and the Half-Edge Data Structure
### Part 3: Area-Weighted Vertex Normals

For a vertex in a geometric mesh, we calculate its area-weighted vertex normal as
the normalized average of the surface normal vectors of the vertex's surrounding
faces, where each surface normal vector is weighted by the area of its face.
We can use these area-weighted vertex normals for Phong shading.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/part3_flat.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mesh_edit/part3_phong.png" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Phong shading (right) produces smoother results than flat shading (left).
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
