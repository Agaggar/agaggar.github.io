---
layout: project
permalink: /:title/
category: industry
ai_drafted: true

meta:
  keywords: "Optimal Transport, MPC, Multi-Agent Manipulation, Human-Robot Collaboration"

project:
  title: "Optimal Transport for Multi-Agent Coordination"
  type: "Honda Research Institute | MPC | Optimal Transport"
  logo: "/assets/images/industry/hri/collaborative-pusht.gif"
  date: Feb. 2026 – May 2026
---
<br>
<span class="h2">Role:</span>
<p>Ph.D. Research Intern, Human-Robot Collaboration Team, Honda Research Institute (San Jose, CA)</p>
<span class="h2">Mentor:</span>
<p>Peter Trautman (also my co-author on <a href="/fast_kes/">Fast Ergodic Search with Kernel Functions</a>)</p>
<span class="h2">Skills:</span>
<p>Optimal Transport, Model Predictive Control, PyTorch, ROS 2, MoveIt</p>

<p class="h2">Motivation:</p>
<p>The question I spent the internship on: when does collaboration actually help? Intuitively, two agents working independently should beat one agent, and two agents working <em>together</em> should beat two agents working independently. But that isn't always true. For a lot of tasks, "you go left, I'll go right" is as good as it gets, and trying to coordinate just adds overhead. I wanted to find tasks where coordinating is genuinely needed, and figure out how to design algorithms for it.</p>

<p class="h2">What I did:</p>
<p>I picked a co-manipulation task: two end effectors pushing a T-shaped block into a goal region (a two-agent version of PushT). Each agent plans with a closed-loop, receding-horizon MPC (cross-entropy method), which gives a distribution over its own future trajectories. The interesting part is how to combine those two marginals into a joint plan. I compared a single agent, two independent agents, and a few ways of coupling them, ending with an optimal transport (OT) formulation that respects both agents' marginals while choosing a joint action.</p>
<p>Qualitatively, the naive couplings either averaged away the useful modes and got stuck in local minima, or had the agents getting in each other's way. The OT version recovered from those local minima. My favorite behavior: one end effector acts as a pivot while the other pushes, which independent agents never figured out.</p>
<p>On the side, I set up a robot arm on hardware, including position and velocity control and a PR for ROS 2 Foxy MoveIt support.</p>

<!-- TODO(ayush): PushT two-agent video -->
<!--
<video class="custom-video" autoplay loop muted playsinline controls>
    <source src="/assets/images/industry/honda/TODO.mp4" alt="two-agent PushT with optimal transport coordination" type="video/mp4">
</video>
-->

<!-- TODO(ayush): robot arm hardware video -->
<!--
<video class="custom-video" autoplay loop muted playsinline controls>
    <source src="/assets/images/industry/honda/TODO.mp4" alt="robot arm hardware" type="video/mp4">
</video>
-->
