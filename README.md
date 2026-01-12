<div align="center">
  <img src="assets/images/CraftUtopia.png" width="240" alt="CraftUtopia logo">

  # CraftUtopia

  **A multi-agent Minecraft construction pipeline that turns 2D images into coordinated 3D builds**

  <p>
    <a href="README.md"><b>English</b></a> · <a href="README_zh.md"><b>中文</b></a>
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Pipeline-2D%20to%20Blueprint%20to%20Build-blue" alt="Pipeline badge">
    <img src="https://img.shields.io/badge/Coordination-Manager%2FForeman%2FWorker-orange" alt="Coordination badge">
    <img src="https://img.shields.io/badge/Skills-Distillation-purple" alt="Skills badge">
  </p>

  <p>
    <a href="#overview">Overview</a> ·
    <a href="#demo-video">Demo Video</a> ·
    <a href="#results">Results</a> ·
    <a href="#project-introduction">Project Introduction</a> ·
    <a href="#system-architecture">System Architecture</a> ·
    <a href="#mechanisms">Mechanisms</a> ·
    <a href="#workflow">Workflow</a> ·
    <a href="#agent-roles">Agent Roles</a>
  </p>
</div>

---

## Overview

> CraftUtopia orchestrates a full-stack build pipeline: an image-to-blueprint design stage and a hierarchical, multi-agent execution stage inside Minecraft. The system coordinates parallel, non-overlapping builds with shared skills and structured task decomposition.

### Key Capabilities

- Image-to-blueprint conversion for block-accurate builds.
- Hierarchical coordination that scales teams without collisions.
- Parallel execution with manager-foreman-worker task partitioning.
- Skill distillation that reuses repeated routines across teams.

## Demo Video

<div align="center">
  <a href="https://youtu.be/NkG13PLTBz4">
    <img src="https://img.youtube.com/vi/NkG13PLTBz4/hqdefault.jpg" width="90%" alt="Demo video on YouTube">
  </a>
</div>

You can also download the MP4 and MOV source files from this repository (`demo.mp4`, `demo.mov`).

---

## Results

<div align="center">
  <table width="90%">
  <tr>
  <td align="center"><b>Success Rate</b><br><sub>Across three builds in five trials</sub><br><b>100%</b></td>
  <td align="center"><b>Scalability</b><br><sub>NCPA completion time</sub><br><b>6 workers: 1.5x vs 3</b></td>
  <td align="center"><b>Team Speedup</b><br><sub>NCPA completion time</sub><br><b>3.9x vs 1 worker</b></td>
  </tr>
  </table>
</div>

<br/>

**Highlights from the paper and demo builds:**

- **100% success rate** across three builds in five trials using only a single 2D reference image.
- **Baseline gap**: MINDcraft fails to complete Temple of Heaven and NCPA even with a full 3D blueprint, and only succeeds in 2/5 trials on the Pyramids.
- **Scalability**: more workers consistently reduce completion time (NCPA: 6 workers are 1.5x faster than 3 workers and 3.9x faster than 1 worker).
- **Large-scale construction**: 40 levels and nearly 20k blocks in a single blueprint.
- **Diverse inputs**: a single pipeline reproduces multiple structures from different PNG images.

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
