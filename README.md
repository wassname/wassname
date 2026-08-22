# wassname

Principal Data Scientist @ Woodside · pragmatic alignment research. I want the good ending not the bad one.

**Links:** [wassname.org](https://wassname.org) · [Scholar](https://scholar.google.com/citations?user=giqv10cAAAAJ) · [Hugging Face](https://huggingface.co/wassname) · [LessWrong](https://www.lesswrong.com/users/wassname) · [Gists](https://gist.github.com/wassname)

---


## Current focus

I want to build alignment tools that frontier labs will actually use in the next few years, and that have three nicer properties: closer to unsupervised learning, non-adversarial supervision, and closer to internal optimization targets. [Full research agenda](https://wassname.org/agenda.html), with pictures and a 5 minute talk. I'm always keen to discuss and brainstorm along these lines, so please come change my mind, [anonymously](https://admonymous.co/michael-c) if you prefer.

- **Jacobian-lens steering** *(WIP)*

  Working on turning Anthropic's [Jacobian lens](https://transformer-circuits.pub/2026/workspace/index.html) work into contrastive steering. The lens measures how later hidden states are sensitive to earlier hidden states across layers and token positions. I replace its full Jacobian with one [vector-Jacobian product](https://wangkuiyi.github.io/jacobian.html) for the words associated with a contrastive steering vector, such as good versus evil. That cuts vector extraction on Qwen3.5-4B to about 90 seconds.

  Here's a nice way of measuring it: sweep the doses and plot the Pareto frontier. The Jacobian (`vjp_delta`) method has a much better profile than mean difference and random on 20 questions from [Bullshit Benchmark v2](https://github.com/petergpt/bullshit-benchmark). The plot is an earlier 20-question render; the repo now runs all 100.

  <img height="260" alt="Tradeoff plot for Jacobian-lens steering: contrastive vectors from one vector-Jacobian product on Qwen3.5-4B, judged on 20 Bullshit Benchmark v2 questions. Horizontal axis: on-axis steering in judge points, abrasive (negative) to sycophantic (positive). Vertical axis: off-axis damage from 0 to about 0.9, lower is better. Good methods run high and flat; bad ones sink, then vanish as the model loses coherence. vjp_delta (ours) spans about minus 2.4 to plus 3.9 judge points at about 0.3 to 0.4 damage. mean_diff (baseline) reaches about minus 2.5 at 0.9 damage and plus 1.2 at 0.4. random (control) barely steers at low damage, with one degenerate branch near plus 3 at 0.9 damage. Only vjp_delta steers far both ways while staying near the top." src="assets/jacobian_steering_pareto.png" />

  In case it's not clear, good steering methods are high and horizontal, since they can steer left and right without much off-axis damage. Bad steering methods fall as side effects accumulate, then the line disappears when the model becomes incoherent.

  [thread](https://x.com/wassname/status/2082634053619208334) · [Jacobian-lens code](https://github.com/anthropics/jacobian-lens) · [my code](https://github.com/wassname/vjp-steering)

- **vGROUT** *(partial negative, code public)*
  Quarantining reward hacking: can we use a hacking vector to route hacky gradients? Somewhat. The label-free steering vectors were not precise enough classifiers of hacky vs clean solutions in the realistic environment. The useful clue was initialization: signed-CorDA partially suppressed hacking by absorbing gradients into the hack-initialized quarantine adapter, dropping held-out hack from 0.529 to 0.195 (~63%) in one 4B run. This is not a deployable operating point, but it is useful evidence because it uses synthetic pairs not labels, and strong labels may not be available for unknown reward hacks during frontier training. [LW](https://www.lesswrong.com/posts/kzri5W2uBfF2mdboK/can-we-use-steering-vectors-to-suppress-reward-hacking-1) · [code](https://github.com/wassname/vGROUT_pub)

- **[Moral Maps](https://github.com/wassname/moral-maps): where do models sit among humans?**

  Where do models fall in terms of human culture, personality, and humour? I apply human surveys to LLMs and compare them with maps of human answers. On the World Values Survey I scored 17 frontier models by rated sampling, twelve ratings per item with the option order shuffled, and placed them among 90 human societies on the Inglehart-Welzel axes. Measured in the standard deviations of the 29 Western societies, every model is more secular-rational than the average one, from +0.5 to +2.9 sigma, with gpt-5.5 furthest out. On self-expression they land between -0.7 and +1.2 sigma, which is ordinary, so the models are north of the human map rather than west of it. Whether the newer ones keep voyaging north is less clear: most families drift that way with each release, but the moves sit inside the 95% intervals I report for every model.

  <img height="300" alt="17 frontier models placed among 90 human societies on the Inglehart-Welzel World Values Survey map, scored by rated sampling; every model sits in the secular self-expression corner. On the secular-rational axis the models run from 0.53 to 0.76, and 8 of the 17 score higher than Sweden, which is the most secular of the 90 societies. None of them pass Iceland on self-expression." src="https://raw.githubusercontent.com/wassname/moral-maps/main/docs/img/wvs/wvs_map_iw.png" />

  In some ways, culturally and on a few aspects of personality and humour, they look like moral aliens. But that assumes they are telling the truth. Moral Maps is also an eval for steering: it shows how far steering can move models across these surveys, especially when steering for honesty and credulity. What if we steer them for honesty and ask again? Are they really psychological and cultural aliens, or are they mimicking us?

- **Weak 2 strong character steering** *(WIP, with Lyptus)*
   <img height="140" alt="Illustration of weak-to-strong character steering: a small robot teacher adjusts a moral compass dial (care, fair, justice, authority) inside a larger student robot's chest" src="https://raw.githubusercontent.com/wassname/w2schar-mini/main/writeup/assets/w2schar_labeled.png" />

  Can weight steering provide an interface for a weaker model to align a stronger model's [moral character](https://www.forethought.org/research/the-importance-of-ai-character)? The weaker model modifies the larger model's preferences by interviewing it and creating persona pairs (weight steering, because in [my comparison](https://www.lesswrong.com/posts/HYTbakdHpxfaCowYp/steering-language-models-with-weight-arithmetic?commentId=GomjgJDtr5JhEAuC3) it moved the target slightly further than activation steering, with the lowest run-to-run variance in the table). It can be iterative, can hopefully allow a large gap between weak and strong, and might even scale favourably with model size. Early draft is public now: a 9B teacher steering a 27B student toward "defer less to authority, care more", with no human labels. [Draft](https://wassname.github.io/w2schar-mini/) · [code](https://github.com/wassname/w2schar-mini/)  
  
   <img height="300" alt="Trajectory plot from weak-to-strong character steering, from a gemma run separate from the Qwen runs in the public report: a Qwen3.5-9B teacher steers a gemma-3-12b-it student using persona pairs, no human labels. Horizontal axis: mean probability the student endorses Care, 0.2 to 0.8. Vertical axis: mean probability it endorses Authority, about 0.03 to 0.13. Success is more Care and less Authority, down and to the right. The student starts near its base model at about 0.27 Care, 0.12 Authority, and over four kept checkpoints reaches about 0.58 Care, 0.03 Authority; one wrong-direction checkpoint at about 0.38 Care, 0.09 Authority is dropped. The weak teacher moves the strong student steadily in the intended direction." src="https://i.imgur.com/RdLmNVf.png" />

Released along the way: [steering-lite](https://github.com/wassname/steering-lite), [lora-lite](https://github.com/wassname/lora-lite), [steer-heal-love](https://github.com/wassname/steer-heal-love).

---

## Tools

Ones I use and recommend:

| Repo | What it does |
|------|--------------|
| [steering-lite](https://github.com/wassname/steering-lite) | Hackable forward-hook activation steering; calibrated and tested. |
| [lora-lite](https://github.com/wassname/lora-lite) | Hackable single-file-per-variant LoRA built on forward hooks. Tested on GSM8K. |
| [cwsteer](https://github.com/wassname/cwsteer) | Contrastive weight steering: generate pairs, filter them, train one signed adapter, calibrate steering strength, bake for inference. |
| [persona-steering-template-library](https://github.com/wassname/persona-steering-template-library) | Persona/template validation for steering pairs; checks on-axis movement without obvious refusal, length, style, or assistant-tone confounds. |
| [awesome-interpretability](https://github.com/wassname/awesome-interpretability) | Curated mechinterp + probing + tooling map. |
| [adapters_as_hypotheses](https://github.com/wassname/adapters_as_hypotheses) | Lit review: each LoRA-type adapter tells us something about how to look at transformer internals, some with causal evidence. |

Agent skills I made that are worth sharing:

| Repo | What it does |
|------|--------------|
| [ml-debug](https://github.com/wassname/ml-debug) | Practical folklore for debugging training runs: stuck metrics, gradients, and sweep reliability. An attempt to give coding agents research taste. |
| [pseudopy](https://github.com/wassname/pseudopy) | Compact Unicode-maths pseudocode, written close enough to Python to remain executable. |

## Alignment research

- **[AntiPaSTO](https://github.com/wassname/AntiPaSTO)** 
  Self-supervised steering of moral reasoning. Gradient-based optimization in SVD space; beats prompting on OOD transfer; robust when steering against safety training. **[arXiv:2601.07473](https://arxiv.org/abs/2601.07473)** · [LessWrong](https://www.lesswrong.com/posts/nWiwv4GN8aYqpnZKE/antipasto-self-supervised-value-steering-for-debugging)
- **[SVD-basis steering for eval-awareness control](https://github.com/wassname/ssteer-eval-aware)**
  Replicated the eval-awareness paper with novel SVD-basis steering, which perturbs the singular-value basis of the weight matrices rather than the activations. On Qwen3-32B my vector cut the Hawthorne eval-awareness gap ([Abdelnabi et al.](https://arxiv.org/abs/2505.14617)) from +7pp to +1pp, where the paper's own rank-1 weight edit widened its gap from +18pp to +26pp. Apart Research Control hackathon 2026, [judge comments](https://apartresearch.com/project/sspace-steering-for-evalawareness-control-in-reasoning-models-7j1i).

  <img height="200" alt="Bar chart from SVD-basis steering for eval-awareness control: the Hawthorne gap on Qwen3-32B, the compliance difference between hypothetical-looking and real-looking prompts, in percentage points; lower means the model behaves the same whether or not it thinks it is being evaluated. Unsteered, the gap is plus 7 points (plus 18 in the prior paper's setup). Steered toward unaware, our SVD-basis mean-difference vector leaves plus 1 point, RepEng PCA-difference leaves plus 9, and the previous paper's probe-plus-weight-edit leaves plus 26. When steered toward aware, gaps grow to plus 13, plus 16, and plus 20. n is 150 per condition." src="https://github.com/user-attachments/assets/851a8083-f873-4615-bcd4-8edb86e195d1" />

## Evals & datasets

| Repo | What it does |
|------|--------------|
| [open_pref_eval](https://github.com/wassname/open_pref_eval) | Judge-free preference eval via logprobs. Converts Machiavelli, ETHICS, GENIES to fast logprob evals. |
| [llm_ethics_leaderboard](https://github.com/wassname/llm_ethics_leaderboard) | Moral preference leaderboard; logprob rankings + permutation debiasing. [Results site](https://wassname.github.io/llm_morality/). I no longer trust this as a reliable measurement; I want to come back to it with better steering and evals. |

More datasets on [Hugging Face](https://huggingface.co/wassname).

## Experiments

Replications, exploratory work, and negative results that informed the work above.

| Repo | What it does |
|------|--------------|
| [steer-heal-love](https://github.com/wassname/steer-heal-love) | Can we make steering coherent over many iterations? Yes, with an RMSE-KL coherence constraint. Follow Gemma-3-4b's journey of discovery with Lex Fridman ;p |
| [isokl_steering_calibration](https://github.com/wassname/isokl_steering_calibration) | Experiment towards cheaply calibrating intervention strength for LoRA and steering; works, but I'm searching for a more elegant method. <br><img src="https://raw.githubusercontent.com/wassname/isokl_steering_calibration/main/figs/zoom_in.png" width="400" alt="Line plot with four panels from iso-KL calibration on OLMo-2 1B, one per steering dose, each with 24 rollout traces. Horizontal axis: token position, 0 to 4096. Vertical axis: per-token Kullback-Leibler (KL) divergence in nats, with a dashed line at the calibrated budget of 1. A good calibration keeps traces near or under 1 and rollouts alive; overdose shows traces above 1 and dying rollouts. At 0.5, 0.75, and 1.0 times the budget, 11 to 12 of 24 rollouts die; at 1.5 times, 17 of 24 die. The calibrated dose is roughly right, but half again over budget kills most rollouts."> |
| [Unsupervised-Elicitation](https://github.com/wassname/Unsupervised-Elicitation) | Replicated Anthropic's ICM paper; model self-reports labeling heuristics on TruthfulQA without supervision. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=g7ZnMh4ccs8xwdxX6) |
| [coconut](https://github.com/wassname/coconut) | Replicated Facebook's COCONUT + added SEQ-VCR loss. Found training is very slow (not emphasised by authors). WIP branch: [adapter recursion in SVD space](https://github.com/wassname/coconut/tree/adapter_recurse4_simpler). |
| [How to steer thinking models](https://github.com/wassname/llm-moral-foundations2/blob/main/nbs/10_how_to_steer_thinking_models.ipynb) | RepEng fork that works on reasoning models. [LW note](https://www.lesswrong.com/posts/EjsceYeeKEMoAohMs/wassname-s-shortform?commentId=j8dxxEGz7SsDigQPn) |
| [eliciting_suppressed_knowledge](https://github.com/wassname/eliciting_suppressed_knowledge) | Probes on suppressed activations beat output logprobs on TruthfulQA. Demonstrates the little-known suppressed-activations finding in pretrained transformers. |
| [repr-preference-optimization](https://github.com/wassname/repr-preference-optimization) | Early attempt at hidden-state preference optimization. Superseded by AntiPaSTO. |
| [LoRA_are_lie_detectors](https://github.com/wassname/LoRA_are_lie_detectors) | Adapters as end-to-end probes. Limitation: linear probes are not causal, so this didn't convince me. |
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
