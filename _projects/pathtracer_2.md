---
layout: page
title: Pathtracer (Part 2)
description: raytracing - expansion
img: assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_100.png
importance: 4
category: graphics
---
**Irene Geng and Mingyang Wang**

In this project:
- Expanding the functionality of our raytracer to render additional materials, including mirror (reflective), glass (refractive), and microfacet surfaces.
- Implementing environment lighting, which allows us to simulate incident radiance from every direction on the sphere.
- Implementing a thin lens model for the camera, which allows us to simulate different depth of field effects by adjusting the lens radius and focal distance.


### Part 1: Mirror and Glass Materials.

Here is a sequence of 7 images of CBspheres.dae rendered with max ray depth set to 0, 1, 2, 3, 4, 5, and 100. We used 256 samples per pixel and 4 samples per light.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_0.png" caption="m = 0" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_1.png" caption="m = 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_2.png" caption="m = 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_3.png" caption="m = 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_4.png" caption="m = 4" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_5.png" caption="m = 5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="text-center">
  <img src="/assets/img/pathtracer_2/Part1/Writeup_1.1_spheres_256_4_100.png" class="mx-auto d-block img-fluid rounded z-depth-1" alt="Centered Image">
  <figcaption class="caption">m = 100</figcaption>
</div>

When the max ray depth is 0, we only see zero-bounce lighting from the area light on the ceiling, and nothing in the scene is illuminated.

For m = 1, we only see direct lighting, which includes zero- and one-bounce lighting; the shadows are black, similar to in Project 3-1. Additionally, the spheres are black, as it takes at least two light bounces for the glass effects of the spheres to be rendered properly (discussed more below).

At all higher max ray depths (m > 1), the image is rendered with global illumination. We note that the left sphere is reflective and the right sphere is refractive.

For m = 2, the left sphere begins to show a reflection of the environment’s direct lighting from the m = 1 step (we note that the ceiling and other sphere are black, like in the m = 1 case). We see a faint reflection on the right sphere, but do not yet see any refraction (refraction needs at least three bounces, as it must enter and exit the sphere as opposed to reflection just bouncing once).

For m = 3, the left sphere shows a reflection of the m = 2 case (thus containing global illumination, but the other sphere is still black), and the right sphere’s glass material is finally beginning to show refraction properly; this is the first image in the sequence that shows the caustic effect.

For m = 4, the left sphere’s reflection finally shows the refractive effects of the right sphere (and thus looks like glass). We see a spot of light that has been refracted through the right sphere to land on the right wall of the box.

The images rendered with m = 5 and m = 100 look quite similar, with no major additional multibounce effects. The images generally appear less noisy, especially the spot of light on the right wall.


### Part 2: Microfacet Materials

Here is a sequence of 4 images of CB_dragon_microfacet_au.dae rendered with $$\alpha$$ set to 0.005, 0.05, 0.25, and 0.5. We used 256 samples per pixel, 4 samples per light, and max ray depth of 7.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.1_dragon_256_4_7-0.005.png" caption="alpha = 0.005" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.1_dragon_256_4_7-0.05.png" caption="alpha = 0.05" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.1_dragon_256_4_7-0.25.png" caption="alpha = 0.25" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.1_dragon_256_4_7-0.5.png" caption="alpha = 0.5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We observe that as we increase $$\alpha$$, the dragon looks less and less glossy and more matte-like. Another interesting thing of note is that a higher $$\alpha$$ results in a slightly noisier image, likely due to the increased amount/intensity of reflections.

Here are two images of CBbunny_microfacet_cu.dae rendered using cosine hemisphere sampling and our importance sampling. We used 64 samples per pixel, 1 sample per light, and max ray depth of 5.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.2_bunny_64_1_5-cosine.png" caption="Cosine Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.2_bunny_64_1_5-importance.png" caption="Importance Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We see that the cosine sampling case does not converge as well as the importance sampling case: the bunny is a lot darker/less well lit, and both the bunny and the surrounding environment are a lot more noisy. Importance sampling shows a much better lit bunny, and the bunny has a lot better color and metallic look. However, there is still a noticeable amount of noise on the surrounding walls, which can be fixed with more samples.

Here are images of CB_lucy_hg.dae with modified *eta* and *k* values. We used parameters corresponding to titanium and cesium metal.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.3_lucy_1024_8_5-Ti.png" caption="Titanium" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part2/Writeup_2.3_lucy_1024_8_5-Cs.png" caption="Cesium" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The titanium Lucy looks silvery, while the cesium Lucy is yellow and gold-like. Cesium is liquid at room temperature and highly reactive, but coding those effects were out of scope for this project and left as an exercise for the reader.


