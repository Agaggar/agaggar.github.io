---
layout: project
permalink: /:title/
category: industry
ai_drafted: true

meta:
  keywords: "Audio-Visual Separation, Sound Source Separation, Diffusion Transformers, Flow Matching, LoRA"

project:
  title: "Joint Audio-Visual Sound Decomposition"
  type: "Dolby Laboratories | Audio-Visual Separation | Flow Matching"
  logo: "/assets/images/industry/dolby/ft_sam_fm_architecture.png"
  date: May 2026 – Aug. 2026
---
<br>
<span class="h2">Role:</span>
<p>Ph.D. Research Intern, Multimodal Lab, Dolby Laboratories (San Francisco, CA)</p>
<span class="h2">Mentor:</span>
<p>Lie Lu</p>
<span class="h2">Skills:</span>
<p>PyTorch, Diffusion Transformers, Flow Matching, LoRA, Audio-Visual Learning</p>

<p class="h2">Motivation:</p>
<p>We often see things we don't hear, and hear things we don't see. Picture a street video: you can see people walking and flags moving (silent), and you can hear a motorcycle that never shows up in frame (off-screen). If you want to tie each sound to the object making it, you have to deal with that asymmetry.</p>
<p>Current sound separation models like SAM-Audio work one prompt at a time: give it an object, get back that object's sound and everything else. With K objects in a scene, that's K separate forward passes, each one blind to the others. That felt wasteful to me, and it seemed like the model should do better if it could reason about all the objects at once.</p>

<p class="h2">What I did:</p>
<p>I built an audio-visual separation framework for object-level sound decomposition: split a scene's audio across the objects in it, and flag the mismatches (silent-but-visible objects and off-screen sounds). To do that, I fine-tuned SAM-Audio with LoRA, modified its diffusion transformer with cross-attention, and introduced a flow-matching objective so the audio sources are decomposed jointly instead of one prompt at a time.</p>
<p>Real videos don't come with clean, per-object ground truth audio, so I also built a synthetic audio-visual dataset to evaluate object-conditioned separation in a controlled setting.</p>

<!-- TODO(ayush): add approved figure -->
<!-- <img src="/assets/images/industry/dolby/TODO.png" alt="joint audio-visual decomposition pipeline"> -->
