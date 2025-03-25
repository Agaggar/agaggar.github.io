---
layout: project
permalink: /:title/
category: research

meta:
  keywords: "Ergodic Search, Kernel, Lie Groups"

project:
  title: "Fast Ergodic Search with Kernel Functions"
  type: "Jekyll"
  url: "https://maxsun.io/post/2024-arxiv-kes/"
  logo: "/assets/images/projects/yellowpineapple/logo.png"
  tech: "HTML, CSS, Boostrap, Sass, JavaScript, jQuery, Jekyll"

# agency:
#   title: "Yellow Pineapple Co"
#   url: "https://github.com/arnolds/pineapple"
#   year: "2017, 2018"

images:
  - image:
    url: "/assets/images/projects/yellowpineapple/devices.jpg"
    alt: "Yellow Pineapple website on tablet, mobile and desktop"
  - image:
    url: "/assets/images/projects/yellowpineapple/desktop.jpg"
    alt: "Yellow Pineapple website on a desktop device"
  - image:
    url: "/assets/images/projects/yellowpineapple/mobile.jpg"
    alt: "Yellow Pineapple website on a mobile device"
---
<p>Ergodic search enables optimal exploration of an information distribution while guaranteeing the asymptotic coverage of the search space. However, current methods typically have exponential computation complexity in the search space dimension and are restricted to Euclidean space. We introduce a computationally efficient ergodic search method. Our contributions are two-fold. First, we develop a kernel-based ergodic metric and generalize it from Euclidean space to Lie groups. We formally prove the proposed metric is consistent with the standard ergodic metric while guaranteeing linear complexity in the search space dimension. Secondly, we derive the first-order optimality condition of the kernel ergodic metric for nonlinear systems, which enables efficient trajectory optimization. Comprehensive numerical benchmarks show that the proposed method is at least two orders of magnitude faster than the state-of-the-art algorithm. Finally, we demonstrate the proposed algorithm with a peg-in-hole insertion task. We formulate the problem as a coverage task in the space of SE(3) and use a 30-second-long human demonstration as the prior distribution for ergodic coverage. Ergodicity guarantees the asymptotic solution of the peg-in-hole problem so long as the solution resides within the prior information distribution, which is seen in the 100% success rate.</p>