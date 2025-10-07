---
layout: research
permalink: /:title/
category: research

meta:
  keywords: "NeRFs, Hardware, Vision"

project:
  title: "NeRF-Control: Perception-Aware Trajectory Optimization"
  type: "2026 Intl. Conference on Robotics and Automation [Submitted]"
  authors: <a>A. Gaggar</a>, T. Murphey
  # url: "https://murpheylab.github.io/nerf-control/nerf_control"
  logo: "assets/images/research/nerf_control/nerf_control_hardware.GIF"
  tech: "NeRFs, PyTorch, MLPs, Vision, Uncertainty Quantification"

---
<p class="h3" style="color: #7a995d">TLDR: </p>
<p>
Perception models neglect the motion costs of physical sensing agents to acquire training data, such as execution time, total distance traveled, or energy expenditure. In this work, we present a perception-aware objective function for trajectory optimization that jointly balances reducing model uncertainty, ensuring scene coverage, and minimizing total distance traveled. This objective is used to develop an iterative trajectory optimization framework for closed-loop, active data acquisition. To our knowledge, this is the first work to formulate NeRF-aware trajectory optimization for active data collection under perception objectives and motion constraints.</p>
<br>
<p>Furthermore, we demonstrate autonomously trained NeRFs on a 7-DoF robotic arm by executing optimized view trajectories for two tabletop objects. <span style="color: #a9c191">Training NeRFs on hardware brings its own challenges</span>, with reconstructed models differing in position, orientation, and scale from ground truth validation images. Lighting inconsistencies, motion blur, and defocus must also be addressed. On average, our method achieves <span style="color: #a9c191">33% better performance compared to SOTA methods. </p>

<p class="h2">Background:</p>
<p>
Robots that collect data for perception, mapping, or modeling incur motion costs: every new viewpoint consumes time, energy, and potentially introduces safety risks. Yet most research in neural radiance fields (NeRFs) has focused on reconstruction quality and training efficiency, assuming new training data can be acquired instantaneously and for free. The gap between perception-driven, active view selection and dynamics aware trajectory planning is critical to overcome
to deploy NeRFs on physical agents.
<br><br>
Prior work has focused on <i>which</i> views to collect but not <i>how</i> to collect them efficiently. Our work formulates a perception-aware objective for continuous trajectory optimization, optimizing both NeRF-specific objectives and the physical cost of data acquisition. This enables motion-efficient, online data collection for NeRFs on real robots.<br><br>

Our contributions are:<br>
1) A differentiable objective function for trajectory optimization that balances reducing NeRF model uncertainty, ensuring scene coverage, and minimizing motion cost of an agent.<br>
2) Developing the objective within an iterative trajectory optimization framework with a continuous dynamics model to create discrete viewpoints for NeRF training.<br>
3) End-to-end, online evaluation in simulation and on a 7-DoF robot arm. In simulation, our method achieves 33% higher reconstruction accuracy with 39% reduced trajectory length compared against uniform and TSP-based baselines; in hardware, we achieve better reconstruction, while taking 54% less time on average for the robot to execute our trajectory.<br><br>
</p>

<p>Website with code, videos, and interactive figures will be published after ICRA review.</p>

<!-- <video class="custom-video" autoplay loop muted playsinline controls>
  <source src="/assets/images/research/low_data_nerf/hardware_nerf.mp4" type="video/mp4" alt="hardware nerf">
</video> -->
