---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Latent Space, Control, Autoencoders"

project:
  title: "Control and Planning in the Latent Space"
  type: "ML | Variational Autoencoders"
  logo: "/assets/images/projects/latentplanning/shooting_method.gif"
  date: Ongoing [Mar. 2025]
---
<br>
<span class="h2">Skills:</span>
<p> MLPs, PyTorch, Autoencoders</p>
<p class="h2">Description</p>

<p>Goal: Given a target image, a control method of choice is applied in the latent space to control the system towards the goal image. The model only has access to <em>images</em> (the two previous images) with no state observations and a control input to predict the next image.</p>

<p>Method 1: Re-implementing <a href="https://arxiv.org/pdf/1506.07365">Embed to Control</a>. The images are passed through a VAE, the latent variables are passed through several MLPs to calculate the A, B, and disturbance matrices needed for linear control. (z_next = A * z_t + B * u_t) Given that the latent dynamics model is enforced to be locally linear, optimal control (like iLQR) can be applied.
Pros: Enforcing local linearity in the system
Cons: Struggles for more than one-step predictions; have to replan
In the video, I employ iLQR with a horizon of 5 timesteps and replan after executing one control step.</p>
<br>
<video class="custom-video" autoplay loop muted playsinline controls>
    <source src="/assets/images/projects/latentplanning/iLQR.gif" alt="iLQR control for cartpole balancing" type="video/mp4">
</video>

<p>Method 2: A variant on <a href="https://danijar.com/project/planet/">PlaNet</a>: The images are passed through a VAE, the latent variables are passed through a deep RNN to predict the next latent state mean and variance, which is then passed through a decoder. Although optimal control can't be predicted, you can use MPC methods to guide control (like a random shooting method).
Pros: Simpler architecture, better future predictions, better response to control inputs
Cons: No linearity
In the video, I employ a random shooting method (simulate 20 trajectories, take the control action that most minimizes the latent difference, then replan).</p>

<br>
<video class="custom-video" autoplay loop muted playsinline controls>
    <source src="/assets/images/projects/latentplanning/shooting_method.mp4" alt="Random shooting method, MPC control for cartpole balancing" type="video/mp4">
</video>
<!-- <img src="/assets/images/projects/latentplanning/shooting_method.gif" alt="Random shooting method, MPC control for cartpole balancing"> -->

<p>Performance comparison: both succeed at roughly the same rate (not rigorously tested) and take similar amounts of training time (didn't check compute cost). My hunch is that the RNN would perform better at more complicated tasks, which is probably why papers like Dreamer use it on hardware.</p>

<p>What I've learned (and also why it took so long):
1. There's 3 "plateaus" to overcome with learning latent dynamics: the unfolding of the latent space; overcoming the trivial solution (the average image of the dataset); and the minimization of the latent KL term. The trivial solution problem specifically plagued me for weeks, and it seems like the best solution is simply more data.
2. Defining "areas" in the latent space to be good or bad (think rewards or CBFs) should be possible. I haven't thought too deeply about this.
3. Matching latent transition predictions with ground truth encoder values needs to happen gradually, and after the encoder/decoder work as expected. Otherwise, you're stuck with the trivial solution.</p>