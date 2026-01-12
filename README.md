<div align="center">
  <img src="assets/images/CraftUtopia.png" width="240" alt="CraftUtopia logo">

  # CraftUtopia

  **An LLM-based MAS that <span style="color:#d32f2f;"><b>constructs 3D</b></span> buildings <span style="color:#d32f2f;"><b>from a single 2D image</b></span> in Minecraft and <span style="color:#d32f2f;"><b>scales efficiently</b></span> as the team size increases.**

  <p>
    <a href="README.md"><b>English</b></a> · <a href="README_zh.md"><b>中文</b></a>
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Pipeline-2D%20to%20Blueprint%20to%20Build-blue" alt="Pipeline badge">
    <img src="https://img.shields.io/badge/Coordination-Manager%2FForeman%2FWorker-orange" alt="Coordination badge">
    <img src="https://img.shields.io/badge/Skills-Distillation-purple" alt="Skills badge">
  </p>

  <p>
    <a href="#demo-video">Demo Video</a> ·
    <a href="#highlights">Highlights</a> ·
    <a href="#overview">Overview</a> ·
    <a href="#results">Results</a> ·
    <a href="#project-introduction">Project Introduction</a> ·
    <a href="#system-architecture">System Architecture</a> ·
    <a href="#mechanisms">Mechanisms</a> ·
    <a href="#workflow">Workflow</a> ·
    <a href="#agent-roles">Agent Roles</a>
  </p>
</div>

---

## Demo Video

<div align="center">
  <a href="https://youtu.be/NkG13PLTBz4">
    <img src="https://img.youtube.com/vi/NkG13PLTBz4/hqdefault.jpg" width="90%" alt="Demo video on YouTube">
  </a>
</div>

You can also download the MP4 and MOV source files from this repository (`demo.mp4`, `demo.mov`).

## Highlights

<div align="center">
  <img src="assets/images/highlight.png" width="90%" alt="Highlights">
</div>

- Supports <span style="color:#d32f2f;"><b>3D construction from a single 2D image</b></span>.
- Uses a hierarchical agent architecture (<span style="color:#d32f2f;"><b>manager -> foreman -> worker</b></span>) to improve coordination efficiency.
- Distills workers' successful action sequences into <span style="color:#d32f2f;"><b>reusable, code-based skills</b></span>.
- Achieves a <span style="color:#d32f2f;"><b>100% build success rate</b></span> across three representative builds.
- Scales effectively: <span style="color:#d32f2f;"><b>more workers -> faster builds</b></span>.
- Demonstrates strong generalization to <span style="color:#d32f2f;"><b>any building types</b></span>.
- Exhibits <span style="color:#d32f2f;"><b>human-like emergent behaviors</b></span>, e.g., <span style="color:#d32f2f;"><b>autonomously learning scaffolding</b></span>.

## Overview

> CraftUtopia orchestrates a full-stack build pipeline: an image-to-blueprint design stage and a hierarchical, multi-agent execution stage inside Minecraft. The system coordinates parallel, non-overlapping builds with shared skills and structured task decomposition.

### Key Capabilities

- Image-to-blueprint conversion for block-accurate builds.
- Hierarchical coordination that scales teams without collisions.
- Parallel execution with manager-foreman-worker task partitioning.
- Skill distillation that reuses repeated routines across teams.

## Results

<div align="center">
  <table width="90%">
  <tr>
  <td align="center"><b>Success Rate</b><br><b><span style="color:#d32f2f;">100%</span></b></td>
  <td align="center"><b>Team Speedup</b><br><b><span style="color:#d32f2f;">6 workers</span>: <span style="color:#d32f2f;">3.9x faster</span> than 1 worker</b></td>
  <td align="center"><b>LLM Cost</b><br><b><span style="color:#d32f2f;">1/4</span> of original</b></td>
  </tr>
  <tr>
  <td align="center"><b>Baseline Gap</b><br><b>MINDcraft <span style="color:#d32f2f;">13.33%</span></b></td>
  <td align="center"><b>Scalability</b><br><b><span style="color:#d32f2f;">6 workers</span>: <span style="color:#d32f2f;">1.5x faster</span> than 3 workers</b></td>
  <td align="center"><b>Large Blueprint</b><br><b><span style="color:#d32f2f;">40</span> levels, <span style="color:#d32f2f;">~20k</span> blocks</b></td>
  </tr>
  </table>
</div>

<br/>

