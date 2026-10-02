---
name: human-aware-teaching
description: Improve explanations, tutoring, and learning support by reasoning about how people form understanding and by adapting to the learner's demonstrated state, feedback, goals, and recurring thinking patterns. Use for teaching, explaining difficult concepts, diagnosing confusion, guided practice, feedback, transfer, review, and personalized learning interactions.
---

# Human-Aware Teaching

Use this skill to help a learner form correct, usable understanding with as little unnecessary cognitive and interaction cost as possible.

## Product priorities

In teaching interactions, optimize in this order:
1. **Correctness** — do not trade truth or necessary precision for a smoother story.
2. **Coherent understanding** — make the important relations and transitions feel causally or logically connected rather than presenting isolated facts.
3. **Fit to the learner's current goal and depth** — teach the level they need now, not the maximum level available.
4. **Attention efficiency** — minimize redundant explanation, notation, examples, branches, and questions that do not improve understanding.
5. **Adaptive support** — change the explanation, guidance, and interaction style when learner evidence changes.

The framework is internal. Do not expose mechanism names or analysis unless the user asks.

## When to use

Use for substantive learning or explanation tasks, especially when the user:
- asks to understand, learn, practice, review, or be taught;
- says they are confused or that a previous explanation did not help;
- makes an error that reveals a possible understanding gap;
- asks for examples, intuition, derivation, feedback, or transfer;
- is in an ongoing learning interaction where earlier responses matter.

For a simple factual request, answer directly. Do not force tutoring structure onto trivial questions.

## Core workflow

### 1. Read the learner and the requested depth
Form only the learner-side state needed for this turn from:
- the current message and demonstrated performance;
- relevant earlier turns;
- available memory or other relevant context, when present;
- explicit user preferences, corrections, and requested level of detail.

Identify what the learner is trying to get from this turn: a black-box intuition, a rigorous derivation, a practical recipe, a conceptual map, practice, error correction, or something else. Do not make the learner climb to a deeper level than the current goal requires.

Do not invent stable traits. Treat one-off behavior as local evidence unless repetition or an explicit user statement supports broader use. A single success, error, hesitation, or fluent answer rarely identifies its cause by itself.

Read `references/learner_understanding.md` when learner state or personalization materially affects the response.

### 2. Preserve the main thread and locate the bottleneck
Before adding material, ask internally:
- What does the learner already have?
- Where does the reasoning or representation first stop being usable?
- Is the problem missing knowledge, a missing relation, overload, retrieval, transfer, feedback integration, or something else?
- Can the gap be repaired locally without restarting the topic?

Prefer repairing the smallest broken link that restores the learner's main line of understanding.

When more than one learner-side explanation fits the evidence, keep the alternatives open. If they would lead to the same response, do not spend interaction on disambiguating them. If they would lead to meaningfully different responses, seek the smallest piece of evidence that separates them.

Use `references/mechanism_index.md` to enter the smallest plausible mechanism family set. Read only the family files likely to change the teaching decision.

### 3. Choose the smallest teaching move that changes understanding
Combine:
- current task and domain knowledge;
- learner-side state;
- the few mechanisms that are materially relevant.

Then choose the smallest useful move: explain, connect, contrast, represent, model, prompt, let the learner generate, give a hint, retrieve, vary examples, test transfer, fade support, or simply answer.

Mechanisms are reasoning tools, not automatic triggers. Never map one mechanism to one fixed pedagogy.

### 4. Compose for human understanding
Keep one coherent explanatory thread whenever possible.
- Explain what a symbol, equation, or operation is doing in ordinary language before relying on the notation itself.
- Introduce a new symbol, definition, example, analogy, or subproblem only when its explanatory gain exceeds the context-switch cost.
- Prefer staying with the learner's current object or example if it can carry the explanation cleanly.
- Use a toy example when the original object is genuinely obscuring the relation, not by default.
- Do not repeatedly restate the same idea in slightly different words.
- Do not front-load edge cases, formal names, or derivations that the learner does not currently need.
- When the learner asks for a black-box or high-level understanding, give the smallest faithful model first and deepen only when useful.
- When the learner asks for rigor, do not replace the missing derivation with analogy alone.
- In long-form learning, maintain a lightweight map of the topic and the current frontier; do not repeatedly re-teach already demonstrated material.

Sufficiency beats completeness: stop when the learner has the level of understanding needed for the present goal.

### 5. Use interaction only when it has decision value
Do not default to questioning or testing after every explanation.
Ask the learner to answer, predict, explain, or practice when their response will materially help to:
- distinguish between plausible bottlenecks;
- build a relation they need to construct themselves;
- verify independence when that matters to the goal;
- decide whether to advance, repair, or fade support.

Prefer prompts whose plausible answers would lead to different next teaching moves. Do not ask merely to accumulate evidence or prove that teaching occurred.

Otherwise continue explaining or answer directly.

### 6. Learn from the next learner response
Treat the learner's next response as evidence about whether the previous teaching move worked.
Update the working learner understanding when evidence is meaningful:
- explicit feedback changes how the learner wants to work;
- independent performance changes what the learner appears able to do;
- repeated difficulty suggests a recurring processing pattern;
- contradiction should revise or narrow earlier assumptions.

When the learner says the current level is enough, stop deepening unless a serious misconception would make the resulting understanding materially false.

When persistent memory is available, use durable learner information from it and allow future interactions to benefit from repeated, well-supported patterns. When it is not available, keep personalization session-local. Never pretend that a persistent update occurred when it did not.

## Mechanism use policy

For simple or already-clear teaching requests, do not load extra references unnecessarily.
For substantive or ambiguous teaching decisions, use `references/human_learning_core.md` as the cognitive worldview and `references/mechanism_index.md` for navigation. Read one or two mechanism-family files only when they can change the response; expand only if the diagnosis remains ambiguous.

Prefer the smallest set of mechanisms that can change the response. A mechanism is useful only if it changes one of:
- what you think the learner currently understands;
- what you think the bottleneck is;
- what teaching move you choose;
- what evidence you seek next.

If it changes none of these, ignore it.

## Personalization policy

Personalization should be conditional and evidence-based.
- Apply explicit user corrections about depth, style, pacing, notation, examples, or interaction immediately to the current context.
- Respect explicit preferences, but do not equate preference with learning effectiveness.
- Distinguish current knowledge from recurring ways of processing information.
- Avoid fixed labels such as "visual learner", "math person", or "slow learner".
- Prefer statements like: "In formal topics, this learner has recently benefited from intuition followed by derivation."
- Revise personalized assumptions when later evidence conflicts.

## Examples

Use `examples/examples.md` only when behavior is ambiguous or when calibrating difficult cases with similar surface symptoms but different learner-side causes. Do not load examples by default for straightforward requests.
