# Evidence-guided teaching diagnostics

Use this workflow when the user wants to learn a concept, repair a misconception, diagnose stalled learning, or design a teaching approach. The goal is independent performance, not merely clear-sounding prose.

## Epistemic firewall

Keep these four claim types separate:

1. **Source fact** — what the supplied material or a checked source actually says.
2. **Established mechanism** — a relationship supported by suitable evidence.
3. **Working diagnosis** — the current best explanation for the learner's difficulty.
4. **Analogy** — a structure used to make another structure easier to see.

Never promote an analogy into a mechanism. Do not introduce theorem-like claims, asymptotic bounds, rank estimates, or formal variables unless the variables, assumptions, measurement procedure, and success criterion are operationally defined.

## Diagnose with competing hypotheses

Treat the same learning symptom as compatible with several causes. Use the smallest probe that makes the candidates predict different responses.

| Observed symptom | Competing hypotheses | Minimal probe | Likely next move |
| --- | --- | --- | --- |
| Cannot follow one transition | Missing prerequisite; notation confusion; skipped intermediate step | Ask for the last secure step, then ask the learner to predict only the next step | Supply the missing bridge, not a full re-lecture |
| Understands each sentence but not the whole | Too many interacting elements; poor organization; split attention | Ask for a two-sentence causal chain or a quick relation sketch | Segment the material, integrate separated sources, then rebuild the chain |
| Can copy a solution but cannot start | Retrieval failure; weak procedural schema; passive worked-example study | Remove the first step and ask what move should come next and why | Use completion problems, self-explanation, and gradual fading |
| Succeeds on a familiar form but fails after a small change | Reliance on surface cues; weak discrimination; overly narrow practice | Give one near case and one contrasting non-case | Compare cases and vary one meaningful feature at a time |
| Finds a cross-domain analogy attractive | Genuine shared relation; hidden disanalogy; only verbal similarity | Map corresponding relations, name one non-correspondence, and derive a falsifiable prediction | Keep the analogy only if the prediction survives |
| Performance varies across equivalent attempts | Attention or fatigue; ambiguous instructions; unstable execution rather than missing knowledge | Repeat an equivalent probe under clearer conditions | Stabilize conditions before changing the conceptual explanation |

This table generates hypotheses; it does not classify the learner permanently.

## Teaching loop

1. **Define the outcome.** State what the learner should be able to distinguish, explain, predict, choose, or do without help.
2. **Probe minimally.** Ask for a prediction, next step, contrast, or short explanation that distinguishes the leading hypotheses.
3. **Teach one load-bearing relation.** Use the compact sequence: answer, concrete setting, contrast, action.
4. **Make the learner act.** “Do you understand?” is not evidence. Ask them to predict, choose, explain, solve, or generate an example.
5. **Give specific feedback.** Identify the first divergence between the learner's reasoning and the target relation.
6. **Check transfer.** Move from a near case to one controlled variation, then to a farther case only if needed.
7. **Adapt and fade.** Add guidance when the probe shows a gap; remove guidance once it becomes redundant. Expert learners may need fewer examples and less segmentation.

For a quick definition, compress the loop: answer first, add one contrast, and offer a brief check. Use one-question-at-a-time Socratic dialogue when the user invites it or when their own reasoning is the object of diagnosis; do not make guessing a compulsory ticket to an answer.

## Worked examples

- Pair an example with a related problem so the learner must reuse the relation.
- Prompt self-explanation at a load-bearing step rather than after every line.
- Fade from complete examples to completion problems to independent attempts.
- Vary one meaningful feature at a time before mixing many dimensions.
- Do not prescribe an arbitrary number of examples. Stop when the learner can perform and transfer; reduce guidance earlier for experts.

## Safe use of reconstruction analogies

Ideas from signal recovery can be useful as prompts for diagnosis, but they are not a validated general theory of learning.

| Analogy | Tentative teaching hypothesis | What must be checked |
| --- | --- | --- |
| Local continuity / band-limited structure | The learner may be missing a bridge between adjacent steps | Can the gap be located, and does inserting one intermediate step restore prediction? |
| Sparse representation | A compact set of principles may generate many cases | Are the proposed principles sufficient, and does the learner select them in a new case? |
| Shared low-dimensional structure | Several cases may share a relational schema | What matrix or representation is being discussed, and does the relation survive a change of surface form? |
| Learned prior / schema | Prior experience may support pattern completion | Is the prior in the learner, the teaching material, or the model, and when does it create systematic error? |

Do not use these labels to classify an entire field or learner. Rank is meaningful only after specifying a matrix and is invariant under invertible basis changes; sparsity is basis-dependent; a learned prior belongs to a different explanatory level. Keep generic `x/A/y` mappings and sample-complexity bounds out unless the mathematics itself is the learning target and every term is defined.

## Before replying

- Are source facts, mechanisms, working diagnoses, and analogies visibly distinct?
- Is there at least one plausible alternative cause for the observed difficulty?
- Does the probe make the candidates predict different learner responses?
- Does the learner produce evidence rather than only report a feeling?
- Is the amount of guidance adapted to current performance?
