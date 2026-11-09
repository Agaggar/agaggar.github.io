---
layout: project
permalink: /:title/
category: projects
ai_drafted: true

meta:
  keywords: "World Models, Data Collection, Information Theory, Affordance Discovery, Exploration"

project:
  title: "Information-Theoretic Data Collection for Affordance Discovery in World Models"
  type: "World Models | Data Collection | Information Theory"
  logo: "/assets/images/research/world_models/hardware-pixel.gif"
  date: Nov. 2025 – Mar. 2026
---
<br>
<span class="h2">Skills:</span>
<p> World Models, PyTorch, Information Theory, Data Collection</p>

<!-- TODO(ayush): add cover image/video once the paper is public -->

<p class="h2">Goal:</p>
<p>A world model is only as good as the data it's trained on. If the robot never opens the drawer, the model has no idea what opening the drawer does, and any plan that depends on it is a guess. So the question I've been working on is less "how do we build a better world model" and more "what data should a robot go collect to train one?"</p>
<br>

<p>By "affordance" I mean the interactions the environment actually offers: things that move, open, slide, or respond when the robot acts on them. Those are the parts of the state space a world model most needs to get right, and they're also the easiest to miss. Random actions mostly flail in free space and rarely make meaningful contact. Collecting data for one task covers that task and not much else. Demonstrations are expensive and only show what the demonstrator thought was worth doing.</p>
<br>

<p>The goal is a data collection objective that pushes the robot toward interactions its world model doesn't understand yet, without a task or reward telling it where to look. The implementation ends up similar to the data coverage methods discussed in <a href="https://www.nicklashansen.com/mmbench2/">Hallucination in World Models is Predictable and Preventable</a>, like coverage-aware resampling and hallucination-guided collection, which steer data toward where the world model is likely to be wrong.</p>

<p class="h2">Status:</p>
<p>The paper is under review, so this page sticks to the problem for now! Method and results will go up once it's public.</p>
