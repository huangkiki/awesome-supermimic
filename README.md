<div align="center">

# Awesome SuperMimic

[![Awesome](https://awesome.re/badge.svg)](https://github.com/sindresorhus/awesome) [![Paper](https://img.shields.io/badge/arXiv-2610.28480-b31b1b.svg)](https://arxiv.org/abs/2610.28480) [![License: CC0](https://img.shields.io/badge/License-CC0_1.0-blue.svg)](LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**A curated collection of SuperMimic implementations, extensions, demos, and resources.**

English · [简体中文](README_zh-CN.md)

[Original paper](https://arxiv.org/abs/2610.28480) · [Official website](https://supermimic.github.io/) · [Interactive demo](https://supermimic.github.io/demo/) · [Community projects](#community-projects)

</div>

<p align="center">
  <a href="https://supermimic.github.io/media/world-model/wm_on.mp4"><img src="assets/official/world-model.gif" alt="Official SuperMimic world-model predictions in blue overlaid on simulator motion" width="100%"></a><br>
  <b>World-model predictions</b>
</p>

<table>
  <tr>
    <td width="50%" align="center">
      <a href="https://supermimic.github.io/media/hero/hero_montage_desktop.mp4"><img src="assets/official/simulation-wide.gif" alt="Official SuperMimic simulation: G1 flips, rolls, and dances" width="100%"></a><br>
      <b>Simulation</b>
    </td>
    <td width="50%" align="center">
      <a href="https://supermimic.github.io/media/real/real_bay-wide.mp4"><img src="assets/official/real-g1-wide.gif" alt="Official SuperMimic real G1 performing a side roll and a flip by the bay" width="100%"></a><br>
      <b>Real G1</b>
    </td>
  </tr>
</table>

<p align="center"><sub>Original footage: <a href="https://supermimic.github.io/">SuperMimic authors</a> · Click a preview for the full video · <a href="assets/official/README.md">Media credits</a></sub></p>

Start with the original work below, then choose an implementation by framework and task. This is a community-maintained resource list; the linked implementations are credited to their own authors.

## Contents

- [Original SuperMimic](#original-supermimic)
- [Community projects (38)](#community-projects)
  - 🔬 [Reproductions, methods & frameworks (17)](#reproductions-methods-and-training-frameworks)
  - 👁️ [Perception & terrain (4)](#perception-terrain-and-quadrupeds)
  - 🦾 [Manipulation & hands (4)](#manipulation-and-dexterous-hands)
  - 💪 [Muscles & interaction (3)](#muscle-interaction-and-diagnostics)
  - 🤖 [Robot ports (6)](#robot-porting-and-retargeting)
  - 🚀 [Real robots (2)](#real-robot-deployment-and-sim2real)
  - 💡 [Learning examples (2)](#inspired-experiments)
- [Related methods and baselines](#related-methods-and-baselines)
- [Data and learning resources](#data-and-learning-resources)
- [Contributing](#contributing)
- [Citation](#citation)
- [Acknowledgements and license](#acknowledgements-and-license)
- [Star History](#star-history)

## Original SuperMimic

**[SuperMimic: Scaling Humanoid Whole-Body Control with One Differentiable World Model](https://arxiv.org/abs/2610.28480)**<br>
Qiayuan Liao, Yiyang Shao, Junfeng Long, Kevin Zakka, Roberto Horowitz, Pieter Abbeel, and Koushil Sreenath.<br>
**UC Berkeley · CoRL 2026 Oral**

[Paper](https://arxiv.org/abs/2610.28480) · [PDF](https://arxiv.org/pdf/2610.28480) · [Project](https://supermimic.github.io/) · [Video](https://supermimic.github.io/media/real/film-1080.mp4) · [Browser demo](https://supermimic.github.io/demo/)

SuperMimic learns shared humanoid dynamics from simulator transitions and improves a motion-tracking policy through short imagined rollouts. The world model and policy are updated in the same training loop; policy gradients pass through the learned model. [Method overview](https://supermimic.github.io/#loop).

<p align="center">
  <a href="https://arxiv.org/pdf/2610.28480v1#page=4">
    <img src="assets/official/training-loop.png" width="100%" alt="Original SuperMimic Figure 2: data collection, world-model fitting and policy improvement share a replay buffer; dashed arrows show gradients">
  </a>
</p>
<p align="center">
  <sub>Original paper, Figure 2 · <a href="https://arxiv.org/pdf/2610.28480v1#page=4">Framework, p. 4</a> · <a href="https://arxiv.org/pdf/2610.28480v1#page=15">Algorithm A.1, p. 15</a></sub>
</p>

The world model is fit on **8-step replay windows**; the policy and critic learn from **32-step imagined rollouts**. During the policy update, model weights stay fixed while gradients pass through the model to the policy. Blue dashed arrows show gradients; ❄️ marks frozen weights and 🔥 marks weights being trained in that phase.

The authors report surpassing SONIC's released-checkpoint return after **3 hours on one H100**, with **25 / 129,514 failed motions**, and **0 / 129,514** after 9.8 hours on two H100s. These are training-motion coverage results, with different training hardware and data from SONIC. See the [official results and compute accounting](https://supermimic.github.io/#compute).

**Official code status — checked 2026-10-28:** the official website links the paper, video, and browser demo, but does not link a training-code repository. The projects below are community implementations and extensions.

## Community projects

**38 projects in 7 categories, grouped by purpose.** Each project appears once; overlapping capabilities are described in its entry. The guide retains complementary starting points; ⭐ marks documented experiments, tools or learning examples.

Within each category, **⭐ highlighted projects come first**, followed by the remaining projects; **each group is sorted by GitHub Stars, highest first**. The overview selections follow the same Stars order (2026-10-30 snapshot; ties by repository name). Badges update dynamically; the order does not. Stars reflect repository popularity; results and demos are upstream reports.

<a name="featured-projects"></a>

### ⭐ Featured projects

<table width="100%">
<thead><tr><th align="left" width="32%">Explore</th><th align="left" width="40%">Project · Stars</th><th align="left" width="28%">Highlight</th></tr></thead>
<tbody>
<tr>
<td rowspan="8" valign="top"><a href="#reproductions-methods-and-training-frameworks">🔬&nbsp;Reproduction&nbsp;&amp;&nbsp;training&nbsp;(17)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic_vibed">supermimic_vibed</a></strong>&nbsp;<a href="https://github.com/zita-ch/supermimic_vibed/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/zita-ch/supermimic_vibed.svg?style=social"></a><br>By Chong Zhang</td>
<td valign="top"><strong>Reusable Isaac Lab G1 baseline:</strong> 40/40 LAFAN1 clips completed after 1.47 h training on one RTX PRO 6000 Blackwell; return 0.829.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic-reproduced">SuperMimic-Reproduced</a></strong>&nbsp;<a href="https://github.com/CuboiLeo/SuperMimic-Reproduced/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/CuboiLeo/SuperMimic-Reproduced.svg?style=social"></a><br>By CuboiLeo</td>
<td valign="top"><strong>Large-library reproduction with released weights:</strong> 495/129,943 BONES-SEED training clips fail after 7.1 h on 4× RTX 5090; paper observations, return 0.930.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#unisupermimic">UniSuperMimic</a></strong>&nbsp;<a href="https://github.com/Motphys/Uni-SuperMimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Motphys/Uni-SuperMimic.svg?style=social"></a><br>By Motphys</td>
<td valign="top"><strong>UniLab training-loop and EMA improvements:</strong> 193/129,487 BONES-SEED training clips fail at 8k iterations; return 0.9395 on one RTX 4090 (48 GB reported); optimized-run time unspecified.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#morphmimic">MorphMimic</a></strong>&nbsp;<a href="https://github.com/lzyang2000/morphmimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/lzyang2000/morphmimic.svg?style=social"></a><br>By Lizhi Yang et al.</td>
<td valign="top"><strong>One policy across three bodies:</strong> released ONNX policy for G1, X2 Ultra and T2, plus direct PICO human-motion input; hardware tested on G1 only.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#instanttrack">InstantTrack</a></strong>&nbsp;<a href="https://github.com/Huy-Quang-Dao/instantTrack/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Huy-Quang-Dao/instantTrack.svg?style=social"></a><br>By Huy-Quang-Dao</td>
<td valign="top"><strong>15-minute training on one RTX 5090:</strong> all three seeds reach LAFAN1 return ≥0.82 with 0/40 failed training clips; offline evaluation excluded.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#allmimic">allmimic</a></strong>&nbsp;<a href="https://github.com/Shimingyi/allmimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Shimingyi/allmimic.svg?style=social"></a><br>By Shimingyi</td>
<td valign="top"><strong>Mixed residual/absolute actions and balanced sampling:</strong> one RTX 4090, 0.83 h, LAFAN1 return 0.91 and 0/40 failures; evaluation time excluded.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#scalebfm_plus--supermimic">ScaleBFM_Plus</a></strong>&nbsp;<a href="https://github.com/Hxxxz0/ScaleBFM_Plus/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Hxxxz0/ScaleBFM_Plus.svg?style=social"></a><br>By Hxxxz0</td>
<td valign="top"><strong>Humanoid transformer with held-out evaluation:</strong> 99.5% tracking success on 2,575 held-out motions after 8.3 h on 16× RTX 5090.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic-mjlab">SuperMimic Mjlab</a></strong>&nbsp;<a href="https://github.com/Breezewrf/supermimic_mjlab/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Breezewrf/supermimic_mjlab.svg?style=social"></a><br>By Breezewrf</td>
<td valign="top"><strong>Traceable performance ablations:</strong> LAFAN return rises from 0.6016 to 0.8526; 15k iterations take ≈4 h on one A6000; policy and world-model checkpoints released.</td>
</tr>
<tr>
<td rowspan="2" valign="top"><a href="#perception-terrain-and-quadrupeds">👁️&nbsp;Perception&nbsp;&amp;&nbsp;terrain&nbsp;(4)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#instinctmj--supermimic">InstinctMJ</a></strong>&nbsp;<a href="https://github.com/project-instinct/InstinctMJ/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/project-instinct/InstinctMJ.svg?style=social"></a><br>By Project Instinct</td>
<td valign="top"><strong>Depth-aware G1 terrain tracking:</strong> Render route reports 94.9% success over 10 motions after ≈2.7 h on one RTX 3090; one training seed.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#go2-supermimic">Go2-SuperMimic</a></strong>&nbsp;<a href="https://github.com/Zhengtianjin/go2-supermimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Zhengtianjin/go2-supermimic.svg?style=social"></a><br>By Zhengtianjin</td>
<td valign="top"><strong>Quadruped chase-and-dodge with perception:</strong> three released actors cover flat ground, obstacles and terrain, with evaluation/recording tools; simulation only.</td>
</tr>
<tr>
<td rowspan="3" valign="top"><a href="#manipulation-and-dexterous-hands">🦾&nbsp;Manipulation&nbsp;&amp;&nbsp;hands&nbsp;(4)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#dex-supermimic">Dex SuperMimic</a></strong>&nbsp;<a href="https://github.com/CumulusAlpha/Dex-Supermimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/CumulusAlpha/Dex-Supermimic.svg?style=social"></a><br>By CumulusAlpha</td>
<td valign="top"><strong>Wuji-hand cube reorientation and pen spinning:</strong> three 8k-iteration checkpoints, bundled assets and Viser playback make the hand tasks directly inspectable.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic-for-robot-manipulation">supermimic_manipulation</a></strong>&nbsp;<a href="https://github.com/emoPointer/supermimic_manipulation/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/emoPointer/supermimic_manipulation.svg?style=social"></a><br>By Zhiqiang Zhou (emoPointer)</td>
<td valign="top"><strong>Three ARX5 manipulation tasks:</strong> 100% / 94.9% / 96.9% success on held-out resets (256 episodes/task); 1.8–2.8 h per run sharing one A100 80 GB; weights released.</td>
</tr>
<tr>
<td valign="top" nowrap="nowrap"><strong><a href="#in-hand-rotation-mjlab">In-Hand Rotation mjlab</a></strong>&nbsp;<a href="https://github.com/Msornerrrr/in-hand-rotation-mjlab/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/Msornerrrr/in-hand-rotation-mjlab.svg?style=social"></a><br>By Msornerrrr</td>
<td valign="top"><strong>World-model vs PPO on LEAP cube rotation:</strong> matches PPO’s 6.5-hour reward level in 25 min on one RTX 4090; simulation, one run per configuration.</td>
</tr>
<tr>
<td rowspan="1" valign="top"><a href="#muscle-interaction-and-diagnostics">💪&nbsp;Muscles&nbsp;&amp;&nbsp;interaction&nbsp;(3)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#muscle-supermimic">muscle-supermimic</a></strong>&nbsp;<a href="https://github.com/kaibohex/muscle-supermimic/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/kaibohex/muscle-supermimic.svg?style=social"></a><br>By Kaibo He (kaibohex)</td>
<td valign="top"><strong>700-muscle whole-body control:</strong> MS-Human-700 tracks 104/108 held-out KIT clips after 10.1 h on one RTX 5090; also supports 354-muscle MyoFullBody.</td>
</tr>
<tr>
<td rowspan="1" valign="top"><a href="#robot-porting-and-retargeting">🤖&nbsp;Robot&nbsp;ports&nbsp;(6)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic-retargeted">SuperMimic Retargeted</a></strong>&nbsp;<a href="https://github.com/tianshuwu/supermimic-retargeted/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/tianshuwu/supermimic-retargeted.svg?style=social"></a><br>By tianshuwu</td>
<td valign="top"><strong>Motion preparation for three robot bodies:</strong> SOMA retargeting, coordinate correction and foot-contact checks for G1, A3 and X2 Ultra; training weights not released.</td>
</tr>
<tr>
<td rowspan="1" valign="top"><a href="#real-robot-deployment-and-sim2real">🚀&nbsp;Real&nbsp;robots&nbsp;(2)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#supermimic-repro-sim2real">SuperMimic-Repro-Sim2Real</a></strong>&nbsp;<a href="https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real.svg?style=social"></a><br>By NJU R&amp;L Group Embodied Lab</td>
<td valign="top"><strong>Clip-specific fine-tuning through real-G1 deployment:</strong> a ≈22 s dance with rapid turns and a one-foot landing completed twice; slack safety tether used.</td>
</tr>
<tr>
<td rowspan="1" valign="top"><a href="#inspired-experiments">💡&nbsp;Learning&nbsp;examples&nbsp;(2)</a></td>
<td valign="top" nowrap="nowrap"><strong><a href="#flatworld--supermimic-2d">FlatWorld</a></strong>&nbsp;<a href="https://github.com/swaggyliu/FlatWorld/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/swaggyliu/FlatWorld.svg?style=social"></a><br>By swaggyliu</td>
<td valign="top"><strong>A readable 2D learning loop:</strong> eight-joint humanoid, procedural references, training and per-skill rendering; a 33.3 s multi-skill demo, not a G1 benchmark.</td>
</tr>
</tbody>
</table>

## Reproductions, methods and training frameworks

<a name="independent-reproductions"></a>

<a name="method-and-morphology-variants"></a>

<a name="frameworks-and-training-stacks"></a>

Original-method reproductions, training acceleration, algorithm variants, shared policies across bodies and framework integrations. Projects may span several directions; their strengths and training setups describe the differences.

<a name="supermimic_vibed"></a>

<a name="-supermimic_vibed"></a>

### ⭐ supermimic_vibed [![GitHub stars](https://img.shields.io/github/stars/zita-ch/supermimic_vibed.svg?style=social)](https://github.com/zita-ch/supermimic_vibed/stargazers)

[Repository](https://github.com/zita-ch/supermimic_vibed) · [Setup and usage](https://github.com/zita-ch/supermimic_vibed/blob/8bfc1158bd968f729fcc65d5e897a05b05ea3d36/README.md#setup) · [Results](https://github.com/zita-ch/supermimic_vibed/blob/8bfc1158bd968f729fcc65d5e897a05b05ea3d36/README.md#result-lafan1-40-clips-one-rtx-pro-6000-blackwell)

- **By Chong Zhang.** An independent G1 implementation on Isaac Lab 3, with a kit-less setup, training, full-clip evaluation and rendering tools.
- **Upstream report:** On 40 LAFAN1 clips, normalized return **0.829** and **0 / 40 failures** after **1.47 hours on one RTX PRO 6000 Blackwell**.
- **Useful context:** The author describes it as a rapid, unreviewed reproduction. Documented deviations include disabled self-collisions, bf16 MLP computation and an extra reference-root orientation input. [Source snapshot](https://github.com/zita-ch/supermimic_vibed/blob/8bfc1158bd968f729fcc65d5e897a05b05ea3d36/README.md).

<a href="https://github.com/zita-ch/supermimic_vibed"><img src="https://raw.githubusercontent.com/zita-ch/supermimic_vibed/a1508d42c9d1699a52e8233ab16d08c488441ab9/results/supermimic_lafan1_highlight.gif" width="480" alt="Simulation · LAFAN1 highlights"></a><br><sub>Simulation · LAFAN1 highlights</sub>

<br>

<a name="supermimic-reproduced"></a>

<a name="-supermimic-reproduced"></a>

### ⭐ SuperMimic-Reproduced [![GitHub stars](https://img.shields.io/github/stars/CuboiLeo/SuperMimic-Reproduced.svg?style=social)](https://github.com/CuboiLeo/SuperMimic-Reproduced/stargazers)

[Repository](https://github.com/CuboiLeo/SuperMimic-Reproduced) · [Setup](https://github.com/CuboiLeo/SuperMimic-Reproduced/blob/ba6105349069bf040f1fdad60873d13138d505a2/README.md#setup) · [Experiment log](https://github.com/CuboiLeo/SuperMimic-Reproduced/blob/ba6105349069bf040f1fdad60873d13138d505a2/docs/EXPERIMENTS.md) · [Checkpoint](https://github.com/CuboiLeo/SuperMimic-Reproduced/releases/tag/e8-boneseed-100k)

- **By CuboiLeo.** A from-scratch mjlab implementation for G1, with Chinese reproduction notes, LAFAN1/BONES-SEED processing, multi-GPU training, an interactive replay viewer and a released full-data checkpoint.
- **Upstream report:** With paper observations, four RTX 5090s train on **129,943 BONES-SEED clips** for **7.1 hours (about 28 GPU·h)**. The experiment log reports **0.930 return, 495 / 129,943 failures** on that library; after excluding 452 clips by name, it reports **0.932 return, 145 / 129,491 failures (0.11%)** on the filtered evaluation set. On LAFAN1, anchor-relative observations reach **0.904, 3 / 40 failures**, while paper observations reach **0.56–0.59, 3–9 / 40** across three runs.
- **Useful context:** BONES-SEED clips are short (median 5.8 seconds), whereas paper-observation policies drift on 100–300-second LAFAN1 clips. The two observation settings are not directly comparable. The upstream README pairs 0.930 with the filtered failure count; the set-specific figures above follow the [experiment log](https://github.com/CuboiLeo/SuperMimic-Reproduced/blob/ba6105349069bf040f1fdad60873d13138d505a2/docs/EXPERIMENTS.md). [Source snapshot](https://github.com/CuboiLeo/SuperMimic-Reproduced/blob/ba6105349069bf040f1fdad60873d13138d505a2/README.md).

<a href="https://github.com/CuboiLeo/SuperMimic-Reproduced/releases/tag/e8-boneseed-100k"><img src="https://raw.githubusercontent.com/CuboiLeo/SuperMimic-Reproduced/ba6105349069bf040f1fdad60873d13138d505a2/media/g1_boneseed_highlights.gif" width="480" alt="Simulation · one full BONES-SEED policy across jumps, spins, hops and get-ups"></a><br><sub>Simulation · one full-BONES-SEED policy across six challenging motion clips</sub>

<br>

<a name="unisupermimic"></a>

<a name="-unisupermimic"></a>

### ⭐ UniSuperMimic [![GitHub stars](https://img.shields.io/github/stars/Motphys/Uni-SuperMimic.svg?style=social)](https://github.com/Motphys/Uni-SuperMimic/stargazers)

[Repository](https://github.com/Motphys/Uni-SuperMimic) · [Installation](https://github.com/Motphys/Uni-SuperMimic/blob/05a9772ca09509c50a4cc3fe96f9d6b3c180f3d2/README.md#installation) · [Results](https://github.com/Motphys/Uni-SuperMimic/blob/05a9772ca09509c50a4cc3fe96f9d6b3c180f3d2/README.md#results)

- **By Motphys.** Implements G1 tracking in UniLab with LAFAN1/BONES-SEED download, filtering, packing, training and full-clip evaluation, plus mjwarp, MuJoCo and Motrix entrypoints. The updated evaluator recycles finished environments to reduce long-clip batch tails.
- **Upstream report:** On **129,487 BONES-SEED clips**, one **RTX 4090 (48 GB as reported upstream)** trains the **12k baseline in 1.69 h**, with full-library return **0.9243 and 350 / 129,487 failures**. Adding EMA, no-sync training and a learning-rate change on the same GPU reaches **0.9395 and 193 / 129,487 failures at 8k iterations**. The older RTX 5090 / 10,000-clip sample is a separate run.
- **Useful context:** The explicitly paired 1.69 h belongs to the 12k baseline. The README also advertises a strong checkpoint in about 40 minutes, but does not give a precise elapsed time for the optimized 8k row. These are the reported mjwarp experiments, not equivalent validation across backends. BONES-SEED evaluation covers training motions, not held-out generalization. [Source snapshot](https://github.com/Motphys/Uni-SuperMimic/blob/05a9772ca09509c50a4cc3fe96f9d6b3c180f3d2/README.md).

<a href="https://github.com/Motphys/Uni-SuperMimic/blob/9bdcbde1f191d88b489309182624a9877e7b6c30/docs/assets/supermimic_comparison.mp4"><img src="https://raw.githubusercontent.com/Motphys/Uni-SuperMimic/9bdcbde1f191d88b489309182624a9877e7b6c30/docs/assets/supermimic_comparison.gif" width="480" alt="Simulation · G1 jump tracking"></a><br><sub>Simulation · G1 jump tracking</sub>

<br>

<a name="morphmimic"></a>

<a name="-morphmimic"></a>

### ⭐ MorphMimic [![GitHub stars](https://img.shields.io/github/stars/lzyang2000/morphmimic.svg?style=social)](https://github.com/lzyang2000/morphmimic/stargazers)

[Repository](https://github.com/lzyang2000/morphmimic) · [Setup](https://github.com/lzyang2000/morphmimic/blob/770394b4a0cad9effbf807a6c03435d1699733d0/README.md#setup) · [Method differences](https://github.com/lzyang2000/morphmimic/blob/770394b4a0cad9effbf807a6c03435d1699733d0/README.md#differences-from-supermimic)

- **By Lizhi Yang et al.** Shares a world model, policy, or both across G1, X2 Ultra and T2 in mjlab / MuJoCo Warp. v0.1 adds a 24-joint / five-point human interface that consumes PICO body tracking directly, without first retargeting it to robot motion.
- **Upstream report:** Releases a unified **60,000-iteration ONNX policy** for `g1_amber`, X2 Ultra and T2 with motion and human interfaces. The authors tested it on their **real G1** and provide onboard teleoperation. X2 Ultra and T2 have only run in simulation; aggregate success rates and training duration are not reported.
- **Useful context:** The released `g1_amber` configuration adapts to the authors’ weak G1 waist motors; it is not validation on every G1. Later checkpoints from 78k onward swayed while standing on hardware despite apparently normal training metrics. Default interfaces do not need robot world pose; optional robot-anchor mode still needs pose estimation. [Source snapshot](https://github.com/lzyang2000/morphmimic/blob/770394b4a0cad9effbf807a6c03435d1699733d0/README.md).

<a href="https://lzyang2000.github.io/morphmimic/static/videos/dance_hiphop_shuffle_sequence_v_001_R_003__A306.mp4"><img src="assets/community/morphmimic.gif" width="480" alt="Simulation · one shared policy for G1 / X2 Ultra / T2"></a><br><sub>Simulation · one shared policy for G1 / X2 Ultra / T2</sub>

[Video](https://lzyang2000.github.io/morphmimic/static/videos/morphmimic.mp4) · [Interactive demo](https://lzyang2000.github.io/morphmimic/demo/)

<br>

<a name="instanttrack"></a>

<a name="-instanttrack"></a>

### ⭐ InstantTrack [![GitHub stars](https://img.shields.io/github/stars/Huy-Quang-Dao/instantTrack.svg?style=social)](https://github.com/Huy-Quang-Dao/instantTrack/stargazers)

[Repository](https://github.com/Huy-Quang-Dao/instantTrack) · [Setup](https://github.com/Huy-Quang-Dao/instantTrack/blob/a33691a08bca8802d9d2985f62e2567479735a8e/README.md#setup) · [Results and ablations](https://github.com/Huy-Quang-Dao/instantTrack/blob/a33691a08bca8802d9d2985f62e2567479735a8e/results/report.md) · [Training presets](https://github.com/Huy-Quang-Dao/instantTrack/blob/a33691a08bca8802d9d2985f62e2567479735a8e/scripts/presets.sh)

- **By Huy-Quang-Dao.** Builds on the mjlab port of supermimic_vibed for G1, combining GPU training-loop optimizations, EMA policy weights, a smaller world model and failure-focused resets; the main preset also adds a contact reward during imagined rollouts.
- **Upstream report:** On one RTX 5090, all three seeds reach **return ≥ 0.82 and 0 / 40 failed LAFAN1 clips in about 15 minutes**, with mean return **0.831** at that point. The reported **2.2×** speed-up is against the author's SuperMimic + EMA baseline on the same machine; the **6×** figure uses their plain reimplementation.
- **Useful context:** Time marks the first of three consecutive qualifying checkpoints, excludes offline evaluation and is not an end-to-end setup time. Evaluation covers the training clips in simulation; no larger motion library or real-robot results are reported. Model size, update count and training reward differ from the baseline; this is not a cross-project speed ranking. [Source snapshot](https://github.com/Huy-Quang-Dao/instantTrack/blob/a33691a08bca8802d9d2985f62e2567479735a8e/README.md).

<a href="https://github.com/Huy-Quang-Dao/instantTrack/blob/a33691a08bca8802d9d2985f62e2567479735a8e/media/equal_time_15min.gif"><img src="https://raw.githubusercontent.com/Huy-Quang-Dao/instantTrack/a33691a08bca8802d9d2985f62e2567479735a8e/media/equal_time_15min.gif" width="480" alt="Simulation · SuperMimic + EMA versus InstantTrack after 15 minutes of training"></a><br><sub>Upstream simulation · same 15-minute training budget; SuperMimic + EMA (left), InstantTrack (right), fall-and-get-up motion</sub>

<br>

<a name="allmimic"></a>

### ⭐ allmimic [![GitHub stars](https://img.shields.io/github/stars/Shimingyi/allmimic.svg?style=social)](https://github.com/Shimingyi/allmimic/stargazers)

[Repository](https://github.com/Shimingyi/allmimic) · [Install](https://github.com/Shimingyi/allmimic/blob/cb334ff674b2f57248f33f8c21b7fb526fbdf8cc/README.md#install) · [Results](https://github.com/Shimingyi/allmimic/blob/cb334ff674b2f57248f33f8c21b7fb526fbdf8cc/README.md#results)

- **By Shimingyi.** Builds on supermimic_vibe for G1 in mjlab, mixing residual upper-body actions with absolute leg actions, weighting world-model losses and balancing motion sampling.
- **Upstream report:** With the recommended preset on one RTX 4090, full-length LAFAN1 evaluation reports **0 / 40 failures and return 0.91 after 0.83 hours**; training time excludes evaluation.
- **Useful context:** The recommended preset changes the method and data sampling. The 306-hard-motion-only run and full BONES-SEED training are separate experiments. [Source snapshot](https://github.com/Shimingyi/allmimic/blob/cb334ff674b2f57248f33f8c21b7fb526fbdf8cc/README.md).

<a href="https://github.com/Shimingyi/allmimic"><img src="https://raw.githubusercontent.com/Shimingyi/allmimic/cb334ff674b2f57248f33f8c21b7fb526fbdf8cc/assets/challenge_cases.gif" width="480" alt="Simulation · challenging motion clips"></a><br><sub>Simulation · challenging motion clips</sub>

<br>

<a name="scalebfm_plus--supermimic"></a>

<a name="-scalebfm_plus--supermimic"></a>

### ⭐ ScaleBFM_Plus · SuperMimic [![GitHub stars](https://img.shields.io/github/stars/Hxxxz0/ScaleBFM_Plus.svg?style=social)](https://github.com/Hxxxz0/ScaleBFM_Plus/stargazers)

[Repository](https://github.com/Hxxxz0/ScaleBFM_Plus) · [Training and results](https://github.com/Hxxxz0/ScaleBFM_Plus/blob/65e4d524bd31fdc4284ba8c6e624fb0b0127da03/ScaleTrack/README.md#fast-training-with-a-learned-world-model-supermimic) · [Released checkpoint](https://github.com/Hxxxz0/ScaleBFM_Plus/tree/65e4d524bd31fdc4284ba8c6e624fb0b0127da03/ScaleTrack/checkpoints/supermimic_m)

- **By Hxxxz0, building on ScaleBFM.** Integrates SuperMimic-style world-model learning and 32-step BPTT into ScaleTrack for G1 in IsaacLab / RSL-RL, retaining the humanoid transformer and tracking modes, with PPO-compatible policy export and playback.
- **Upstream report:** Training on **309 h / 138k clips** from BONES-SEED, any4hdmi and LAFAN1 for **8.3 h on 16 RTX 5090s** yields **99.5% tracking success on 2,575 held-out motions**. On 386 dynamic test motions, both this policy and the official ScaleBFM-M checkpoint succeed on **376 / 386**, with mean global body-position errors of **6.35 cm** and **6.43 cm**, respectively.
- **Useful context:** This is a community extension of ScaleBFM. The reported **26× per-step speedup** compares **0.65 s on 16 RTX 5090s** with PPO's **17.0 s on 8 RTX 5090s**; it is not a matched-compute or time-to-quality comparison. [Source snapshot](https://github.com/Hxxxz0/ScaleBFM_Plus/blob/65e4d524bd31fdc4284ba8c6e624fb0b0127da03/ScaleTrack/README.md).

<a href="https://github.com/Hxxxz0/ScaleBFM_Plus/blob/65e4d524bd31fdc4284ba8c6e624fb0b0127da03/ScaleTrack/assets/demos/supermimic_vs_official.gif"><img src="https://media.githubusercontent.com/media/Hxxxz0/ScaleBFM_Plus/65e4d524bd31fdc4284ba8c6e624fb0b0127da03/ScaleTrack/assets/demos/supermimic_vs_official.gif" width="480" alt="Simulation · official ScaleBFM-M (left) and SuperMimic (right), unseen LAFAN dance"></a><br><sub>Simulation · official ScaleBFM-M (left) and SuperMimic (right), unseen LAFAN dance · Source: Hxxxz0 / ScaleBFM_Plus</sub>

<br>

<a name="supermimic-mjlab"></a>

<a name="-supermimic-mjlab"></a>

### ⭐ SuperMimic Mjlab [![GitHub stars](https://img.shields.io/github/stars/Breezewrf/supermimic_mjlab.svg?style=social)](https://github.com/Breezewrf/supermimic_mjlab/stargazers)

[Repository](https://github.com/Breezewrf/supermimic_mjlab) · [Setup](https://github.com/Breezewrf/supermimic_mjlab/blob/a7cee74636a4c596cd8710f8c2e51f82d78bb150/doc/setup_en.md) · [Ablations and checkpoint](https://github.com/Breezewrf/supermimic_mjlab/blob/a7cee74636a4c596cd8710f8c2e51f82d78bb150/README.md#ablation-results-and-released-checkpoint)

- **By Breezewrf.** An independent SuperMimic reproduction for Unitree G1 in mjlab, with a complete performance-improvement ablation study, multi-motion and velocity training, OOD playback, video-to-motion export, full-clip evaluation and released policy/world-model checkpoints.
- **Upstream report:** On all 40 LAFAN motions, the selected checkpoint achieves **40 / 40 successful motions**, **100% mean completion** and **0.8528 normalized return** in fixed-start, full-clip deterministic evaluation. Training for **15,000 iterations takes approximately 4 hours on one RTX A6000 48 GB**, with 4,096 environments and FP32 networks.
- **Useful context:** Documents the full progression from Actor/Critic input normalization through a torso-frame motion orientation anchor, world-model normalization and a corrected cosine learning-rate schedule: mean normalized return **0.6016 → 0.8130 → 0.8504 → 0.8526** at 15,000 iterations over all 40 motions. The final rerun mean is distinct from the selected checkpoint score above. Updated documentation adds the RoboJuDo-Plus SuperMimic deployment route; the authors report **23DoF G1** hardware use, with velocity tracking still in development. [Source snapshot](https://github.com/Breezewrf/supermimic_mjlab/blob/a7cee74636a4c596cd8710f8c2e51f82d78bb150/README.md).

<a href="https://github.com/Breezewrf/supermimic_mjlab/blob/77183062eb92026bfbee2daf276f87cad36fd957/doc/assets/demo_v0.gif"><img src="assets/community/mjlab-demo.gif" width="480" alt="Simulation · 12-second excerpt from the SuperMimic Mjlab motion playback demo"></a><br><sub>Simulation · 12-second excerpt from the 60.8-second playback demo; click for the full upstream GIF</sub>

<br>

<a name="holomotion--supermimic"></a>

### HoloMotion · SuperMimic [![GitHub stars](https://img.shields.io/github/stars/HorizonRobotics/HoloMotion.svg?style=social)](https://github.com/HorizonRobotics/HoloMotion/stargazers)

[Repository](https://github.com/HorizonRobotics/HoloMotion) · [Training guide](https://github.com/HorizonRobotics/HoloMotion/blob/f52dd81ae935a828b0296f5ee0f833beb7378bf0/docs/supermimic.md) · [Results](https://github.com/HorizonRobotics/HoloMotion/blob/f52dd81ae935a828b0296f5ee0f833beb7378bf0/docs/supermimic.md#7-recorded-30-minute-results)

- **By Horizon Robotics.** Integrates SuperMimic into HoloMotion’s G1 assets, HDF5 motion data and Hydra workflow, sharing tasks and evaluation with PPO on MuJoCo Warp and Isaac PhysX.
- **Upstream report:** The selected MuJoCo Warp recipe completes **32 / 40 LAFAN1 training clips after 30 minutes on one RTX 5090**.
- **Useful context:** The validated route uses a compact policy. The preview shows short excerpts from a separate run; it does not replace complete-clip evaluation or establish the planned large-policy integration. [Source snapshot](https://github.com/HorizonRobotics/HoloMotion/blob/f52dd81ae935a828b0296f5ee0f833beb7378bf0/docs/supermimic.md).

<a href="https://github.com/HorizonRobotics/HoloMotion"><img src="https://raw.githubusercontent.com/HorizonRobotics/HoloMotion/adaacd50ada6ba9338f6c3f539093f85453e2554/docs/media/supermimic_training_progress.webp" width="480" alt="Simulation · PPO / SuperMimic, two backends"></a><br><sub>Simulation · PPO / SuperMimic, two backends</sub>

<br>

<a name="rethinking-supermimic"></a>

### Rethinking SuperMimic [![GitHub stars](https://img.shields.io/github/stars/btx0424/rethinking-supermimic.svg?style=social)](https://github.com/btx0424/rethinking-supermimic/stargazers)

[Repository](https://github.com/btx0424/rethinking-supermimic) · [Installation](https://github.com/btx0424/rethinking-supermimic/blob/2cbbd1278bfb8bd59c31fe48d7413c46ae205e32/README.md#installation) · [Implementation comparison](https://github.com/btx0424/rethinking-supermimic/blob/2cbbd1278bfb8bd59c31fe48d7413c46ae205e32/README.md#ours-the-paper-and-supermimic_vibed)

- **By btx0424.** Studies goal conditioning for G1 in mjlab: concatenating the goal with proprioception versus using FiLM to modulate the policy layers. The latest revision adds an HL-Gauss critic, gradient checks and selectable heading- or pelvis-frame world-model coordinates.
- **Useful context:** Provides configurable observations, anchor choices and Viser playback. Its implementation table explains differences from the paper and supermimic_vibed, including self-collisions and observation inputs. [Source snapshot](https://github.com/btx0424/rethinking-supermimic/blob/2cbbd1278bfb8bd59c31fe48d7413c46ae205e32/README.md).

<a href="https://github.com/btx0424/rethinking-supermimic/blob/ecdaeb6a916a16cf7eb69b19226c17be31a6bc27/README.md"><img src="assets/community/rethinking-comparison.png" width="720" alt="Historical implementation table excerpt · 2026-10-26 snapshot; current comparison linked above"></a><br><sub>Historical implementation table excerpt · 2026-10-26 snapshot; current comparison linked above</sub>

<br>

<a name="standing-mbrl-vs-ppo"></a>

### Standing MBRL vs PPO [![GitHub stars](https://img.shields.io/github/stars/JackMin7/supermimic_whole_body_tracking.svg?style=social)](https://github.com/JackMin7/supermimic_whole_body_tracking/stargazers)

[Repository](https://github.com/JackMin7/supermimic_whole_body_tracking) · [Experiment details](https://github.com/JackMin7/supermimic_whole_body_tracking/blob/553a7d32dc5fc00cbe6de5ee46479af2fcceeda8/docs/EXPERIMENTS.md) · [Reproduction notes](https://github.com/JackMin7/supermimic_whole_body_tracking/blob/553a7d32dc5fc00cbe6de5ee46479af2fcceeda8/docs/REPRODUCIBILITY.md)

- **By JackMin7.** Adapts SuperMimic's differentiable world-model loop to a static G1 standing task and compares it with an RSL-RL PPO baseline derived from BeyondMimic.
- **Upstream report:** With the same 29-DoF G1, task, reward and about one hour of training on 256 environments, MBRL succeeds **32 / 32** times in both the **20-second and 60-second** tests; PPO succeeds **12 / 32** and **16 / 32**. Mean 20-second joint RMSE is **0.144 versus 0.415 rad**.
- **Useful context:** Single training seed, shared GPU, no disturbances, and the 32 rollouts are copies rather than independent seeds. The project does not claim training-speed or real-robot gains. [Source snapshot](https://github.com/JackMin7/supermimic_whole_body_tracking/blob/553a7d32dc5fc00cbe6de5ee46479af2fcceeda8/README.md).

<a href="https://github.com/JackMin7/supermimic_whole_body_tracking/blob/553a7d32dc5fc00cbe6de5ee46479af2fcceeda8/media/ppo_vs_mbrl_60s.mp4"><img src="https://raw.githubusercontent.com/JackMin7/supermimic_whole_body_tracking/553a7d32dc5fc00cbe6de5ee46479af2fcceeda8/media/PPO%E4%B8%8EMBRL%E7%AB%99%E7%AB%8B%E5%AF%B9%E7%85%A7_60%E7%A7%92%E5%8A%A8%E5%9B%BE.gif" width="640" alt="Simulation · PPO and MBRL G1 standing comparison over 60 seconds"></a><br><sub>Simulation · 60-second PPO / MBRL comparison at normal speed; PPO freezes after termination</sub>

<br>

<a name="trackerlab-supermimic"></a>

### TrackerLab SuperMimic [![GitHub stars](https://img.shields.io/github/stars/Renforce-Dynamics/trackerlab-supermimic.svg?style=social)](https://github.com/Renforce-Dynamics/trackerlab-supermimic/stargazers)

[Repository](https://github.com/Renforce-Dynamics/trackerlab-supermimic) · [Install](https://github.com/Renforce-Dynamics/trackerlab-supermimic/blob/813f37a89d9be0791c9c72695a322307001a5d11/README.md#install) · [Results and limits](https://github.com/Renforce-Dynamics/trackerlab-supermimic/blob/813f37a89d9be0791c9c72695a322307001a5d11/docs/results.md)

- **By Renforce Dynamics.** Provides a shared Isaac Lab / PhysX workflow for retargeting, training, full-clip evaluation and export across G1, Go2, A3, T1, Bumi and Pi+, plus Go2 task policies.
- **Upstream report:** Re-evaluation of the 32,000-iteration G1 parent checkpoint reports normalized return **0.8694663** and **0 / 40 LAFAN1 failures**.
- **Useful context:** Results use PhysX, while supermimic_vibed uses MuJoCo Warp. Robot-specific motion libraries and training histories differ; held-out motion generalization remains unmeasured. A separate G1 MuJoCo-Warp entrypoint and motion-tail/normalizer fixes are now available. The Warp integration has CPU regression coverage but still needs target-GPU qualification; it does not inherit the historical PhysX score above. [Source snapshot](https://github.com/Renforce-Dynamics/trackerlab-supermimic/blob/813f37a89d9be0791c9c72695a322307001a5d11/README.md).

<a href="https://github.com/Renforce-Dynamics/trackerlab-supermimic/blob/29d24524f2f731bf4df75b319c3e76544165849e/docs/media/g1_dance_032000.mp4"><img src="https://raw.githubusercontent.com/Renforce-Dynamics/trackerlab-supermimic/29d24524f2f731bf4df75b319c3e76544165849e/docs/media/g1_dance_032000.gif" width="480" alt="Simulation · G1 policy / reference dance"></a><br><sub>Simulation · G1 policy / reference dance</sub>

<br>

<a name="supermimic_vibe"></a>

### supermimic_vibe [![GitHub stars](https://img.shields.io/github/stars/dhmbb2/supermimic_vibe.svg?style=social)](https://github.com/dhmbb2/supermimic_vibe/stargazers)

[Repository](https://github.com/dhmbb2/supermimic_vibe) · [Setup](https://github.com/dhmbb2/supermimic_vibe/blob/d0934d069207ee745be8489d9631a8314c94c1f3/README.md#setup) · [Results log](https://github.com/dhmbb2/supermimic_vibe/blob/d0934d069207ee745be8489d9631a8314c94c1f3/notes/RESULTS.md)

- **By dhmbb2.** An independent G1 reproduction in mjlab / MuJoCo Warp, with claim-by-claim PPO-Sim/PPO-WM, critic, horizon, push-recovery, velocity-control, BONES-SEED scaling and SONIC comparisons.
- **Upstream report:** One RTX A6000 reaches LAFAN1 return **0.833 at 1.34 h**; its best checkpoint scores **0.947 with 0 / 40 failures at 11.4 h**. On **128,904 BONES-SEED clips**, a modified configuration collecting without exploration noise in half the environments reaches **0.923 and 45 / 128,904 failures at 14.4 h**. Times exclude evaluation.
- **Useful context:** The noise-free collection fraction is an addition to the paper. The paper-faithful BONES-SEED run collapses after roughly six hours, and the two-GPU zero-failure result was not reproduced; these negative results are documented alongside ablations. A6000 and paper H100 timings are not equivalent; hardware transfer is out of scope. [Source snapshot](https://github.com/dhmbb2/supermimic_vibe/blob/d0934d069207ee745be8489d9631a8314c94c1f3/README.md).

<a href="https://github.com/dhmbb2/supermimic_vibe/blob/072f0910dadc9d95c720e625b546120e9ce917c9/README.md"><img src="assets/community/vibe-results.png" width="720" alt="Historical report screenshot · earlier A6000 experiments; updated results above"></a><br><sub>Historical report screenshot · earlier A6000 experiments; updated results above</sub>

<br>

<a name="supermimic-on-locomujoco"></a>

### SuperMimic on LocoMuJoCo [![GitHub stars](https://img.shields.io/github/stars/Alchedata/supermimic-locomujoco.svg?style=social)](https://github.com/Alchedata/supermimic-locomujoco/stargazers)

[Repository](https://github.com/Alchedata/supermimic-locomujoco) · [Setup](https://github.com/Alchedata/supermimic-locomujoco/blob/de9f39191b9e8b87ff1afd2b0129dd93d4795e8c/README.md#setup) · [Results](https://github.com/Alchedata/supermimic-locomujoco/blob/de9f39191b9e8b87ff1afd2b0129dd93d4795e8c/README.md#results)

- **By Alchedata.** Ports the method to H1 with JAX and LocoMuJoCo, adding a **full-state ODE world model** and **anti-saturation regularization** alongside the MLP, residual-expert, action-sensitivity and trust-aware variants.
- **Upstream report:** With fixed 5,000-iteration checkpoints and 160 initial states, adding anti-saturation to the Euler ODE model reduces aggregate failures from **15 / 480 to 1 / 480** over three seeds. Seed 43 improves from **878.71 / 15 failures to 935.38 / 0 failures**, while seed 42 becomes slightly worse, so this is not a uniform score increase.
- **Useful context:** The reward is LocoMuJoCo episode return, not the G1 normalized tracking score. Midpoint ODE acceleration runs are still in progress and are not included as completed results. [Source snapshot](https://github.com/Alchedata/supermimic-locomujoco/blob/de9f39191b9e8b87ff1afd2b0129dd93d4795e8c/README.md).

<a href="https://github.com/Alchedata/supermimic-locomujoco/blob/de9f39191b9e8b87ff1afd2b0129dd93d4795e8c/docs/figures/return_vs_step.png"><img src="assets/community/locomujoco-results.png" width="720" alt="Training curves · return versus training step for ODE and anti-saturation variants"></a><br><sub>Upstream training curves · ODE and anti-saturation variants at fixed 5k evaluation checkpoints</sub>

<br>

<a name="supermimickit"></a>

### SuperMimicKit [![GitHub stars](https://img.shields.io/github/stars/OMEGA-i/SuperMimicKit.svg?style=social)](https://github.com/OMEGA-i/SuperMimicKit/stargazers)

[Repository](https://github.com/OMEGA-i/SuperMimicKit) · [Preview release](https://github.com/OMEGA-i/SuperMimicKit/releases/tag/demo-preview-20261024) · [Evaluation and limits](https://github.com/OMEGA-i/SuperMimicKit/blob/6697ff8ca53adc9233ded12a7c8777610ca1154d/docs/preview-release.md)

- **By OMEGA-i.** An independent MuJoCo Warp implementation for G1, H2 and A3, with motion retargeting, policy/world-model ONNX export and WebGPU browser previews.
- **Upstream report:** Publishes separate train40 and held-out val37 evaluations for G1/H2. The G1 55.5k preview reports **0.7990, 3 / 40 failures** on train40 and **0.3103, 31 / 37 failures** on val37; A3 100k full-clip evaluation is pending.
- **Useful context:** An experimental preview with limited held-out tracking and documented later-checkpoint regressions. Supply licensed motion data; no top-level code license was found at the reviewed revision. [Source snapshot](https://github.com/OMEGA-i/SuperMimicKit/blob/6697ff8ca53adc9233ded12a7c8777610ca1154d/README.md).

<a href="https://github.com/OMEGA-i/SuperMimicKit/blob/6697ff8ca53adc9233ded12a7c8777610ca1154d/docs/media/teaser.mp4"><img src="https://raw.githubusercontent.com/OMEGA-i/SuperMimicKit/6697ff8ca53adc9233ded12a7c8777610ca1154d/docs/media/teaser.gif" width="480" alt="Browser preview · G1 / H2 / A3"></a><br><sub>Browser preview · G1 / H2 / A3</sub>

<br>

<a name="supermimic-lab"></a>

### SuperMimic Lab [![GitHub stars](https://img.shields.io/github/stars/chu-fa/isaaclab-supermimic.svg?style=social)](https://github.com/chu-fa/isaaclab-supermimic/stargazers)

[Repository](https://github.com/chu-fa/isaaclab-supermimic) · [Setup](https://github.com/chu-fa/isaaclab-supermimic/blob/d350e4378c6dc08a3f2a1d35d47b45d83db0e081/docs/SETUP.md) · [Custom-task guide](https://github.com/chu-fa/isaaclab-supermimic/blob/d350e4378c6dc08a3f2a1d35d47b45d83db0e081/docs/CUSTOM_TASKS.md)

- **By chu-fa.** Packages a reusable SuperMimic learner and runner for Isaac Lab custom tasks, with a separately installable AGIBOT A3 example.
- **What it provides:** Provides task contracts, setup instructions and backend validation records. A custom task must supply differentiable state, observation, reward and termination functions.
- **Useful context:** Targets the Isaac Lab 3 development API. The A3 preview uses separately initialized segments; convergence, backend equivalence and hardware deployment are not established. [Source snapshot](https://github.com/chu-fa/isaaclab-supermimic/blob/d350e4378c6dc08a3f2a1d35d47b45d83db0e081/README.md).

<a href="https://github.com/chu-fa/isaaclab-supermimic"><img src="https://raw.githubusercontent.com/chu-fa/isaaclab-supermimic/d350e4378c6dc08a3f2a1d35d47b45d83db0e081/docs/media/a3_reference_vs_policy.webp" width="480" alt="A3 reference / policy · separately initialized segments"></a><br><sub>A3 reference / policy · separately initialized segments</sub>

<br>

<a name="supermimic-on-rtx-5080"></a>

### SuperMimic on RTX 5080 [![GitHub stars](https://img.shields.io/github/stars/rzc156/supermimic-rtx5080.svg?style=social)](https://github.com/rzc156/supermimic-rtx5080/stargazers)

[Repository](https://github.com/rzc156/supermimic-rtx5080) · [Reproduction analysis](https://github.com/rzc156/supermimic-rtx5080/blob/df967c61c29a2ed9ba6b188e1607ba59225fe8a7/REPRODUCTION_ANALYSIS.md) · [Evaluation videos](https://github.com/rzc156/supermimic-rtx5080/blob/df967c61c29a2ed9ba6b188e1607ba59225fe8a7/results/lafan1_anchor/videos/index.html)

- **By rzc156.** An independent mjlab reproduction derived from CuboiLeo, configured for one **16 GB RTX 5080** with 2,048 training environments and additional anchor-relative observations.
- **Upstream report:** The **40k** checkpoint reaches **0.8515 mean / 0.8608 step-weighted return** with **2 / 40 failures** after **2.7 hours**. The 48k checkpoint averages **0.8375**, **4–6 / 40 failures**, after **3.3 hours** over three evaluations.
- **Useful context:** This is a single training seed, and the extra anchor observations make it non-equivalent to the paper-observation protocol. The author highlights 40k as the preferred checkpoint but notes that 40k/44k/48k differences still require multiple seeds. [Source snapshot](https://github.com/rzc156/supermimic-rtx5080/blob/df967c61c29a2ed9ba6b188e1607ba59225fe8a7/README.md).

<a href="https://github.com/rzc156/supermimic-rtx5080/blob/df967c61c29a2ed9ba6b188e1607ba59225fe8a7/results/lafan1_anchor/videos/index.html"><img src="https://raw.githubusercontent.com/rzc156/supermimic-rtx5080/df967c61c29a2ed9ba6b188e1607ba59225fe8a7/results/lafan1_anchor/gifs/walk1.gif" width="480" alt="Simulation · G1 walking with the RTX 5080 reproduction policy"></a><br><sub>Simulation · 40k checkpoint on a 15-second LAFAN1 walk clip; click for all seven videos</sub>

<br>

## Perception, terrain and quadrupeds

Vision, height-scan, terrain and quadruped task adaptations.

<a name="instinctmj--supermimic"></a>

<a name="-instinctmj--supermimic"></a>

### ⭐ InstinctMJ · SuperMimic [![GitHub stars](https://img.shields.io/github/stars/project-instinct/InstinctMJ.svg?style=social)](https://github.com/project-instinct/InstinctMJ/stargazers)

[Repository](https://github.com/project-instinct/InstinctMJ/tree/supermimic) · [Method and results](https://github.com/project-instinct/InstinctMJ/blob/03563ee02665f327425106372264070315673748/src/instinct_mj/rl/supermimic/README.md#results) · [Releases](https://github.com/project-instinct/InstinctMJ/releases)

- **By Project Instinct.** Implements perceptive G1 terrain tracking in mjlab / instinct_rl with two routes: **Render** ray-casts depth from predicted robot state; **Latent** predicts the depth encoder's features. Both feed stop-gradient encoder features to the actor; the encoder learns from reconstruction, with an annealed value head in Render.
- **Upstream report:** One RTX 3090, 1,024 training environments and **8,000 iterations**, on 10 motions: **Render 94.9% success, Latent 96.9%**. Render takes about **2.7 h**, evaluated with 3 seeds × 256 environments; the report has **one training seed**, and Latent uses 128 evaluation environments from the original pre-merge run.
- **Useful context:** Use the **supermimic branch**. Render without the value head reaches **91.0%**; the removed policy-gradient-only encoder variant degraded below a random encoder. The two results have different evaluation setups. Rendering uses known scene meshes, not unknown real environments. Licensed CC BY-NC 4.0. [Source snapshot](https://github.com/project-instinct/InstinctMJ/blob/03563ee02665f327425106372264070315673748/src/instinct_mj/rl/supermimic/README.md).

<a href="https://github.com/project-instinct/InstinctMJ/blob/03563ee02665f327425106372264070315673748/src/instinct_mj/rl/supermimic/assets/two_methods.png"><img src="https://raw.githubusercontent.com/project-instinct/InstinctMJ/03563ee02665f327425106372264070315673748/src/instinct_mj/rl/supermimic/assets/two_methods.png" width="720" alt="Method comparison · Render and Latent vision routes"></a><br><sub>Method comparison · Render and Latent vision routes</sub>

<br>

<a name="go2-supermimic"></a>

<a name="-go2-supermimic"></a>

### ⭐ Go2-SuperMimic [![GitHub stars](https://img.shields.io/github/stars/Zhengtianjin/go2-supermimic.svg?style=social)](https://github.com/Zhengtianjin/go2-supermimic/stargazers)

[Repository](https://github.com/Zhengtianjin/go2-supermimic) · [Quickstart](https://github.com/Zhengtianjin/go2-supermimic/blob/d9eee9b3f248e5300e636c433255db2c1c3e086a/README.md#-quickstart) · [Pretrained policies](https://github.com/Zhengtianjin/go2-supermimic/blob/d9eee9b3f248e5300e636c433255db2c1c3e086a/README.md#pretrained-policies)

- **By Zhengtianjin.** Adapts SuperMimic to Unitree Go2 chase-and-dodge tasks in mjlab, covering flat ground, obstacles and terrain with LiDAR or height-scan inputs.
- **What it provides:** Publishes separate flat, obstacle and terrain actors, plus evaluation and recording tools. Actor-only downloads support playback; resuming training also needs the world model and critic.
- **Useful context:** Simulation only, with ground-truth target perception. The released terrain policy still has falls and bar collisions under the hardest settings. [Source snapshot](https://github.com/Zhengtianjin/go2-supermimic/blob/d9eee9b3f248e5300e636c433255db2c1c3e086a/README.md).

<a href="https://github.com/Zhengtianjin/go2-supermimic"><img src="https://raw.githubusercontent.com/Zhengtianjin/go2-supermimic/054a13c13285a1c94b2e69dc8ac7331f9a8c71cf/resources/terrain.gif" width="480" alt="Simulation · Go2 terrain chase and dodge"></a><br><sub>Simulation · Go2 terrain chase and dodge</sub>

<br>

<a name="supermimic-parkour"></a>

### SuperMimic Parkour [![GitHub stars](https://img.shields.io/github/stars/yhx1203/supermimic_parkour.svg?style=social)](https://github.com/yhx1203/supermimic_parkour/stargazers)

[Repository](https://github.com/yhx1203/supermimic_parkour) · [Data setup](https://github.com/yhx1203/supermimic_parkour/blob/f398519453a25b3f10722626b7356266d8b7f875/README.md#motion-data) · [Checkpoint](https://github.com/yhx1203/supermimic_parkour/blob/f398519453a25b3f10722626b7356266d8b7f875/logs/php_five_skills/last.pt)

- **By yhx1203.** A five-skill G1 parkour adaptation built on mjlab and PHP Parkour motion-matching data, using a shared differentiable world model and BPTT policy learning.
- **Upstream report:** Trains a policy to clear a **130 cm obstacle in just over 4 hours on one GPU**, ships the resulting checkpoint and provides browser-based playback.
- **Useful context:** The PHP motion bundles are not distributed with the repository and must be supplied separately. This is one upstream demonstration and training-time claim, not an independent benchmark against PPO or SuperMimic. [Source snapshot](https://github.com/yhx1203/supermimic_parkour/blob/f398519453a25b3f10722626b7356266d8b7f875/README.md).

<a href="https://github.com/yhx1203/supermimic_parkour/blob/f398519453a25b3f10722626b7356266d8b7f875/doc/%E5%BD%95%E5%B1%8F%202026%E5%B9%B410%E6%9C%8826%E6%97%A5%2016%E6%97%B641%E5%88%8626%E7%A7%92.gif"><img src="https://raw.githubusercontent.com/yhx1203/supermimic_parkour/f398519453a25b3f10722626b7356266d8b7f875/doc/%E5%BD%95%E5%B1%8F%202026%E5%B9%B410%E6%9C%8826%E6%97%A5%2016%E6%97%B641%E5%88%8626%E7%A7%92.gif" width="720" alt="Simulation · G1 clearing a 130 cm parkour obstacle"></a><br><sub>Simulation · five-skill PHP parkour policy; 11.5-second upstream demo</sub>

<br>

<a name="supermimic-perceptive"></a>

### SuperMimic-perceptive [![GitHub stars](https://img.shields.io/github/stars/mode1223345/SuperMimic-perceptive.svg?style=social)](https://github.com/mode1223345/SuperMimic-perceptive/stargazers)

[Repository](https://github.com/mode1223345/SuperMimic-perceptive) · [Method](https://github.com/mode1223345/SuperMimic-perceptive/blob/3d38bacbaf5bee7e782bdada6a6da678264d0bfa/Ae.md) · [Progress](https://github.com/mode1223345/SuperMimic-perceptive/blob/3d38bacbaf5bee7e782bdada6a6da678264d0bfa/Progress.md)

- **By mode1223345.** Builds on supermimic_vibed in Isaac Lab 3, pretraining a heightmap autoencoder and freezing one shared encoder for the actor, critic and world model.
- **What it provides:** Documents four flat-ground/step-terrain control experiments and separate reconstruction checks; the published control comparisons remain in progress.
- **Useful context:** Maps come from simulator ground truth. Real-depth reconstruction and hardware perception are not integrated, and inherited baseline scores do not establish gains from the encoder. [Source snapshot](https://github.com/mode1223345/SuperMimic-perceptive/blob/3d38bacbaf5bee7e782bdada6a6da678264d0bfa/README.md).

<a href="https://github.com/mode1223345/SuperMimic-perceptive/blob/3d38bacbaf5bee7e782bdada6a6da678264d0bfa/results/Curves.png"><img src="https://raw.githubusercontent.com/mode1223345/SuperMimic-perceptive/3d38bacbaf5bee7e782bdada6a6da678264d0bfa/results/Curves.png" width="720" alt="Training curves · 2026-10-24 snapshot; control comparisons in progress"></a><br><sub>Training curves · 2026-10-24 snapshot; control comparisons in progress</sub>

<br>

## Manipulation and dexterous hands

Arm, hand and object-interaction tasks, with dexterous manipulation grouped here.

<a name="dex-supermimic"></a>

<a name="-dex-supermimic"></a>

### ⭐ Dex SuperMimic [![GitHub stars](https://img.shields.io/github/stars/CumulusAlpha/Dex-Supermimic.svg?style=social)](https://github.com/CumulusAlpha/Dex-Supermimic/stargazers)

[Repository](https://github.com/CumulusAlpha/Dex-Supermimic) · [Installation](https://github.com/CumulusAlpha/Dex-Supermimic/blob/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/README.md#installation) · [Demos](https://github.com/CumulusAlpha/Dex-Supermimic/blob/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/README.md#demos) · [Checkpoints](https://github.com/CumulusAlpha/Dex-Supermimic/releases/tag/pretrained-wuji-v2)

- **By CumulusAlpha.** Adapts world-model-based policy training to Wuji Hand 1/Hand 2 cube reorientation and Wuji Hand 2 pen spinning, using mjlab / MuJoCo Warp and the InstinctMJ task framework.
- **What it provides:** Three task configurations, bundled hand and cube assets, Viser playback, and three 8,000-iteration checkpoints in the `pretrained-wuji-v2` release.
- **Useful context:** This is a dexterous-manipulation adaptation with a different task and reward from humanoid motion tracking. [Source snapshot](https://github.com/CumulusAlpha/Dex-Supermimic/blob/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/README.md).

<table>
  <tr>
    <td width="50%" align="center"><a href="https://github.com/CumulusAlpha/Dex-Supermimic/blob/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/docs/demos/hand1_reorient.gif"><img src="https://raw.githubusercontent.com/CumulusAlpha/Dex-Supermimic/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/docs/demos/hand1_reorient.gif" width="100%" alt="Simulation · Wuji Hand 1 cube reorientation"></a><br><sub>Wuji Hand 1 · cube reorientation</sub></td>
    <td width="50%" align="center"><a href="https://github.com/CumulusAlpha/Dex-Supermimic/blob/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/docs/demos/hand2_pen_spin.gif"><img src="https://raw.githubusercontent.com/CumulusAlpha/Dex-Supermimic/3a7c1a33fd8e5c6cc047e381ea9309da96553c27/docs/demos/hand2_pen_spin.gif" width="100%" alt="Simulation · Wuji Hand 2 pen spinning"></a><br><sub>Wuji Hand 2 · pen spinning</sub></td>
  </tr>
</table>

<br>

<a name="supermimic-for-robot-manipulation"></a>

<a name="-supermimic-for-robot-manipulation"></a>

### ⭐ SuperMimic for Robot Manipulation [![GitHub stars](https://img.shields.io/github/stars/emoPointer/supermimic_manipulation.svg?style=social)](https://github.com/emoPointer/supermimic_manipulation/stargazers)

[Repository](https://github.com/emoPointer/supermimic_manipulation) · [Setup](https://github.com/emoPointer/supermimic_manipulation/blob/810e5768c50117d2fec75f20f9e643a11cd0882b/README.md#install) · [Results](https://github.com/emoPointer/supermimic_manipulation/blob/810e5768c50117d2fec75f20f9e643a11cd0882b/README.md#results)

- **By Zhiqiang Zhou (emoPointer).** Adapts SuperMimic to state-based manipulation with a simulated ARX5 arm in mjlab / MuJoCo Warp across the Lemon, BoxInBin and MugHang tasks.
- **Upstream report:** Held-out reset banks with 256 complete episodes per task at 4,000 iterations reach **100.0%** Lemon, **94.9%** BoxInBin and **96.9%** MugHang success; the runs take **1.8 / 1.9 / 2.8 hours on one A100 80 GB** while sharing the GPU.
- **Useful context:** OmniReset-style reset categories shorten the effective horizon, and contact-based success tests use differentiable geometric surrogates during imagination. The policy observes low-dimensional state only; released checkpoints and reset banks are on Hugging Face. [Source snapshot](https://github.com/emoPointer/supermimic_manipulation/blob/810e5768c50117d2fec75f20f9e643a11cd0882b/README.md).

<a href="https://github.com/emoPointer/supermimic_manipulation"><img src="https://raw.githubusercontent.com/emoPointer/supermimic_manipulation/810e5768c50117d2fec75f20f9e643a11cd0882b/docs/media/lemon.gif" width="480" alt="Simulation · ARX5 Lemon task with two held-out resets"></a><br><sub>Simulation · ARX5 Lemon task · two held-out resets</sub>

<br>

<a name="in-hand-rotation-mjlab"></a>

<a name="-in-hand-rotation-mjlab"></a>

### ⭐ In-Hand Rotation mjlab [![GitHub stars](https://img.shields.io/github/stars/Msornerrrr/in-hand-rotation-mjlab.svg?style=social)](https://github.com/Msornerrrr/in-hand-rotation-mjlab/stargazers)

[Repository](https://github.com/Msornerrrr/in-hand-rotation-mjlab) · [Install](https://github.com/Msornerrrr/in-hand-rotation-mjlab/blob/0ab03eb2244b4a1a020d94ef38a4823bb9e15ba0/README.md#install) · [Results](https://github.com/Msornerrrr/in-hand-rotation-mjlab/blob/0ab03eb2244b4a1a020d94ef38a4823bb9e15ba0/README.md#results) · [Checkpoints](https://github.com/Msornerrrr/in-hand-rotation-mjlab/blob/0ab03eb2244b4a1a020d94ef38a4823bb9e15ba0/README.md#quick-start-the-released-policies)

- **By Msornerrrr.** Applies SuperMimic-style world-model policy learning (an MLP world model refit online, backpropagation through imagined rollouts, a TD(λ) critic and weight averaging) to the LEAP Hand in mjlab / MuJoCo Warp, next to PPO baselines on the same environments: palm-up cube yaw, SO(3) cube reorientation (PPO only) and palm-down fingertip rotation of 22 objects, on a servo model identified on the real hand. Checkpoints for both methods are released.
- **Upstream report:** On cube yaw, the world-model policy reaches PPO's level (≈0.26 reward/s) after **25 minutes and 18M env steps**, where PPO needs 6.5 hours and 262M, and ends at **0.292 vs 0.261**. On palm-down fingertip rotation (64 rollouts per object, 60 s, randomized pad friction 0.25–1.2), a joints-only world-model policy reaches **933°** rewarded yaw with **4.0%** drops, against **675° / 10.4%** for the deployed PPO student distilled from a teacher, and **944° / 2.1%** for the privileged PPO teacher.
- **Useful context:** World-model results are in simulation; the real-robot videos (yaw and SO(3)) show PPO policies. Fingertip numbers use the repository's own evaluation (rotation reward capped at 0.3 rad/s; a drop is 30 mm of drift). Single runs per configuration; wall-clock times are on one RTX 4090. [Source snapshot](https://github.com/Msornerrrr/in-hand-rotation-mjlab/blob/0ab03eb2244b4a1a020d94ef38a4823bb9e15ba0/README.md).

<a href="https://github.com/Msornerrrr/in-hand-rotation-mjlab"><img src="https://raw.githubusercontent.com/Msornerrrr/in-hand-rotation-mjlab/0ab03eb2244b4a1a020d94ef38a4823bb9e15ba0/assets/sim_fingertip.gif" width="480" alt="Simulation · palm-down fingertip rotation of a sphere, cube, cylinder and cuboid by a joints-only world-model policy"></a><br><sub>Simulation · palm-down fingertip rotation, joints-only world-model policy</sub>

<br>

<a name="humanoid-mimic--supermimic"></a>

### Humanoid Mimic · SuperMimic [![GitHub stars](https://img.shields.io/github/stars/shuayyy/humanoid-amp-ppo.svg?style=social)](https://github.com/shuayyy/humanoid-amp-ppo/stargazers)

[Repository](https://github.com/shuayyy/humanoid-amp-ppo) · [Quickstart](https://github.com/shuayyy/humanoid-amp-ppo/blob/681874bab20273ba9211cb92d5ff108900ce3490/README.md#quickstart) · [Results and protocol](https://github.com/shuayyy/humanoid-amp-ppo/blob/681874bab20273ba9211cb92d5ff108900ce3490/docs/supermimic/RESULTS.md)

- **By shuayyy.** Compares SuperMimic and PPO-Sim on shared G1 walking, squatting and box-lifting tasks in mjlab; the repository also contains a separate AMP-PPO stack.
- **Upstream report:** Box-lift success reaches **100% at 31 million environment steps**, reported for two SuperMimic seeds with 64 randomized evaluation episodes; success means finishing within 10 cm of the reference box height.
- **Useful context:** Those SuperMimic scores used clean observations. The newer evaluation adds observation noise, and the published checkpoints have not been re-evaluated under that setting. [Source snapshot](https://github.com/shuayyy/humanoid-amp-ppo/blob/681874bab20273ba9211cb92d5ff108900ce3490/README.md).

<a href="https://github.com/shuayyy/humanoid-amp-ppo/blob/4889389118e0c88d3945dff54d2cd3f992ed815e/assets/supermimic_vs_ppo_lift.mp4"><img src="https://raw.githubusercontent.com/shuayyy/humanoid-amp-ppo/4889389118e0c88d3945dff54d2cd3f992ed815e/assets/supermimic_vs_ppo_lift.gif" width="480" alt="Box lift · SuperMimic 12k / PPO-Sim 6k iterations"></a><br><sub>Box lift · SuperMimic 12k / PPO-Sim 6k iterations</sub>

<br>

## Muscle, interaction and diagnostics

Muscle-actuated bodies, physical interaction and contact-focused diagnostics.

<a name="muscle-supermimic"></a>

<a name="-muscle-supermimic"></a>

### ⭐ Muscle SuperMimic [![GitHub stars](https://img.shields.io/github/stars/kaibohex/muscle-supermimic.svg?style=social)](https://github.com/kaibohex/muscle-supermimic/stargazers)

[Repository](https://github.com/kaibohex/muscle-supermimic) · [Setup](https://github.com/kaibohex/muscle-supermimic/blob/932ac22ca720b1c4db40c4323a3b67bf3c1eaa99/README.md#install) · [Status](https://github.com/kaibohex/muscle-supermimic/blob/932ac22ca720b1c4db40c4323a3b67bf3c1eaa99/README.md#status)

- **By Kaibo He (kaibohex).** Extends SuperMimic to muscle-driven whole-body tracking on MS-Human-700 (700 muscles) and MyoFullBody (354 muscles) in mjlab / MuJoCo Warp.
- **Upstream report:** On MuscleMimic's 108 held-out KIT clips with 4,096 environments on one RTX 5090, MS-Human-700 reaches **0.91 normalized return after 10.1 hours** (iteration 16k, **104 / 108 tracked**); MyoFullBody reaches **0.83 after 6.0 hours** (iteration 10k, **101 / 108 tracked**).
- **Useful context:** Active development. The policy controls muscle excitation at 100 Hz, and the project provides a differentiable torch muscle model plus retargeting tools. The retargeted KIT data is gated and subject to AMASS terms; MS-Human-700 is provided as a Git submodule. [Source snapshot](https://github.com/kaibohex/muscle-supermimic/blob/932ac22ca720b1c4db40c4323a3b67bf3c1eaa99/README.md).

<a href="https://github.com/kaibohex/muscle-supermimic"><img src="https://raw.githubusercontent.com/kaibohex/muscle-supermimic/b7c7cdd83e82399e057cb9d3f1b76f23ca022c7b/docs/assets/teaser_three.gif" width="480" alt="Simulation · MS-Human-700 and MyoFullBody tracking KIT clips at iteration 10000"></a><br><sub>Simulation · MS-Human-700 and MyoFullBody · iteration 10000</sub>

<br>

<a name="supermimic-backflip-diagnostics"></a>

### SuperMimic Backflip Diagnostics [![GitHub stars](https://img.shields.io/github/stars/liudi159/supermimic-backflip-5090.svg?style=social)](https://github.com/liudi159/supermimic-backflip-5090/stargazers)

[Repository](https://github.com/liudi159/supermimic-backflip-5090) · [Results](https://github.com/liudi159/supermimic-backflip-5090/blob/5b313d75e804cdd2ff1ce9bdcfa899a98eca856b/README.md#结果) · [Quickstart](https://github.com/liudi159/supermimic-backflip-5090/blob/5b313d75e804cdd2ff1ce9bdcfa899a98eca856b/README.md#快速入口)

- **By liudi159.** A focused G1 backflip study on Isaac Lab 3 and one RTX 5090, tracking leg symmetry, contact forces, penetration and landing stability.
- **Upstream report:** The final V14 checkpoint completes the rotation and landing hold, but the original strict evaluation records one frame of non-foot penetration and **fails acceptance**.
- **Useful context:** An independent rerun changes the borderline contact outcome. Both records are retained, so the clip should not be read as robust success or reproduction of all paper experiments. [Source snapshot](https://github.com/liudi159/supermimic-backflip-5090/blob/5b313d75e804cdd2ff1ce9bdcfa899a98eca856b/README.md).

<a href="https://github.com/liudi159/supermimic-backflip-5090/blob/5b313d75e804cdd2ff1ce9bdcfa899a98eca856b/media/v14_blue_checker.mp4"><img src="assets/community/backflip.gif" width="480" alt="Simulation · final V14 policy; strict evaluation failed"></a><br><sub>Simulation · final V14 policy; strict evaluation failed</sub>

<br>

<a name="supermimic-pera"></a>

### SuperMimic-PERA [![GitHub stars](https://img.shields.io/github/stars/shangchaohu718/supermimic-pera.svg?style=social)](https://github.com/shangchaohu718/supermimic-pera/stargazers)

[Repository](https://github.com/shangchaohu718/supermimic-pera) · [Current status](https://github.com/shangchaohu718/supermimic-pera/blob/0e89e55187a800341e609129b5d5200a607a467c/README.md#当前状态) · [Skateboarding report](https://github.com/shangchaohu718/supermimic-pera/blob/0e89e55187a800341e609129b5d5200a607a467c/docs/FIRST_SKATEBOARD_SKILL.md)

- **By shangchaohu718.** Builds on UniSuperMimic for G1 interaction experiments, retaining a frozen tracker while developing separate interaction policies in UniLab / MuJoCo.
- **Upstream report:** A separate skateboarding policy completes 30-second simulated runs from one standard and eight held-out perturbed initial states, traveling **39.87–42.13 m**.
- **Useful context:** Tracking and skateboarding are selected as separate branches. A shared world-model-driven interaction actor is not established; box handling and stairs remain unsuccessful in the reported prototype. [Source snapshot](https://github.com/shangchaohu718/supermimic-pera/blob/0e89e55187a800341e609129b5d5200a607a467c/README.md).

<a href="https://github.com/shangchaohu718/supermimic-pera/blob/0e89e55187a800341e609129b5d5200a607a467c/README.md"><img src="assets/community/pera-tracking-results.png" width="720" alt="Report screenshot · tracking checkpoints 500–6000; separate from skateboarding"></a><br><sub>Report screenshot · tracking checkpoints 500–6000; separate from skateboarding</sub>

<br>

## Robot porting and retargeting

Robot-, simulator- and hardware-specific ports, together with motion-retargeting tools.

<a name="supermimic-retargeted"></a>

<a name="-supermimic-retargeted"></a>

### ⭐ SuperMimic Retargeted [![GitHub stars](https://img.shields.io/github/stars/tianshuwu/supermimic-retargeted.svg?style=social)](https://github.com/tianshuwu/supermimic-retargeted/stargazers)

[Repository](https://github.com/tianshuwu/supermimic-retargeted) · [Quickstart](https://github.com/tianshuwu/supermimic-retargeted/blob/ff69a0e5305126eb5b80b323bcd815805bc3df4e/README.md#快速开始) · [Data guide](https://github.com/tianshuwu/supermimic-retargeted/blob/ff69a0e5305126eb5b80b323bcd815805bc3df4e/docs/DATA.md)

- **By tianshuwu.** Extends the CuboiLeo mjlab baseline to G1, A3 and X2 Ultra, adding robot-specific kinematics, SOMA retargeting, coordinate corrections and foot-contact checks.
- **What it provides:** Publishes LAFAN1/BONES-SEED preparation workflows and historical evaluation records. Training weights are not distributed, and motion data must be prepared separately.
- **Useful context:** The reported policies use extra anchor-relative observations computed from simulator truth. These require corresponding state estimation on hardware; real-robot transfer is not validated. [Source snapshot](https://github.com/tianshuwu/supermimic-retargeted/blob/ff69a0e5305126eb5b80b323bcd815805bc3df4e/README.md).

<a href="https://github.com/tianshuwu/supermimic-retargeted/blob/ff69a0e5305126eb5b80b323bcd815805bc3df4e/media/demo.mp4"><img src="https://raw.githubusercontent.com/tianshuwu/supermimic-retargeted/ff69a0e5305126eb5b80b323bcd815805bc3df4e/media/demo-preview.gif" width="480" alt="Simulation · G1 / X2 Ultra / A3"></a><br><sub>Simulation · G1 / X2 Ultra / A3</sub>

<br>

<a name="supermimic-mujoco"></a>

### SuperMimic-MuJoCo [![GitHub stars](https://img.shields.io/github/stars/panhainan2020/SuperMimic-MuJoCo.svg?style=social)](https://github.com/panhainan2020/SuperMimic-MuJoCo/stargazers)

[Repository](https://github.com/panhainan2020/SuperMimic-MuJoCo) · [Setup](https://github.com/panhainan2020/SuperMimic-MuJoCo/blob/db045afa9c52458f213e2c66037387e9c109a03a/README.md#环境安装) · [Evaluation](https://github.com/panhainan2020/SuperMimic-MuJoCo/blob/db045afa9c52458f213e2c66037387e9c109a03a/README.md#评估结果)

- **By panhainan2020.** A standalone mjlab / CPU MuJoCo port of supermimic_vibed for G1, with observation-compatibility profiles, inference weights and held-out 100STYLE evaluation.
- **Upstream report:** The fixed 98k policy completes **40 / 40 LAFAN training motions** at return **0.8713**, and **3,569 / 3,573 unseen 100STYLE clips** at **0.8045**, without fine-tuning.
- **Useful context:** Mean clip duration is 18.77 s for 100STYLE versus 220.55 s for LAFAN; retargeting also differs. Completion only means no termination, not accurate tracking. Cross-source semantic duplicates were not checked. The inference checkpoint does not resume full training. [Source snapshot](https://github.com/panhainan2020/SuperMimic-MuJoCo/blob/db045afa9c52458f213e2c66037387e9c109a03a/README.md).

<a href="https://github.com/panhainan2020/SuperMimic-MuJoCo/blob/db045afa9c52458f213e2c66037387e9c109a03a/README.md"><img src="assets/community/mujoco-evaluation.png" width="720" alt="Report screenshot · LAFAN training motions and unseen 100STYLE clips"></a><br><sub>Report screenshot · LAFAN training motions and unseen 100STYLE clips</sub>

[Full video gallery](https://supermimic-mujoco-results.zippyaspen7.chatgpt.site)

<br>

<a name="supermimic-wheel-legged-wheelbipe"></a>

### SuperMimic Wheel-Legged (wheelbipe) [![GitHub stars](https://img.shields.io/github/stars/RadiantForever/supermimic_wheelbipe.svg?style=social)](https://github.com/RadiantForever/supermimic_wheelbipe/stargazers)

[Repository](https://github.com/RadiantForever/supermimic_wheelbipe) · [Setup](https://github.com/RadiantForever/supermimic_wheelbipe/blob/0bf3456299a9f754289da58dce6c97c46afd3f03/README.md#setup) · [Results](https://github.com/RadiantForever/supermimic_wheelbipe/blob/0bf3456299a9f754289da58dce6c97c46afd3f03/README.md#results)

- **By RadiantForever.** Downstream port of SuperMimic to the wheeled-legged wheelbipe V14_2. The humanoid motion library is replaced by a velocity-command library; a 6-DoF action policy (four leg targets plus two wheel speeds) is optimised inside the differentiable world model, with PhysX / Isaac Lab as the data source and no PPO in the loop.
- **Upstream report:** On a 16-command grid the unified checkpoint reaches **0 / 16 falls** and normalized return **0.983**; a speed-focused checkpoint tracks **1.40 m/s at 0.01 error**, and yaw reaches **10.21 rad/s (1.62 rev/s)** with a **0.20-0.28 m** leg cycle. Single RTX 4090, 4096 environments, 3.72 h cumulative over resumed runs; one run, no seed sweep.
- **Useful context:** A pretrained PPO policy for the same robot is mixed into the world-model buffer for the first 800 iterations only, and no teacher-free ablation was run, so these numbers are not attributable to the method alone. The port requires the robot USD asset from the upstream repository; there is no URDF. [Source snapshot](https://github.com/RadiantForever/supermimic_wheelbipe/blob/0bf3456299a9f754289da58dce6c97c46afd3f03/README.md).

<a href="https://www.bilibili.com/video/BV1haxM6CEGm/"><img src="assets/community/wheelbipe-grid.gif" width="480" alt="Simulation · four commanded conditions"></a><br><sub>Simulation · four commanded conditions: 10 rad/s yaw (top-left), 0.20-0.28 m leg cycle (top-right), 1.5 m/s forward with leg cycle (bottom-left), yaw with leg cycle (bottom-right)</sub>

<br>

<a name="supermimic-e1"></a>

### SuperMimic E1 [![GitHub stars](https://img.shields.io/github/stars/wenconggan/SuperMimic_e1.svg?style=social)](https://github.com/wenconggan/SuperMimic_e1/stargazers)

[Repository](https://github.com/wenconggan/SuperMimic_e1) · [Setup](https://github.com/wenconggan/SuperMimic_e1/blob/d5fbe8f219c438b84633130652c5e6e74beff628/README.md#安装与资源) · [Results](https://github.com/wenconggan/SuperMimic_e1/blob/d5fbe8f219c438b84633130652c5e6e74beff628/README.md#已测结果)

- **By wenconggan.** Adapts the Isaac Lab 3 implementation to the 21-DoF DroidUp E1, with standalone native-MuJoCo sim-to-sim playback and evaluation.
- **Upstream report:** The 164k checkpoint completes **40 / 40 training motions**, return **0.8559**, in Isaac Lab. A separate 168k checkpoint completes **10 / 10 sampled eight-second segments** in native MuJoCo.
- **Useful context:** Complete-clip evaluation and independently initialized short segments use different protocols. Neither result measures unseen-motion generalization or hardware transfer. [Source snapshot](https://github.com/wenconggan/SuperMimic_e1/blob/d5fbe8f219c438b84633130652c5e6e74beff628/README.md).

<a href="https://github.com/wenconggan/SuperMimic_e1/blob/d5fbe8f219c438b84633130652c5e6e74beff628/docs/assets/e1_random10_80s.mp4"><img src="https://raw.githubusercontent.com/wenconggan/SuperMimic_e1/d5fbe8f219c438b84633130652c5e6e74beff628/docs/assets/e1_preview.gif" width="480" alt="E1 sim-to-sim · native MuJoCo"></a><br><sub>E1 sim-to-sim · native MuJoCo</sub>

<br>

<a name="supermimic-oli"></a>

### SuperMimic Oli [![GitHub stars](https://img.shields.io/github/stars/liuskywalkerjskd/supermimic_oli.svg?style=social)](https://github.com/liuskywalkerjskd/supermimic_oli/stargazers)

[Repository](https://github.com/liuskywalkerjskd/supermimic_oli) · [Setup](https://github.com/liuskywalkerjskd/supermimic_oli/blob/2dc90d90e89fb2e097e985c84c8b99a77708fa5f/README.md#setup) · [Results](https://github.com/liuskywalkerjskd/supermimic_oli/blob/2dc90d90e89fb2e097e985c84c8b99a77708fa5f/README.md#results)

- **By liuskywalkerjskd.** Ports supermimic_vibed to the 31-DoF LimX Oli in Isaac Lab 3, adding motion retargeting, robot kinematics and full-motion video export.
- **Upstream report:** At iteration **18,000**, the original 40-motion LAFAN1 evaluation reports return **0.6783** and **36 / 40 completed clips**, after about **2.20 hours on one RTX 4090**.
- **Useful context:** The displayed walking clip is a selected excerpt. Use the full-library evaluation when judging tracking coverage. [Source snapshot](https://github.com/liuskywalkerjskd/supermimic_oli/blob/2dc90d90e89fb2e097e985c84c8b99a77708fa5f/README.md).

<a href="https://github.com/liuskywalkerjskd/supermimic_oli/blob/2dc90d90e89fb2e097e985c84c8b99a77708fa5f/results/oli_walk1_subject1_full.mp4"><img src="https://raw.githubusercontent.com/liuskywalkerjskd/supermimic_oli/2dc90d90e89fb2e097e985c84c8b99a77708fa5f/results/oli_walk1_subject1_preview.gif" width="480" alt="Simulation · selected Oli walking excerpt"></a><br><sub>Simulation · selected Oli walking excerpt</sub>

<br>

<a name="supermimic-on-apple-m5"></a>

### SuperMimic on Apple M5 [![GitHub stars](https://img.shields.io/github/stars/WXyuany/supermimic-m5.svg?style=social)](https://github.com/WXyuany/supermimic-m5/stargazers)

[Repository](https://github.com/WXyuany/supermimic-m5) · [Run the released model](https://github.com/WXyuany/supermimic-m5/blob/42451591718e1a9a5ec601366997f47c0ad180a3/README.md#三步运行已训练模型) · [Results](https://github.com/WXyuany/supermimic-m5/blob/42451591718e1a9a5ec601366997f47c0ad180a3/README.md#实验结果)

- **By WXyuany.** Adapts the CuboiLeo G1 baseline to Apple Silicon, using CPU MuJoCo for physics and PyTorch MPS for learning, with released weights and playback tools.
- **Upstream report:** For the released 21k checkpoint on a 24 GB Apple M5, seed 0, the original 40-motion evaluation reports return **0.7081** and **25 / 40 completed clips**; a fresh-environment check completes **26 / 40**.
- **Useful context:** Return is normalized by executed steps without zero-padding after failure, and the actor uses nine extra anchor-observation dimensions. Read return together with completion; held-out generalization is untested. [Source snapshot](https://github.com/WXyuany/supermimic-m5/blob/42451591718e1a9a5ec601366997f47c0ad180a3/README.md).

<a href="https://github.com/WXyuany/supermimic-m5/blob/42451591718e1a9a5ec601366997f47c0ad180a3/assets/videos/walk1_subject1.mp4"><img src="https://raw.githubusercontent.com/WXyuany/supermimic-m5/42451591718e1a9a5ec601366997f47c0ad180a3/assets/images/walk-preview.gif" width="480" alt="Simulation · G1 walking on Apple M5"></a><br><sub>Simulation · G1 walking on Apple M5</sub>

<br>

## Real-robot deployment and Sim2Real

Real-robot runtimes and sim-to-real transfer paths.

<a name="supermimic-repro-sim2real"></a>

<a name="-supermimic-repro-sim2real"></a>

### ⭐ SuperMimic-Repro-Sim2Real [![GitHub stars](https://img.shields.io/github/stars/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real.svg?style=social)](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/stargazers)

[Repository](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real) · [Quickstart](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/blob/f8f60d7bbdba68468c050ef100af02d752ca238e/README.md#快速开始) · [v1.1 field notes](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/blob/f8f60d7bbdba68468c050ef100af02d752ca238e/docs/REAL_ROBOT_LEAN35KFS.md) · [G1 deployment](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/blob/f8f60d7bbdba68468c050ef100af02d752ca238e/docs/DEPLOY_G1.md)

- **By NJU R&amp;L Group Embodied Lab.** Extends the CuboiLeo mjlab baseline with custom dance/video-motion tools, clip-specific fine-tuning, ONNX export and G1 deployment through native MuJoCo and the Unitree SDK.
- **Upstream report:** v1.0 publishes a roughly **46-second real-G1 dance** assembled from four motion segments. In v1.1, the clip-specific `e24_0355000` policy completed a roughly **22-second dance twice on the real G1**, including two rapid turns and a one-foot landing jump; nine earlier models had failed this clip. Both v1.1 runs used a slack safety tether, and repeating one model is not an ablation.
- **Useful context:** The v1.1 checkpoint is specialized to that single dance, not general motion tracking. Paper-style observations and anchor-augmented training remain separate configurations. [Source snapshot](https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/blob/f8f60d7bbdba68468c050ef100af02d752ca238e/README.md).

<a href="https://github.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/releases/download/v1.1/shanshenbu_pro_real_robot.mp4"><img src="https://raw.githubusercontent.com/NJU-R-L-Group-Embodied-Lab/SuperMimic-Repro-Sim2Real/f8f60d7bbdba68468c050ef100af02d752ca238e/docs/assets/shanshenbu_pro_demo.gif" width="480" alt="Real G1 · v1.1 dance with fast turns and a one-foot landing jump"></a><br><sub>Real G1 · v1.1 clip-specific dance; human reference on the left, robot on the right</sub>

<br>

<a name="supermimic-g1-deployment"></a>

### SuperMimic G1 Deployment [![GitHub stars](https://img.shields.io/github/stars/KyrieYoung926/supermimic_deploy.svg?style=social)](https://github.com/KyrieYoung926/supermimic_deploy/stargazers)

[Repository](https://github.com/KyrieYoung926/supermimic_deploy) · [MuJoCo guide](https://github.com/KyrieYoung926/supermimic_deploy/blob/7e63e3bbd5150d55afbdece28278781800f3ed21/README.md#3-run-in-mujoco) · [Real-G1 guide](https://github.com/KyrieYoung926/supermimic_deploy/blob/7e63e3bbd5150d55afbdece28278781800f3ed21/README.md#4-run-on-the-real-g1)

- **By KyrieYoung926.** A deployment runtime for a SuperMimic-Reproduced policy on the 29-DoF G1, using ONNX Runtime, MuJoCo and Unitree SDK2.
- **What it provides:** Provides both simulation and real-G1 demos, with separate guides for fetching deployment assets and running the policy on each target.
- **Useful context:** This repository covers deployment, not a new training benchmark. Motion data, model weights and robot assets retain their own terms beyond the code license. [Source snapshot](https://github.com/KyrieYoung926/supermimic_deploy/blob/7e63e3bbd5150d55afbdece28278781800f3ed21/README.md).

<a href="https://github.com/KyrieYoung926/supermimic_deploy"><img src="https://raw.githubusercontent.com/KyrieYoung926/supermimic_deploy/7e63e3bbd5150d55afbdece28278781800f3ed21/media/deploy_real.gif" width="480" alt="Real G1 · upstream deployment demo"></a><br><sub>Real G1 · upstream deployment demo</sub>

<br>

## Inspired experiments

Ideas transferred to other control settings, with different tasks and evaluation protocols.

<a name="flatworld--supermimic-2d"></a>

<a name="-flatworld--supermimic-2d"></a>

### ⭐ FlatWorld · SuperMimic-2D [![GitHub stars](https://img.shields.io/github/stars/swaggyliu/FlatWorld.svg?style=social)](https://github.com/swaggyliu/FlatWorld/stargazers)

[Repository](https://github.com/swaggyliu/FlatWorld) · [Quickstart](https://github.com/swaggyliu/FlatWorld/blob/601d96c3aa69b5b226533f767d1c2e6f917c5a5d/supermimic2d/README.md#quick-start) · [Reference motions](https://github.com/swaggyliu/FlatWorld/blob/601d96c3aa69b5b226533f767d1c2e6f917c5a5d/supermimic2d/README.md#reference-motions-lafan-like-2d)

- **By swaggyliu.** Recreates the shared-world-model and imagined-policy-learning loop in FlatWorld with an eight-joint 2D humanoid and motion-tracking tasks.
- **What it provides:** Provides training, reference baking, per-skill rendering and a **33.3-second multi-skill promo** covering walking, running, jumping, dancing, fighting, crouching and fall/get-up.
- **Useful context:** References are procedural, LAFAN-like 2D motions, not the LAFAN1 dataset. The character also uses a mild root assist, so this is an illustrative adaptation rather than a G1 benchmark. [Source snapshot](https://github.com/swaggyliu/FlatWorld/blob/601d96c3aa69b5b226533f767d1c2e6f917c5a5d/supermimic2d/README.md).

<a href="https://github.com/swaggyliu/FlatWorld/blob/886dad634c44ed652eea951be62370478f367d8b/docs/media/promo_supermimic.mp4"><img src="assets/community/flatworld.gif" width="480" alt="2D simulation · 33-second multi-skill motion-tracking promo"></a><br><sub>2D simulation · full 33.3-second multi-skill promo</sub>

<a name="g05--supermimic-style-steering"></a>

### G0.5 · SuperMimic-style Steering [![GitHub stars](https://img.shields.io/github/stars/azizkhadraoui/g05.svg?style=social)](https://github.com/azizkhadraoui/g05/stargazers)

[Repository](https://github.com/azizkhadraoui/g05) · [Experiment code](https://github.com/azizkhadraoui/g05/blob/e3de0de50db7d90068483e2d30f2eacd781300b4/jobs/119_smsteer.py)

- **By azizkhadraoui.** Transfers SuperMimic-style gradient-based learning to G0.5 VLA steering on LIBERO: a noise policy is trained through a frozen flow sampler using world-model and critic gradients.
- **Useful context:** This is one task-specific steering experiment within a broader VLA stack. The linked script identifies the relevant method; the repository’s other planning and memory results are separate experiments. [Source snapshot](https://github.com/azizkhadraoui/g05/blob/e3de0de50db7d90068483e2d30f2eacd781300b4/jobs/119_smsteer.py).

<a href="https://github.com/azizkhadraoui/g05/blob/e3de0de50db7d90068483e2d30f2eacd781300b4/README.md"><img src="assets/community/g05-steering-entry.png" width="720" alt="Code index screenshot · world-model / critic steering experiment"></a><br><sub>Code index screenshot · world-model / critic steering experiment</sub>

<br>

## Related methods and baselines

These works provide methodological background or comparison points; they are separate research projects.

| Work | Connection | Primary resources |
| --- | --- | --- |
| **SuperTrack** (2021) | Earlier character motion tracking through a learned differentiable world model and gradient-based control learning. | [Author explanation](https://www.ubisoft.com/en-us/studio/laforge/news/7fMzaMaDgnd0gqPsCaJZYb/supertrack-motion-tracking-for-physically-simulated-characters-using-supervised-learning) · [Paper](https://staticctf.ubisoft.com/J3yJr34U2pZ2Ieem48Dwy9uqj5PNUQTn/OXYoOEqVwwtxSMiPzMIva/302e9a76da0b1f95ab62d6c766179868/SuperTrack.pdf) |
| **BeyondMimic** (2025) | Humanoid motion tracking and guided diffusion control; `supermimic_vibed` references its actuator and task conventions. | [Project](https://beyondmimic.github.io/) · [Paper](https://arxiv.org/abs/2508.08241) |
| **SONIC** (2025) | Large-scale humanoid motion tracking; the original SuperMimic work compares against a released SONIC checkpoint. | [Project](https://nvlabs.github.io/GEAR-SONIC/) · [Paper](https://arxiv.org/abs/2511.07820) · [Code](https://github.com/NVlabs/GR00T-WholeBodyControl) |

## Data and learning resources

- [LAFAN1 retargeting dataset](https://huggingface.co/datasets/lvhaidong/LAFAN1_Retargeting_Dataset) — G1 motion assets used by `supermimic_vibed`, UniSuperMimic, and SuperMimic-Reproduced. Follow each repository's preparation instructions and the dataset's own terms.
- [BONES-SEED](https://huggingface.co/datasets/bones-studio/seed) — the motion-data source used for the original paper's large-scale benchmark. The raw dataset and paper-filtered evaluation set have different counts. Access requires accepting the dataset's terms on Hugging Face.
- [Official interactive demo](https://supermimic.github.io/demo/) — explore the original policy in the browser before choosing a training stack.
- [Official method explanation](https://supermimic.github.io/#loop) — simulator collection, model fitting, and policy learning.
- [InstinctMJ releases](https://github.com/project-instinct/InstinctMJ/releases) — upstream distribution of task data and model assets; check the release description for the relevant branch and task.
- [awesome-supermimic-community](https://github.com/vicfei/awesome-supermimic-community) — community hub with language-tagged deep dives (Chinese-reading section included), a status-tracked reproduction board, and the world-model lineage and toolchain; implementations and extensions stay in this primary list.

## Contributing

Have a new implementation, extension, tutorial, or demo? Open a pull request using the [contribution guide](CONTRIBUTING.md). Include the original source, the relationship to SuperMimic, the relevant branch, and evidence for any result you quote.

## Citation

When building on the method, cite the **original SuperMimic paper** and credit the implementation you use. BibTeX below follows the [official project](https://supermimic.github.io/#cite):

```bibtex
@inproceedings{liao2026supermimic,
  title     = {{SuperMimic}: Scaling Humanoid Whole-Body Control
               with One Differentiable World Model},
  author    = {Liao, Qiayuan and Shao, Yiyang and Long, Junfeng and
               Zakka, Kevin and Horowitz, Roberto and Abbeel, Pieter and
               Sreenath, Koushil},
  booktitle = {Conference on Robot Learning (CoRL)},
  year      = {2026}
}
```

## Acknowledgements and license

Thanks to the original SuperMimic authors and all community maintainers. The presentation of this list is inspired by [Awesome Nano Banana Images](https://github.com/PicoTrex/Awesome-Nano-Banana-images) and [Awesome World Models](https://github.com/knightnemo/Awesome-World-Models).

The original curation text in this collection is released under [CC0 1.0](LICENSE). Third-party code, papers, datasets, and media retain their respective rights and terms. This includes the [original paper figure and official video previews](assets/official/README.md) stored in this repository; they are not covered by this collection's CC0 dedication. [Community media previews and credits](assets/community/README.md) follow the same attribution rule.

## Star History

<p align="center"><b>If this list helps you, consider <a href="https://github.com/miao-org/awesome-supermimic">starring the repository</a> so more people can discover it.</b></p>

<p align="center">
  <a href="https://star-history.com/#miao-org/awesome-supermimic&Date">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=miao-org/awesome-supermimic&type=Date&theme=dark">
      <img src="https://api.star-history.com/svg?repos=miao-org/awesome-supermimic&type=Date" alt="Star history chart for miao-org/awesome-supermimic" width="100%">
    </picture>
  </a>
</p>
