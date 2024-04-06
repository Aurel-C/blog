---
title: "Self-supervised Depth Estimation"
date: 2024-04-01T14:15:35+02:00
math: true
math: true
ShowBreadCrumbs: false
---

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

<!-- 
Block math:

$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } }
$$ -->

When you want to train a deep learning model to estimate depth from images, but this usually requires a large amount of labeled data. Instead, could we train a model to estimate depth from images without any labeled data? This is the idea behind self-supervised learning.


First here is how supervised learning works:
![Supervised_Training](/supervised.svg)

In supervised learning, we don't have annotations so we need to get the graident from elsewhere. One way to do this is to use the photometric error. The photometric error is the difference between the original image and the image warped using the estimated depth. The goal is to minimize this error.
![Self-Supervised_Training](/ssl.svg)

More precisely, the warping is done like this:
![Warping](/warping.svg)

{{< math.inline >}}
To get the color of the warped pixel at position \((x, y)\) we need to find where it projects in the image at \(T_0\), in position \((x_0, y_0)\).
Whith the camera intrinsic \(K\) and motion matrix \(M\) we can find \((x_0, y_0)\) with:
  \[d_0 \begin{bmatrix}
           x_0 \\
           y_0 \\
           1
         \end{bmatrix}= K M K^{-1} d \begin{bmatrix}
           x \\
           y \\
           1
            \end{bmatrix}\]


{{</ math.inline >}}
