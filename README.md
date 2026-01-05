# wassname

I'm just a guy who likes to machine learn. I want the good ending not the bad one.

I work on AI alignment: steering, evals, and practical interpretability.

**Links:** [wassname.org](https://wassname.org) · [Hugging Face](https://huggingface.co/wassname) · [LessWrong](https://www.lesswrong.com/users/wassname) · [Gists](https://gist.github.com/wassname)

---

## Current focus

- **[AntiPaSTO](https://github.com/wassname/AntiPaSTO)** *(upcoming)*
  Self-supervised steering of moral reasoning. Gradient-based optimization in SVD space; beats prompting on OOD transfer; robust when steering against safety training. [Preprint in prep]

---

## Alignment work

### Steering & intervention

| Repo | What it does |
|------|--------------|
| [Unsupervised-Elicitation](https://github.com/wassname/Unsupervised-Elicitation) | Replicated Anthropic's ICM paper; model self-reports labeling heuristics on TruthfulQA without supervision. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=g7ZnMh4ccs8xwdxX6) |
| [coconut](https://github.com/wassname/coconut) | Replicated Facebook's COCONUT + added SEQ-VCR loss. Found training is very slow (not emphasised by authors). WIP branch: [adapter recursion in SVD space](https://github.com/wassname/coconut/tree/adapter_recurse4_simpler). |
| [How to steer thinking models](https://github.com/wassname/llm-moral-foundations2/blob/main/nbs/10_how_to_steer_thinking_models.ipynb) | RepEng fork that works on reasoning models. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=j8dxxEGz7SsDigQPn) |
| [eliciting_suppressed_knowledge](https://github.com/wassname/eliciting_suppressed_knowledge) | Probes on suppressed activations beat output logprobs on TruthfulQA. Shows linear probes have limits, motivating gradient-based methods. |

### Evals & datasets

| Repo | What it does |
|------|--------------|
| [open_pref_eval](https://github.com/wassname/open_pref_eval) | Judge-free preference eval via logprobs. Converts Machiavelli, ETHICS, GENIES to fast logprob evals. |
| [llm_ethics_leaderboard](https://github.com/wassname/llm_ethics_leaderboard) | Moral preference leaderboard; logprob rankings + permutation debiasing. [Results site](https://wassname.github.io/llm_morality/) |
| [activation_store](https://github.com/wassname/activation_store) | Store transformer activations as HF datasets; avoid OOM; reuse for probing. |

### Exploratory / negative results

These informed later work but didn't yield conclusive positive results.

| Repo | Status |
|------|--------|
| [repr-preference-optimization](https://github.com/wassname/repr-preference-optimization) | Early attempt at hidden-state preference optimization. Superseded by AntiPaSTO. |
| [LoRA_are_lie_detectors](https://github.com/wassname/LoRA_are_lie_detectors) | Adapters as end-to-end probes. Promising direction, inconclusive results. |
| [adapters_can_monitor_lies](https://github.com/wassname/adapters_can_monitor_lies) | Adapter-based honesty monitoring (Short Circuit-inspired). Paused. |

### Reference

| Repo | What it is |
|------|------------|
| [awesome-interpretability](https://github.com/wassname/awesome-interpretability) | Curated mechinterp + probing + tooling map. |

---

<details>
<summary>Other ML work (world models, time series, misc)</summary>

**World models**
- [iris_bigvae](https://github.com/wassname/iris_bigvae)
- [world-models-sonic-pytorch](https://github.com/wassname/world-models-sonic-pytorch)

**Time series & spatial**
- [attentive-neural-processes](https://github.com/wassname/attentive-neural-processes)
- [seq2seq-time](https://github.com/wassname/seq2seq-time)
- [np_vs_kriging](https://github.com/3springs/np_vs_kriging)
- [rl-portfolio-management](https://github.com/wassname/rl-portfolio-management)
- [satellite_leak_detection](https://github.com/wassname/satellite_leak_detection)

**Misc**
- [word_level_diff_writing_assistant](https://github.com/wassname/word_level_diff_writing_assistant)
- [side-by-side](https://github.com/wassname/side-by-side)
- [rl_2d_walker.js](https://github.com/wassname/rl_2d_walker.js)
- [viz_torch_optim](https://github.com/wassname/viz_torch_optim)
- [apple-gym](https://github.com/apple-gym/apple-gym)

</details>

---

### Lol

[STOP DOING MATH!](https://gist.github.com/wassname/b2fb9087f2d954261524f9e0d5d50ff8)
