<div align="center">
  <img src="assets/images/CraftUtopia.png" width="240" alt="CraftUtopia logo">

  # CraftUtopia

  **一个基于 LLM 的 MAS，在 Minecraft 中从 <span style="color:#d32f2f;"><b>单张 2D 图像</b></span> <span style="color:#d32f2f;"><b>构建 3D</b></span> 建筑，并随团队规模提升而 <span style="color:#d32f2f;"><b>高效扩展</b></span>。**

  <p align="center">
    <a href="README.md"><b>English</b></a> · <a href="README_zh.md"><b>中文</b></a>
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Pipeline-2D%20to%20Blueprint%20to%20Build-blue" alt="Pipeline badge">
    <img src="https://img.shields.io/badge/Coordination-Manager%2FForeman%2FWorker-orange" alt="Coordination badge">
    <img src="https://img.shields.io/badge/Skills-Distillation-purple" alt="Skills badge">
  </p>

  <p>
    <a href="#演示视频">演示视频</a> ·
    <a href="#亮点">亮点</a> ·
    <a href="#概览">概览</a> ·
    <a href="#结果">结果</a> ·
    <a href="#项目介绍">项目介绍</a> ·
    <a href="#系统架构">系统架构</a> ·
    <a href="#机制">机制</a> ·
    <a href="#流程">流程</a> ·
    <a href="#角色">角色</a>
  </p>
</div>

---

## 演示视频

<div align="center">
  <a href="https://youtu.be/NkG13PLTBz4">
    <img src="https://img.youtube.com/vi/NkG13PLTBz4/hqdefault.jpg" width="90%" alt="YouTube 演示视频">
  </a>
</div>

也可以从仓库中下载 MP4 和 MOV 格式的源文件（`demo.mp4`、`demo.mov`）。

## 亮点

<div align="center">
  <img src="assets/images/highlight.png" width="90%" alt="亮点概览">
</div>

- 支持 <span style="color:#d32f2f;"><b>单张 2D 图像到 3D 建造</b></span>。
- 采用分层智能体架构（<span style="color:#d32f2f;"><b>manager -> foreman -> worker</b></span>）提升协作效率。
- 将工人的成功动作序列蒸馏为 <span style="color:#d32f2f;"><b>可复用的代码技能</b></span>。
- 三个代表性建筑实验中达到 <span style="color:#d32f2f;"><b>100% 建造成功率</b></span>。
- 具备良好扩展性：<span style="color:#d32f2f;"><b>人数越多，建造越快</b></span>。
- 展示强泛化能力，可适配 <span style="color:#d32f2f;"><b>任意建筑类型</b></span>。
- 呈现 <span style="color:#d32f2f;"><b>类人涌现行为</b></span>，如 <span style="color:#d32f2f;"><b>自主学习使用脚手架</b></span>。

## 概览

> CraftUtopia 通过“图像到蓝图”的设计阶段与分层多智能体的执行阶段，完成 Minecraft 中的大规模协作建造。系统以共享技能与结构化任务分解为核心，实现并行、互不干扰的构建。

### 核心能力

- 图像到蓝图的转换，实现精确的方块级建造。
- 分层协作，扩大规模时避免相互冲突。
- 管理者-工头-工人式并行执行。
- 技能蒸馏，复用重复操作以减少规划开销。

## 结果


<br/>

<div align="center">
<table align="center" width="100%" style="margin: 0 auto; width: 100%;">
<tr>
<td align="center" width="100%">
<img src="assets/images/tiantan.png" height="300" alt="超大规模建造">
<br/><sub><b>大规模：</b>系统可处理大规模蓝图，包括 40 层、约 2 万方块的设计。</sub>
</td>
</tr>
<tr>
<td align="center" width="100%">
<img src="assets/images/img2build.png" height="300" alt="多种图像到建筑">
<br/><sub><b>多样化输入：</b>从不同 PNG 输入重建多样化建筑。CraftUtopia 所有建筑建造成功率 100%。</sub>
</td>
</tr>
<tr>
<td align="center" width="100%">
<img src="assets/images/metrics_comparison.png" height="300" alt="可扩展性">
<br/><sub><b>扩展性：</b>工人数量增加，完成时间下降；6 人比 3 人快 1.5x，比 1 人快 3.9x。</sub>
</td>
</tr>
<tr>
<td align="center" width="100%">
<img src="assets/images/compare.png" height="300" alt="基线对比">
<br/><sub><b>基线对比：</b>与 MINDcraft 相比，CraftUtopia 可完成其失败的建造任务。</sub>
</td>
</tr>
</table>
</div>

-----

## 项目介绍

> CraftUtopia 面向开放世界中的协作建造任务，具有长时序、部分可观测和动态变化的环境特征，并且直接从**单张 2D 参考图像**进行建造，不依赖预定义模板。系统采用“设计-建造”两阶段流程，并通过分层协作与技能获取实现可扩展性。

### 我们解决的关键问题

- **开放世界设定**：长时序任务、部分可观测与非平稳动态。
- **模板依赖**：无需预定义模板或 3D 蓝图，仅基于 2D 图像。
- **规模瓶颈**：避免多工人带来的协作摩擦，提升整体效率。

---

## 系统架构

<p align="center">
  <img src="assets/images/architecture.jpg" alt="CraftUtopia 架构图">
</p>

CraftUtopia 采用两阶段流程：**设计**将单张 2D 参考图像转换为 Minecraft 兼容的 3D 蓝图；**建造**将蓝图拆分为空间互不重叠的子任务并并行执行。

<table align="center" width="100%">
<tr>
<td width="50%" valign="top" align="center">

### 设计阶段
- 从 2D 图像重建 3D 模型（TRELLIS.2）。
- 转换为基于方块的蓝图（ObjToSchematic）。
- 由 LLM 生成包含方块类型与位置的结构文件。

</td>
<td width="50%" valign="top" align="center">

### 建造阶段
- **Manager -> Foreman -> Worker** 分层结构将任务划分为互不重叠区域。
- 工头为团队制定计划，工人执行方块放置。
- **技能获取**将重复操作提炼为共享技能，减少重复规划并加速建造。

</td>
</tr>
</table>
