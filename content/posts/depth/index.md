---
title: "Depth"
date: 2025-01-12T22:30:49+01:00
draft: true
---

## Introduction
Estimating depth from images is very important as it allows the recovery of 3d. It has wide applications in for robotics, intelligent vehicules, augmented and virtual reality, allowing thing like obstacles localisation 3d objects reconstruction. 
There are multiple ways to estimate depth from images and traditionnaly these methods also knowed as photogrammetry require multiple images to recover the depth. If the cameras used to take photos are not knowed we can use methods such as bundle ajustement that works great when we have lots of photos and can be used make 3d models of monuments for example.
However, if we know the cameras that have been used we can go down to only two photos and be able to reconstruct the depth.
Thanks to the avenemet of deep neural networks, we now have methods that are able to reconstruct depth from single images and this is what we will focus on in the next parts. 
 Thanks to the avenemet of deep neural networks, we now have methods that are able to reconstruct depth from single images and this is what we will focus on in the next parts. 

## Perspective Transformation
A fondamental concept to know before everything else is how cameras take objets in the 3D world and are able to reprensent them in 2D images. 
This process be formalized mathematically as a perspective transformation and allows to compute the position (u,v) in an image a point (x, y, z) of the world takes.
To do this transformation two informations are needed about the camera: the optical center (c_x, c_y) and the focal lengths (f_x, f_y).
We then have:

## Monocular depth
When using a single image there are actually a lot of clues that allows to estiamte depth. Here are some of the ones that human use: perpective, relative size , known size, absolute size, occulatation, texture gradient, lighting and shading, elevation.

## Neural Networks
While all of these informations provide very useful information, it is actually very hard to implement concrete algorithm to leverage them since most of them come from the assumption that we already know the objects of the scene while in practice we often want to do the inverse of first estimating depth and then find 3d objects.
That why deep neural networks are escially adapted to this kind of task where we can directly give the network data and optimize it to get a depth estimation function.
The classical way is to record videos with additioanl captors such as lidars that use lasers to estimate the depth on some points of the image and then we can use these data to train our model on these points that are sufficent for the whole model to generalize. 
Synthetic data recorded in virtual worlds like video games or simulation are also often used since they are often easier to obtain and better quality but additional steps are needed to make sure that models trained on these data work with images of the real world
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<div id="3d-container" style="width: 100%; height: 400px;"></div>

<script>
// Three.js scene setup
const container = document.getElementById('3d-container');
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, container.clientWidth / container.clientHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer();

renderer.setSize(container.clientWidth, container.clientHeight);
container.appendChild(renderer.domElement);

// Add a simple cube
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

camera.position.z = 5;

// Animation loop
function animate() {
    requestAnimationFrame(animate);
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    renderer.render(scene, camera);
}
animate();
</script>