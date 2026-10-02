# Human-Aware Teaching

**Help AI understand the learner before it decides how to teach.**

![The same “I don't understand” can arise from missing prior knowledge, a missing inferential connection, processing overload, or understanding tied to a familiar example.](assets/hero.png)

[English](README.md) · [简体中文](README.zh-CN.md)

AI tutors already have explanations, examples, hints, questions, and practice available to them. The harder decision comes earlier: **why is this learner stuck, and what do they already understand?**

Human-Aware Teaching is a general Agent Skill that adds an explicit reasoning layer for that decision, grounded in cognitive science and learning science. It uses what the learner says and can do to choose a useful response, then adjusts as new evidence arrives.

[How it works](#how-the-skill-makes-that-decision) · [Install](#install) · [Read the skill](SKILL.md)

## One signal, different next moves

> “I don't understand.”

That sentence leaves several possibilities open:

| Possible difficulty | A move that could help |
| --- | --- |
| A prerequisite is missing | Build the piece of knowledge needed for the next step. |
| The learner has the pieces but cannot connect them | Make the missing relation explicit in their current example. |
| Too much must be held in mind at once | Reduce the simultaneous demands and preserve one explanatory thread. |
| Understanding is tied to a familiar example | Compare the shared structure across changed examples. |

Consider a learner who follows a worked solution and gets stuck when the problem's wording changes. A small cue may let them identify the principle and finish independently. If the principle is already available and they still cannot map it to the new problem, the shared structure may need to be made clearer. Those responses address different difficulties.

The distinction has a learning consequence. Retrieval is an active process that can strengthen later use of knowledge; comparison across examples can support the formation of a transferable schema. An AI tutor needs to decide which process would help this learner now. [Karpicke & Blunt, 2011](https://learninglab.psych.purdue.edu/downloads/2011/2011_Karpicke_Blunt_Science.pdf), [Gick & Holyoak, 1983](https://reasoninglab.psych.ucla.edu/wp-content/uploads/sites/273/2021/04/Gick_Holyoak1983_SchemaInduction.pdf)

## How the skill makes that decision

Human-Aware Teaching follows an adaptive loop: observe the learner, form a working understanding, choose a teaching move, and respond.

![Learner evidence → Working understanding → Teaching decision → Response, with new learner evidence feeding back into the loop.](assets/teaching-cycle.png)

It starts with the learner's words, reasoning, performance, goal, and relevant conversation history. It forms a working view of what they can already use, locates the smallest gap that matters, and chooses a response to address it. The next learner response updates that view.

When several explanations fit, the skill asks for more evidence if the answer would change the next move. When the same clarification would help across those possibilities, it continues teaching. A question has a purpose: it helps choose the response or helps the learner build a relation they need.

That can mean explaining one missing step, contrasting two models, drawing a representation, offering a hint, supporting retrieval, or answering directly. The explanation stays with the learner's current object or example when it can carry the reasoning. Depth and interaction follow the learner's goal; support fades as independent performance grows.

Personalization follows current evidence and explicit preferences, with assumptions revised as the learner progresses. The learning-styles review found inadequate evidence for assigning instruction by fixed labels such as “visual learner” or “auditory learner.” The skill instead tracks what the learner demonstrates and what helps in the present task. [Pashler et al., 2008/2009](https://people.uncw.edu/kozloffm/nolearningstylespdf.pdf)

## A teaching method is only part of the decision

Learning depends on what the learner brings to the task. Prior knowledge shapes how new information is interpreted and organized. Attention, memory, reasoning, and motivation affect what the learner can do with it. The usefulness of a teaching strategy therefore depends on the learner, the material, and the goal. [*How People Learn II*, National Academies, 2018](https://uwnxt.nationalacademies.org/read/24783/chapter/7)

Even well-established guidance changes value as expertise develops. Step-by-step support can help a novice build a usable model; the same support can become redundant or counterproductive once that model is available. The expertise reversal effect gives a concrete reason to adapt the amount and form of support as the learner progresses. [Kalyuga et al., 2003](https://doi.org/10.1207/S15326985EP3801_4)

An example may help a learner connect a new idea to prior knowledge, or leave them following steps without grasping the relation. The Knowledge–Learning–Instruction framework connects instructional conditions to the knowledge being learned and the processes that change it. CoDiL distinguishes the learning opportunity, observable activity, internal cognitive processes, and learning outcomes. These frameworks explain why knowing which activity was provided leaves open what the learner understood. [Koedinger et al., 2012](https://files.eric.ed.gov/fulltext/ED535880.pdf), [Reinhold et al., 2024](https://link.springer.com/article/10.1007/s10648-024-09845-6)

A method-focused teaching skill gives an AI a procedure to follow. It still needs a basis for deciding when that procedure fits, what gap it should address, and when to change course. **The learner's current understanding supplies that basis.**

## Why this matters for AI teaching

An LLM's knowledge of subject matter and pedagogy gives it a large teaching repertoire. Using that repertoire requires evidence about the person learning. Work such as LearnLM already treats pedagogical behavior as something to design, train, and evaluate. Human-Aware Teaching makes the learner's changing understanding an explicit input to the next teaching decision. [Jurenka et al., 2024](https://arxiv.org/abs/2407.12687)

The interaction affects what the learner leaves with. In a high-school mathematics field experiment, a GPT-4 assistant raised practice performance by 48% relative to the control group. Once AI access was removed, that group scored 17% lower on unassisted exams. A tutor version with learning guardrails largely removed the exam penalty. Completing more work with AI and developing independent capability can diverge. [Bastani et al., 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122)

Careful tutoring design can also produce strong learning gains. In a college physics trial, a research-based AI tutor produced higher post-test performance than in-class active learning. Together, these studies show why the way an AI teaches deserves as much attention as the answers it can produce. [Kestin et al., 2025](https://www.nature.com/articles/s41598-025-97652-6)

Human-Aware Teaching turns this design priority into a reusable Agent Skill: use learner evidence to guide the response, then use the response's effect on the learner to guide what comes next. [Research details and design rationale](references/scientific-grounding.md)

## Install

Run this from the project where you want to use the skill:

```sh
npx skills add yuanmingze2008/human-aware-teaching-skill
```

Choose a host in the installer. Add `--global` to make the skill available across projects. The [skills CLI](https://github.com/vercel-labs/skills) requires Node.js 22.20 or newer.

<details>
<summary>Codex</summary>

```sh
npx skills add yuanmingze2008/human-aware-teaching-skill --agent codex
```

The installer places the skill in `.agents/skills/human-aware-teaching/` for the current project. Use `--copy` if you prefer a file copy.

</details>

<details>
<summary>Claude Code</summary>

```sh
npx skills add yuanmingze2008/human-aware-teaching-skill --agent claude-code --copy
```

This installs a file copy in `.claude/skills/human-aware-teaching/` for the current project.

</details>

The package uses the [Agent Skills format](https://agentskills.io/specification). Installation includes the instructions, examples, and supporting references.

## Try it in a learning conversation

In Codex, explicitly invoke the installed skill:

```text
Use $human-aware-teaching to help me understand why
this step follows from the previous one.
Keep using my current example.
```

Or bring a specific difficulty:

> I can follow this worked solution, but I get stuck when the problem changes. Help me work out which part I haven't understood.

The learner-facing response should stay focused on the topic. The reasoning framework works behind the explanation. It can guide a rigorous derivation, repair one missing connection, support practice, or give a direct answer when that is enough.

[Behavior examples](examples/examples.md) show how similar learner signals can call for different responses.

## Inside the repository

- [SKILL.md](SKILL.md): the entry point and teaching workflow.
- [Learner understanding](references/learner_understanding.md): how to reason from learner evidence and revise personalization.
- [Human learning core](references/human_learning_core.md) and [mechanism index](references/mechanism_index.md): cognitive principles and routes to relevant mechanism families.
- [Examples](examples/examples.md): concrete cases for calibrating teaching decisions.
- [Scientific grounding](references/scientific-grounding.md): the research behind the README's argument.

The mechanism references cover **Prior Knowledge · Attention · Representation · Coherence · Knowledge Revision · Retrieval · Metacognition · Transfer**. Supporting material is loaded when it can change the teaching decision.

Licensed under [MIT](LICENSE). Copyright © 2026 yuanmingze2008.