### Part 3: Environment Light

We used grace.exr for the images in this part of the write-up. Here is a converted .jpg of the environment map.

<div class="text-center">
  <img src="/assets/img/pathtracer_2/Part3/grace.jpg" class="mx-auto d-block img-fluid rounded z-depth-1" alt="Centered Image">
  <figcaption class="caption">grace.jpg</figcaption>
</div>

Environment lighting simulates incident radiance from every direction on the sphere, from a light source that is infinitely far away. We can use environment lighting to model real-world light sources and environments. For example, the environment lighting of grace.exr simulates the lighting inside of a large cathedral, with direct light sources from multiple lamps and stained glass windows and indirect bounce lighting from every surface.

Here is the probability_debug.png file for grace.exr, generated using the save_probability_debug() function.

<div class="text-center">
  <img src="/assets/img/pathtracer_2/Part3/probability_debug.png" class="mx-auto d-block img-fluid rounded z-depth-1" alt="Centered Image">
  <figcaption class="caption">Probability Debug</figcaption>
</div>

Here is bunny_unlit.dae and grace.exr rendered with uniform sampling and importance sampling. We used 4 samples per pixel, 64 samples per light, and max ray depth of 7.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part3/Writeup_3.3_bunny_unlit_4_64_7-uniform.png" caption="Uniform Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part3/Writeup_3.3_bunny_unlit_4_64_7-importance.png" caption="Importance Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The image rendered with importance sampling is much less noisy than the uniform sampling image. The uniform sampling image is almost entirely dark, with specks of color scattered on the model surface. It is additionally somewhat difficult to see the bunny’s shape in the uniform sampling image.

Here is bunny_microfacet_cu_unlit.dae and grace.exr rendered with uniform sampling and importance sampling. We used 4 samples per pixel, 64 samples per light, and max ray depth of 7.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part3/Writeup_3.4_bunny_microfacet_unlit_4_64_7-uniform.png" caption="Uniform Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part3/Writeup_3.4_bunny_microfacet_unlit_4_64_7-importance.png" caption="Importance Sampling" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The image rendered with importance sampling is significantly less noisy and is brighter than the uniform sampling image. Moreover, the bunny has a distinct metallic look in the importance sampling image, but has a very limited effect in the uniform sampling image. The uniform sampling image is much more noisy: the copper material of the bunny model and the pillow it’s placed on has many small bright specks (while there are much fewer in the importance sampling image).


### Part 4: Depth of Field

In a pinhole camera model, we assume a perfect lens aperture of 0. As a result, every point in the scene appears in focus, as all the rays pass through one individual “pinhole” point in the camera, so every point in camera space receives radiance from a single point.

In the thin-lens camera model, the camera has a lens (of non zero aperture) that bends and refracts light. Only points that lie at the plane of focus (based on the camera’s focal length) will appear exactly in focus, while points in front or behind the plane of focus will be out of focus and blurred. A point in camera space receives radiance from any point on the thin lens, so we must uniformly sample over the thin lens disk.

Here is CBdragon_microfacet_au.dae focused at 4 visibly different depths. We used 512 samples per pixel, 4 samples per light, and an aperture of 0.23.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.2_512-64_0.05_12_4_0.23_4.5.png" caption="d = 4.5" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.2_512-64_0.05_12_4_0.23_4.8.png" caption="d = 4.8" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.2_512-64_0.05_12_4_0.23_5.png" caption="d = 5" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.2_512-64_0.05_12_4_0.23_6.png" caption="d = 6" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

As the focal length increases, the plane of focus moves farther back. The above sequence of images shows the plane of focus at the head of the dragon, the body of the dragon, the tail of the dragon, and the back wall of the Cornell Box.

Here is CBbunny_microfacet_cu.dae rendered with 4 different aperture sizes, all with a focal length of 4.6 (focused on the head of the bunny). We used 512 samples per pixel and 4 samples per light.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.3_bunny_512-64_0.05_12_4_0.05_4.6.png" caption="b = 0.05" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.3_bunny_512-64_0.05_12_4_0.3_4.6.png" caption="b = 0.3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.3_bunny_512-64_0.05_12_4_0.6_4.6.png" caption="b = 0.6" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pathtracer_2/Part4/Writeup_4.3_bunny_512-64_0.05_12_4_1_4.6.png" caption="b = 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

As the aperture size increases, the depth of field decreases. When b = 0.05, we see that everything is in focus. However, when b = 0.3 and b = 0.6, we see that the walls of the Cornell Box, the edges of the light on the roof, and the back ear of the bunny begin to appear out of focus. When b = 1, the edges of the back all are almost indistinguishable, and the ears of the bunny are almost entirely blurred out.
