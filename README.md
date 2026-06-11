# wassname

I'm just a guy who likes to machine learn. I want the good ending not the bad one.

I work on AI alignment: steering, evals, and practical interpretability.

**Links:** [wassname.org](https://wassname.org) · [Scholar](https://scholar.google.com/citations?user=giqv10cAAAAJ) · [Hugging Face](https://huggingface.co/wassname) · [LessWrong](https://www.lesswrong.com/users/wassname) · [Gists](https://gist.github.com/wassname)

---


## Current focus

- **Weak 2 strong character steering** *(WIP, with Lyptus)*
  Can weight steering provide an interface for a weaker model to align a stronger model's [moral character](https://www.forethought.org/research/the-importance-of-ai-character)? The weaker model modifies the larger model's preferences by interviewing it and creating persona pairs (weight steering, because it beats activation steering by my measures). It can be iterative, can hopefully allow a large gap between weak and strong, and might even scale favourably with model size. It's a work in progress, it's hard to get it working reliably with small models.

  ![weak to strong character steering early results](https://i.imgur.com/RdLmNVf.png)

- **vGROUT** *(WIP, code not yet public)*
  Quarantining reward hacking: can we use a hacking vector to route hacky gradients? We build the hacking vector from synthetic hack/honest pairs (the GRPO gradient update for the LoRA weights), then compare each training sample's gradient with it: high cosine similarity gets routed to a quarantine adapter, and the vast majority of in-between gradients get sorted out by absorption. Preliminary result (still improving robustness): the vectors remove reward hacking much better than vanilla GRPO but reduce solving a bit. This is interesting because it uses synthetic pairs not labels, and relies on internal representations, which could scale well with model capability.
  
<img height="200" alt="image" src="https://github.com/user-attachments/assets/4354817d-fe77-4c5a-8c70-4119b8dfef51" />


Released along the way: [steering-lite](https://github.com/wassname/steering-lite), [lora-lite](https://github.com/wassname/lora-lite), [steer-heal-love](https://github.com/wassname/steer-heal-love), [tinymfv](https://github.com/wassname/tinymfv).

---

## Tools

Ones I use and recommend:

| Repo | What it does |
|------|--------------|
| [steering-lite](https://github.com/wassname/steering-lite) | Hackable forward-hook activation steering; calibrated and tested. |
| [lora-lite](https://github.com/wassname/lora-lite) | Hackable single-file-per-variant LoRA built on forward hooks. Tested on GSM8K. |
| [tinymfv](https://github.com/wassname/tinymfv) | Tiny moral foundations vignettes; fast logprob measure of moral preference change. Still is a reliable and sensitive way to test your adapter or steering in ~10mins, I use this a lot and recommend it. |
| [awesome-interpretability](https://github.com/wassname/awesome-interpretability) | Curated mechinterp + probing + tooling map. |

Early drafts, contributions welcome:

| Repo | What it does |
|------|--------------|
| [ml_debug](https://github.com/wassname/ml_debug) | An attempt to uplift ML research taste in coding agents. Not working yet, but helps a bit. |
| [pseudopy](https://github.com/wassname/pseudopy/blob/main/SKILL.md) | A unicode+python type of pseudocode. |

## Alignment research

- **[AntiPaSTO](https://github.com/wassname/AntiPaSTO)** 
  Self-supervised steering of moral reasoning. Gradient-based optimization in SVD space; beats prompting on OOD transfer; robust when steering against safety training. **[arXiv:2601.07473](https://arxiv.org/abs/2601.07473)** · [LessWrong](https://www.lesswrong.com/posts/nWiwv4GN8aYqpnZKE/antipasto-self-supervised-value-steering-for-debugging)
- **[S-space steering for eval-awareness control](https://github.com/wassname/ssteer-eval-aware)**
  Replicated eval-awareness paper with novel S-space (singular value basis) steering; Hawthorne gap 1% vs prior work's 26% on Qwen3-32B. Apart Research Control hackathon 2026.

  <img height="200" alt="eval-awareness steering results" src="https://github.com/user-attachments/assets/851a8083-f873-4615-bcd4-8edb86e195d1" />

## Evals & datasets

| Repo | What it does |
|------|--------------|
| [open_pref_eval](https://github.com/wassname/open_pref_eval) | Judge-free preference eval via logprobs. Converts Machiavelli, ETHICS, GENIES to fast logprob evals. |
| [llm_ethics_leaderboard](https://github.com/wassname/llm_ethics_leaderboard) | Moral preference leaderboard; logprob rankings + permutation debiasing. [Results site](https://wassname.github.io/llm_morality/) |

More datasets on [Hugging Face](https://huggingface.co/wassname).

## Experiments

Replications, exploratory work, and negative results that informed the work above.

| Repo | What it does |
|------|--------------|
| [steer-heal-love](https://github.com/wassname/steer-heal-love) | Can we make steering coherent over many iterations? Yes, with an RMSE-KL coherence constraint. Follow Gemma-3-4b's journey of discovery with Lex Fridman ;p |
| [isokl_steering_calibration](https://github.com/wassname/isokl_steering_calibration) | Experiment towards cheaply calibrating intervention strength for LoRA and steering; works, but I'm searching for a more elegant method. <br><img src="https://raw.githubusercontent.com/wassname/isokl_steering_calibration/main/figs/zoom_in.png" width="400" alt="iso-KL calibration plot"> |
| [Unsupervised-Elicitation](https://github.com/wassname/Unsupervised-Elicitation) | Replicated Anthropic's ICM paper; model self-reports labeling heuristics on TruthfulQA without supervision. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=g7ZnMh4ccs8xwdxX6) |
| [coconut](https://github.com/wassname/coconut) | Replicated Facebook's COCONUT + added SEQ-VCR loss. Found training is very slow (not emphasised by authors). WIP branch: [adapter recursion in SVD space](https://github.com/wassname/coconut/tree/adapter_recurse4_simpler). |
| [How to steer thinking models](https://github.com/wassname/llm-moral-foundations2/blob/main/nbs/10_how_to_steer_thinking_models.ipynb) | RepEng fork that works on reasoning models. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=j8dxxEGz7SsDigQPn) |
| [eliciting_suppressed_knowledge](https://github.com/wassname/eliciting_suppressed_knowledge) | Probes on suppressed activations beat output logprobs on TruthfulQA. Shows linear probes have limits, motivating gradient-based methods. |
| [repr-preference-optimization](https://github.com/wassname/repr-preference-optimization) | Early attempt at hidden-state preference optimization. Superseded by AntiPaSTO. |
| [LoRA_are_lie_detectors](https://github.com/wassname/LoRA_are_lie_detectors) | Adapters as end-to-end probes. Promising direction, inconclusive results. |
| [adapters_can_monitor_lies](https://github.com/wassname/adapters_can_monitor_lies) | Adapter-based honesty monitoring (Short Circuit-inspired). Paused. |

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
