<div align="center">
  <img src="assets/images/CraftUtopia.png" width="240" alt="CraftUtopia logo">

  # CraftUtopia

  **An LLM-based MAS that <span style="color:#d32f2f;"><b>constructs 3D</b></span> buildings <span style="color:#d32f2f;"><b>from a single 2D image</b></span> in Minecraft and <span style="color:#d32f2f;"><b>scales efficiently</b></span> as the team size increases.**

  <p>
    <a href="README.md"><b>English</b></a> · <a href="README_zh.md"><b>中文</b></a>
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Agent-2D%20to%20Blueprint%20to%20Build-blue" alt="Agent badge">
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

---

## Results


- **Consistent success:** CraftUtopia achieves 100% success across all three builds using only a single 2D image
<div align="center">
  <img src="assets/images/img2build.png" width="90%" style="height: auto;" alt="Multiple builds from 2D images">
</div>

- **Efficient scaling:** Build time decreases substantially as more workers are added.
<div align="center">
  <img src="assets/images/metrics_comparison.png" width="90%" style="height: auto;" alt="Scalability with more workers">
</div>

- **Reliable execution:** MINDcraft fails to complete the build under any agent configuration, even with 3D input, whereas CraftUtopia builds reliably from a single 2D image.
<div align="center">
  <img src="assets/images/compare.png" width="90%" style="height: auto;" alt="Baseline comparison">
</div>

---

## System Architecture

<p align="center">
  <img src="assets/images/architecture.jpg" alt="CraftUtopia architecture diagram">
</p>

CraftUtopia is a hierarchical multi-agent system for in-game construction. The **Manager -> Foreman -> Worker** hierarchy splits work into non-overlapping regions, coordinates execution, and performs block placements in Minecraft. Skill distillation captures successful routines to reduce replanning and improve scalability.
