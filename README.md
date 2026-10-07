# developmental-epistemics

> **Status:** concept-only research direction.  
> **Horizon:** post-Endophasia / post-Magpie.  
> **License:** [MIT](LICENSE).  
> **No implementation yet.**

## Question

Can epistemic habits become **developmental properties** of a learned system, rather than behaviours added after general capability formation?

The narrow hypothesis is:

> **Holding information and compute fixed, does learning useful epistemic structure earlier change how durable that behaviour is under later optimisation?**

That is different from the simpler claim that epistemic content is useful at all.

## Why ask this?

Several recent results suggest that pretraining and midtraining history can shape later behaviour:

- [Alignment Pretraining](https://arxiv.org/abs/2601.10160) shows that changing alignment-related discourse during pretraining changes downstream behavioural priors.
- [Implicit meta-learning may lead language models to trust more reliable sources](https://arxiv.org/abs/2310.15047) shows that models can learn indicators of source usefulness and later internalise information differently based on them.
- [Metadata Conditioning then Cooldown (MeCo)](https://arxiv.org/abs/2501.01956) shows that source-like metadata can materially affect pretraining efficiency and later behaviour.
- [Midtraining Bridges Pretraining and Posttraining Distributions](https://arxiv.org/abs/2510.14865) finds that timing and mixture weight can interact strongly, consistent with a possible plasticity window.

But the case is far from settled:

- [Constitutional Midtraining](https://arxiv.org/abs/2607.26654) finds that content presence matters much more than curriculum ordering in its setting.
- [Stress-testing Alignment Midtraining](https://arxiv.org/abs/2609.20412) finds that later training can substantially weaken earlier midtraining-induced behaviour.
- [When Does Metadata Conditioning (NOT) Work?](https://arxiv.org/abs/2504.17562) shows that metadata can become a crutch when the relevant latent context is unavailable at evaluation time.

So the interesting question is not whether an "epistemic childhood" sounds appealing.

It is whether **timing contributes anything once content, metadata and later training pressure are controlled**.

### Developmental ordering may itself be measurable

A complementary result concerns **when capabilities emerge**, rather than whether an alignment intervention survives later training.

- Emmy Liu, Kaiser Sun, Millicent Li, Isabelle Lee, Lindia Tjuatja, Jen-tse Huang and Graham Neubig, [*What Do Language Models Learn and When? The Implicit Curriculum Hypothesis*](https://arxiv.org/abs/2604.08510), find a surprisingly stable fixed-threshold emergence ordering across nine models from four families (mean Spearman \(\rho=.81\) across 45 model pairs). Composite tasks usually emerge after their constructed components, and task representations can predict held-out composite learning trajectories (reported \(R^2=.68\)–\(.84\) across models).

This does **not** show that deliberately changing a curriculum causes more durable epistemic behaviour. It does suggest that developmental state can be operationalised at finer resolution than training step or token count alone.

The authors released useful open measurement artifacts:

- [ElementalTask](https://github.com/KaiserWhoLearns/ElementalTask) — task, checkpoint-evaluation and function-vector tooling; [MIT licensed](https://github.com/KaiserWhoLearns/ElementalTask/blob/main/LICENSE).
- [elemental-tasks/model-trajectories](https://huggingface.co/datasets/elemental-tasks/model-trajectories) — public checkpoint-level trajectory data; MIT licensed.

These are best treated as possible **measurement baselines**, not as evidence for the developmental-epistemics hypothesis itself. A later study could ask whether a curriculum policy informed by measured developmental state outperforms matched random, uniform or human-specified curricula while preserving the causal controls above.

## Conceptual design

A future study could use small synthetic microworlds with exact hidden truth and controlled source structure.

### Relational conditions

**E — epistemically informative**

Source identities, shared origins, support, contradiction and reliability relations correspond to the actual microworld.

**N — nonce relational control**

The same metadata structure and token budget are preserved, but the mapping between those relations and world truth is permuted.

**P — plain anchor**

The same underlying facts are presented without persistent relational metadata.

This gives a useful interpretation:

```text
E vs P  → does useful epistemic structure help?
N vs P  → does meaningless structure hurt?
E vs N  → useful relation vs matched relational control
```

### Timing conditions

For E and N:

```text
Early
Uniform
Late
```

All other training conditions should be matched.

A genuinely developmental effect would therefore look like an **epistemic-specific timing effect**, not merely E outperforming N.

## A deliberately risky prediction

One plausible preregistered prediction would be:

```text
Immediate behaviour:
Late ≥ Uniform ≥ Early

Durability under later optimisation:
Early > Uniform > Late
```

Late exposure may have the strongest immediate effect because it is recent.

If early learning changes representation formation in a deeper way, however, it may prove harder to overwrite.

If Late wins both immediately and later, the developmental hypothesis loses.

If timing disappears once controls are matched, the developmental hypothesis loses.

That is a useful result too.

## What "epistemic" means here

The model should not simply be told that uncertainty, provenance or independent evidence are good.

Instead, synthetic worlds should make those behaviours useful:

- multiple reports may share a hidden origin;
- one source may provide genuinely independent evidence;
- a conclusion may depend on which world or context is active;
- evidence may be insufficient;
- later observations may revise earlier support.

The aim is to study whether a model can learn **how to relate to evidence**, not just memorize a vocabulary for talking about epistemology.

## System boundaries

```text
Synthetic microworld
    owns hidden world truth
    owns exact gold outcomes

Magpie
    owns recorded claims
    owns evidence / provenance
    derives policy-scoped standing
    does not establish truth

Endophasia
    owns experiment coordinates
    owns lineage and evidence records
```

Magpie should not become a truth oracle.

For an initial study, it would make more sense as a **shadow measurement surface** than as part of the training objective.

## What would count as an interesting result?

A positive result would be narrow:

> In a controlled synthetic microworld, epistemically informative relational training acquired earlier changed the durability of later behaviour beyond matched metadata and timing controls.

That would **not** establish that developmental training solves alignment.

A null result would also be informative:

- epistemic content helps, but timing does not;
- nonce metadata is actively harmful;
- early advantages disappear under later training;
- effects fail to generalise to a structurally different held-out generator;
- late exposure dominates both immediately and later.

Any of those would narrow the space.

## Relationship to other projects

This is intentionally downstream of:

- [Endophasia](https://github.com/noctem-o/endophasia) — experiment substrate, lineage, observations and reproducibility;
- [Magpie](https://github.com/noctem-o/magpie) — explicit claims, evidence, provenance and policy-scoped standing.

For now, this repository exists only to preserve the research direction.

No training stack. No CI. No speculative framework.

Just the question:

> **Can the way a model learns how to relate to evidence become part of its developmental history — and does that history matter later?**
