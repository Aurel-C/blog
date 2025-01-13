---
title: "Self-Supervised Learning"
date: 2025-01-12T23:24:55+01:00
draft: true
math: true
---

When you want to train a deep learning model to estimate depth from images, but this usually requires a large amount of labeled data. Instead, could we train a model to estimate depth from images without any labeled data? This is the idea behind self-supervised learning.


First here is how supervised learning works:
![Supervised_Training](/supervised.svg)

In supervised learning, we don't have annotations so we need to get the graident from elsewhere. One way to do this is to use the photometric error. The photometric error is the difference between the original image and the image warped using the estimated depth. The goal is to minimize this error.
![Self-Supervised_Training](/ssl.svg)

More precisely, the warping is done like this:
![Warping](/warping.svg)

To get the color of the warped pixel at position \((x, y)\) we need to find where it projects in the image at \(T_0\), in position \((x_0, y_0)\).
Whith the camera intrinsic \(K\) and motion matrix \(M\) we can find \((x_0, y_0)\) with:

\[d_0 \begin{bmatrix} x_0 \\ y_0 \\ 1 \end{bmatrix}= K M K^{-1} d \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}\]