<table align="center" width="100%">
<tr>
<td align="center" width="50%">
<img src="assets/images/tiantan.png" width="95%" alt="Large blueprint build">
<br/><sub><b>Large-scale:</b> 40-layer blueprint with ~20k blocks.</sub>
</td>
<td align="center" width="50%">
<img src="assets/images/img2build.png" width="95%" alt="Multiple builds from 2D images">
<br/><sub><b>Diverse inputs:</b> reconstructing multiple buildings from PNG images.</sub>
</td>
</tr>
<tr>
<td align="center" width="50%">
<img src="assets/images/metrics_comparison.png" width="95%" alt="Scalability with more workers">
<br/><sub><b>Scaling:</b> completion time decreases as worker count increases.</sub>
</td>
<td align="center" width="50%">
<img src="assets/images/compare.png" width="95%" alt="Baseline comparison">
<br/><sub><b>Baseline gap:</b> CraftUtopia completes builds where MINDcraft fails.</sub>
</td>
</tr>
</table>

### Results Summary

- **CraftUtopia achieves a 100% build success rate across three representative structures with five trials each, using only a single 2D reference image per build.**
- **Compared to MINDcraft, CraftUtopia completes Temple of Heaven and NCPA where the baseline fails; on Pyramids the baseline reaches only 13.33% success.**
- **Scaling improves speed: on NCPA, 6 workers are 1.5x faster than 3 workers and 3.9x faster than 1 worker.**
- **The system handles large-scale blueprints (40 levels, ~20k blocks) and generalizes across diverse building types.**
- **Skill distillation reduces repeated LLM calls to about one quarter of the original cost and supports consistent execution.**
- **Emergent behaviors such as autonomous scaffolding use appear during long-horizon builds.**

---

## Project Introduction

> CraftUtopia targets collaborative construction in an open-world game environment. It operates under long-horizon tasks, partial observability, and non-stationary dynamics, and builds directly from a **single 2D reference image** without relying on predefined templates. The system follows a Design-then-Build pipeline and scales through hierarchical coordination and skill acquisition.

### Challenges We Address

- **Open-world setting**: long-horizon tasks, partial observability, and non-stationary dynamics.
- **Template dependence**: builds directly from a single 2D reference image rather than predefined templates or blueprints.
- **Scaling limits**: prior work shows larger teams can increase coordination friction instead of speed; CraftUtopia is designed to scale.

---

## System Architecture

<p align="center">
  <img src="assets/images/architecture.jpg" alt="CraftUtopia architecture diagram">
</p>

CraftUtopia follows a two-stage pipeline drawn from the paper: **Design** converts a single 2D reference image into a Minecraft-compatible 3D blueprint, and **Build** decomposes that blueprint into spatially disjoint subtasks for parallel execution.

<table align="center" width="100%">
<tr>
<td width="50%" valign="top" align="center">

### Design Stage
- Reconstruct a 3D model from the input image (TRELLIS.2).
- Convert the model into a block-based blueprint (ObjToSchematic).
- Use LLMs to compile the blueprint into a structure file with explicit block types and placements.

</td>
<td width="50%" valign="top" align="center">

### Build Stage
- **Manager -> Foreman -> Worker** hierarchy splits work across non-overlapping regions.
- Foremen plan for their teams and workers execute in Minecraft.
- **Skill acquisition** distills repeated routines into a shared library, reducing LLM replanning and accelerating future builds.

</td>
</tr>
</table>

---

## Mechanisms

CraftUtopia relies on two mechanisms:

### 1) Hierarchical coordination (manager -> foreman -> worker)
- The manager decomposes the blueprint into **spatially disjoint regions** and assigns each region as a team-level goal.  
- Each foreman plans within its assigned region and schedules workers.  
- Workers execute local block placement and report progress upward, reducing cross-team interference.

### 2) Skill acquisition and reuse
- Foremen detect recurring action routines during execution.  
- These routines are reported to the manager, curated into a shared skill library, and distributed to all teams.  
- Foremen invoke learned skills instead of repeated LLM replanning, improving speed and stability at scale.

---

## Workflow

1. **Design (2D to 3D blueprint)**
2. **Build (blueprint to world)**

<details>
<summary><b>Design details</b></summary>

- The architectural designer reconstructs a 3D model from a 2D image.  
- The model is converted into a Minecraft-compatible block blueprint.  
- A structural task file is exported for execution.

</details>

<details>
<summary><b>Build details</b></summary>

- The project manager decomposes the blueprint into disjoint subtasks.  
- Foremen schedule and coordinate parallel teams.  
- Workers place blocks and report progress back to the manager.

</details>

---

## Agent Roles

- **Architectural designer**: Converts 2D inputs into a buildable blueprint.
- **Project manager**: Splits the blueprint into conflict-free task units.
- **Foremen**: Plan execution order and assign work to teams.
- **Workers**: Execute block placement in the game world.
