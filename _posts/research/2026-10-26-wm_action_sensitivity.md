---
layout: research
permalink: /:title/
category: research
ai_drafted: true

meta:
  keywords: "World Models, Model-Based RL, Sensitivity Analysis"

project:
  title: "Does Your World Model Know Actions Have Consequences?"
  type: "2026 CoRL Workshop: Do Robots Need World Models? [Non-archival]"
  authors: <a>A. Gaggar</a>, J. Berry, T. Murphey
  url: "https://do-robots-need-world-models.github.io"
  logo: "/assets/images/research/world_models/ap-metric-sketch.png"
  tech: "World Models, TD-MPC2, MuJoCo, Meta-World, PyTorch, Sensitivity Analysis"
---
<!-- TODO(ayush): add arXiv/OpenReview link -->

<p class="h3" style="color: #7a995d">TLDR: </p>
<p>
Do metrics actually measure the intended benefit of world models? World models provide <span style="color: #a9c191">decision transparency</span> by predicting dynamics without physical rollouts. We need new metrics that evaluate <span style="color: #a9c191">counterfactual predictive accuracy</span> in order to have reliable auditors of end-to-end learning systems.</p>

<p class="h2">Motivation:</p>
<p>
Current world model metrics do not isolate the utility of the dynamics predictor. A world model can have blurry, low-quality reconstructions and still be a great planner. A policy can succeed 100% of the time in distribution and still fall apart the moment it leaves its training data. Neither of those tells you whether the model gets the <em>consequences of an action</em> right, which is the whole reason to have a world model in the first place.</p>
<img src="/assets/images/research/world_models/motivation.png" alt="Left: blurry decoder output vs. ground truth. Right: a policy with 100% in-distribution success vs. the same policy failing out of distribution.">

<p class="h2">Overview:</p>
<p>
An end-to-end learning system is a stack of components: perception, dynamics, a planner, and a reward. Each one already has its go-to metric: reconstruction accuracy for perception, prediction error for dynamics, and task performance for the planner and reward. But those metrics overlook the unique benefit of world models: the <span style="color: #a9c191">fidelity of action-conditioned dynamics</span>. Action sensitivity analysis can audit dynamics prediction, which would otherwise be impossible without physical rollouts.</p>

<p class="h2">Methodology:</p>
<p>
Similar to classic input-output dynamic models, world model fidelity can be measured with standard sensitivity analysis: impulse responses in the action space. The Action Perturbation (AP) metric nudges the nominal controls, then compares how much the world model <em>thinks</em> the outcome changed against how much it <em>actually</em> changed in the environment, over a horizon.
<br><br>
A score of 0 is perfect, and a score of 1 is what you get from a model that ignores the action entirely, so anything above 1 is worse than ignoring it. Because it's a difference of differences, a constant bias in the predicted state cancels out, which makes it a different question from state error.</p>
<img style="display: block; width: 60%; height: auto; margin: 0 auto;" src="/assets/images/research/world_models/ap-metric-sketch.png" alt="Sketch of the AP metric: perturb an action, compare predicted vs. true change in next state.">
<p>
To test it, we froze a released TD-MPC2 model and retrained only the dynamics head on 100k interactions from three data regimes: a workspace raster, imitation learning, and imitation learning with injected noise. We evaluated on two Meta-World tasks, Push and Peg insertion.</p>

<p class="h2">Results:</p>
<p>
State error and AP disagree. The imitation learning and noise-injected heads have similar state error, but the noise-injected head is about 16% (Push) and 48% (Peg) better on AP. Imitation learning looks fine on state error and turns out brittle once actions leave its demonstrations. Depending on the application (surgery, warehouses, home robots, space), roboticists have to make tradeoffs between <span style="color: #a9c191">accurate action sensitivity</span> and <span style="color: #a9c191">low state error</span>.</p>
<img style="display: block; width: 60%; height: auto; margin: 0 auto;" src="/assets/images/research/world_models/ap_vs_state_error.png" alt="AP vs. state error for workspace raster, imitation learning, and noise-injected data, with application icons.">

<p class="h2">What if...</p>
<p>
&bull; Action sensitivity didn't require precisely resetting the system state?<br>
&bull; Planning utility were directly related to action sensitivity? Does a better dynamics predictor naturally lead to better task performance?</p>

<p>OpenReview/arXiv link coming soon.</p>
