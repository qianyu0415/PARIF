<h1 align="center" style="margin-top: 10px;">PARIF: Pushing the Pareto Frontier of Instruction Following and Reasoning with Curriculum Reinforcement Learning</h1>

<p align="center">
  Rongchuan Mu<sup>1*</sup>,
  Zexin Wang<sup>1*</sup>,
  Qianyu Wang<sup>1*</sup>,
  Minghua Ma<sup>1</sup>,
  Zekun Wang<sup>1</sup>,
  Ming Liu<sup>1,2</sup>,
  Bing Qin<sup>1,2</sup>
  <br>
  <sup>1</sup>Harbin Institute of Technology, Harbin, China &nbsp;&nbsp;
  <sup>2</sup>Pengcheng Laboratory, Shenzhen, China
  <br>
  <sup>*</sup>Equal contribution.
</p>

<div align="center"> 

[![Paper](https://img.shields.io/badge/Paper-arXiv-b5212f.svg?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2509.21240)
[![Paper](https://img.shields.io/badge/Paper-Hugging%20Face-yellow?style=flat-square&logo=huggingface)](https://huggingface.co/parif2026)

</div>

## 🔥 News

* **[2026.04]** Our paper is accepted by **ACL 2026 Main Conference**!
* **[2026.04]** We release our models on Hugging Face.

---

## 💡 Overview

[cite_start]PARIF is a two-stage curriculum reinforcement learning framework designed to push the Pareto frontier of instruction following and general reasoning[cite: 7]. [cite_start]As illustrated in our framework pipeline, the workflow consists of three main components[cite: 122]:

* [cite_start]**Data Construction:** We synthesize a high-quality dataset by integrating constraints into seed and math questions using adaptive filling and random insertion strategies, accompanied by corresponding automated validators[cite: 122, 123].
* [cite_start]**RL Stage I:** Focuses on optimizing the model's reasoning paradigm[cite: 134]. [cite_start]It employs **Dynamic Constraint Weighting** to overcome optimization bottlenecks and introduces a **Correctness Proxy** (evaluating linguistic fluency and logical correctness) to mitigate reward hacking[cite: 94, 95, 124].
* [cite_start]**RL Stage II:** Builds upon Stage I to enhance the logical consistency between the reasoning process and the final answers[cite: 125, 134]. [cite_start]By calculating a **Consistency Score**, this stage enables the decoupled optimization of both components via our Decoupled-GRPO algorithm[cite: 120, 125].

---

## 🚀 Quick Start

*(Installation and usage instructions will be updated soon.)*

---

## 📊 Main Results

### 1. Instruction Following Benchmarks
[cite_start]Our models consistently achieve state-of-the-art (SOTA) performance across multiple IF benchmarks[cite: 59].

| Model | IFEval | FollowBench | IFBench | InfoBench | CFBench | Multi-IF | **Avg.** |
|-------|--------|-------------|---------|-----------|---------|----------|----------|
| **7B Reasoning Models** | | | | | | | |
| R1-Distill-Qwen-7B | 57.99 | 43.82 | 10.88 | 75.73 | 59.91 | 46.27 | 48.09 |
| + VerIF | 71.93 | 50.77 | 23.81 | 79.64 | 73.93 | 60.25 | 57.81 |
| **PARIF-Stage II** | **70.70** | **51.20** | **24.49** | **79.88** | **73.68** | **60.83** | **58.31 (+21.25%)** |
| **8B Reasoning Models** | | | | | | | |
| Qwen3-8B | 83.73 | 62.04 | 31.01 | 85.82 | 87.33 | 79.66 | 70.71 |
| + LightIF | 89.41 | 64.04 | 40.14 | 85.56 | 89.82 | 83.47 | 73.63 |
| **PARIF-Stage II** | **89.78** | **66.06** | **39.12** | **86.69** | **90.50** | **83.55** | **74.58 (+5.47%)** |

[cite_start]*Our models exhibit strong generalization, outperforming base models even on out-of-distribution benchmarks like CFBench and Multi-IF[cite: 260, 261].*

### 2. General Reasoning Capabilities
[cite_start]Stage II recovers and enhances the complex reasoning performance that is temporarily impacted by Stage I's strict focus on IF constraints[cite: 263, 264]. 

| Model | MATH-500 | AIME24 | AIME25 | MMLU-Pro | WritingBench | LiveCode | **Avg.** |
|-------|----------|--------|--------|----------|---------|----------|----------|
| Qwen3-8B | 96.80 | 74.32 | 67.29 | 73.15 | 7.50 | 51.38 | 72.99 |
| **PARIF-Stage II** | **97.20** | **74.50** | **65.13** | **73.20** | **7.80** | **56.81** | **74.14** |

---

## 🔬 Key Analysis & Ablation Studies

### The Necessity of Stage I Curriculum
[cite_start]Bypassing Stage I and training directly with Stage II leads to significant performance degradation in IF tasks[cite: 270]. [cite_start]This proves that the logical consistency optimized in Stage II relies fundamentally on the "reasoning paradigm" established during Stage I[cite: 303].

| Method | FollowBench | IFBench | AIME24 | LiveCode | **Avg.** |
|--------|-------------|---------|--------|----------|----------|
| Directly-Stage II | 64.98 | 33.33 | **75.63** | 53.61 | 56.89 |
| **PARIF (Full)** | **69.16** | **39.12** | 74.50 | **56.81** | **59.91** |

### Decoupled-GRPO vs. Traditional Outcome-based GRPO
[cite_start]By utilizing the consistency score as a dynamic coefficient for reward distribution, our Decoupled-GRPO approach outperforms traditional GRPO that relies strictly on outcome rewards[cite: 201, 343].

| Method | FollowBench | IFBench | AIME24 | LiveCode | **Avg.** |
|--------|-------------|---------|--------|----------|----------|
| Outcome GRPO | 67.87 | **40.48** | 71.25 | 54.76 | 56.36 |
| **Decoupled GRPO** | **69.16** | 39.12 | **74.50** | **56.81** | **59.91** |

### Mitigating Overconfidence
[cite_start]Despite enhancing consistency, PARIF does not exacerbate LRM overconfidence[cite: 356, 358]. [cite_start]External output rewards prevent the model from inflating consistency scores artificially, maintaining a healthy confidence distribution[cite: 358].

---

## 📚 Citation

[cite_start]If you find our work helpful, please cite our paper[cite: 13]:

```bibtex
@inproceedings{mu2026parif,
  title={PARIF: Pushing the Pareto Frontier of Instruction Following and Reasoning with Curriculum Reinforcement Learning},
  author={Mu, Rongchuan and Wang, Zexin and Wang, Qianyu and Ma, Minghua and Wang, Zekun and Liu, Ming and Qin, Bing},
  booktitle={Proceedings of the Annual Meeting of the Association for Computational Linguistics},
  year={2026}
}
