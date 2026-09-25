# Autoplay prose

This file is the single source for the player's transcript and timing.
After editing it, run `node tools/build-timeline.mjs` to regenerate `timeline.js`.

## How to fill it in

- One section per deck state. There are 23, in deck order. Do not add, remove or reorder sections.
- The heading reads `## NN · id · m:ss`. The `m:ss` is how long autoplay stays on that state.
  Change the time freely. Leave `NN` and `id` alone, since they bind the prose to the deck.
- Paste the full prose under each heading. Paragraphs are separated by a blank line.
- Optional paragraph cue: start a paragraph with `[m:ss]` to highlight it that many
  seconds into the state. Paragraphs without a cue are spaced evenly across the state.
- `PROSE NEEDED` marks an empty slot. The build script warns about any that remain.

The prose below is final (supplied 2026-09-22; opening stutter note removed at Eric's request 2026-09-23). Only formatting and timing are ours to change.

---

## 01 · opening · 1:43
My background is in social networks and collective behavior. I’m a behavioral scientist and network researcher, and much of my recent work has involved translating those tools into controlled experiments with interacting AI systems. I think of credibility as an evidentiary construct. It is built from multiple kinds of evidence, and what matters depends on the task, the operating conditions, and when and where a system is being used. So I do not think of credibility as a permanent property of a model. The relevant question is what evidence supports relying on this system for this use, under these conditions.

[0:43] One basic lesson from network research is that the components alone do not determine system behavior. The same kinds of components can produce very different collective behavior depending on how they are connected and what passes between them. Once machines interact with other machines, that becomes a credibility problem because evaluating the individual components may no longer be sufficient. The interaction itself can create properties that are not visible when those components are evaluated independently.

[1:13] So the research program I want to show you is organized around two linked questions: What does interaction change, and what evidence does that give us for deciding when reliance on the resulting system is warranted? I’ll first show you the experimental system I use to study those questions, and then a series of studies looking at how structure, communication, failure, model capability, and emergent organization change system behavior and the evidence available for evaluating it.

## 02 · system · 0:38
This is the experimental system I build with, and everything else I’m going to show you happens inside this picture. I’m not particularly wedded to the system as an artifact. I built it to answer research questions, and it is probably more representative of how I approach problems: I build the experimental machinery I need and then use it to interrogate the problem. There are three basic parts: what controls the experiment, what I can vary, and what comes out of the system and how I evaluate it.

## 03 · control · 0:36
The controller is the experimental apparatus, and the experiment itself is specified in code. I can configure conditions, launch models into defined roles, control communication, isolate information, record the complete interaction trace, and repeat conditions across trials. That gives me experimental control, reproducibility, and transparency.

[0:21] The complete trace matters for credibility because I’m not limited to asking whether the final answer was correct. I can inspect how the system got there, where information entered, how it changed, and where dependencies or failures emerged.

## 04 · design · 0:40
Within that apparatus I can vary the task, the evidence agents receive, model composition, network structure, communication rules, and perturbations. These six structures give me a representative communication vocabulary, so the same information can travel through very different paths before it is integrated.

[0:20] And the network still has to earn its complexity against an appropriate single-agent baseline. More agents may create capability, but they can also create dependence, coordination cost, correlated error, and new failure paths. So the basic credibility question is: what changed when we turned a model into a system?

## 05 · evaluation · 0:53
At the system level I can evaluate performance, reliability, robustness, variability, drift, provenance, traceability, and failure behavior using several measurement approaches. None of those is credibility by itself. They are different forms of credibility evidence, and which ones matter depends on the reliance claim, the task, and the operating conditions.

[0:23] The projects I’m about to show you are all active research. They are either under review, in revision, or approaching submission. Taken together, they are also indicative of how I think about programmatic research: build a common experimental infrastructure, then use it to ask a family of related questions whose results can accumulate. After the meeting I’ll send a link to my research site with this talk and a small portfolio of the papers behind it.

## 06 · q-problem-solving · 0:09
The first research question is how task and network structure affect collective problem solving.

## 07 · problem-solving · 0:51
The setup is fairly simple: give a group of agents a problem that no single agent can complete alone, distribute the pieces, and change the structure through which those pieces can be combined. The problem pieces stay the same while the integration paths change.

[0:21] What we found is that architecture mattered substantially on simpler, objectively scored constraint tasks, whereas on more open-ended synthesis tasks the differences were much less clearly resolved. So I would not say that there is a generally best architecture. The effect of structure depends on what the system is being asked to do, which matters for credibility because evidence obtained on one kind of task does not automatically support a broader claim about the architecture itself.

## 08 · q-judgment · 0:10
The next question is when communication improves collective judgment and when it makes the system less reliable.

## 09 · judgment · 1:17
Here I construct a task in which a weak numerical majority points one way while a better-informed minority points the other, so simply counting agents and actually weighting the available evidence imply different answers. I hold the private evidence fixed and change what agents are allowed to communicate. They can transmit the evidence behind their judgment, only the conclusion, or, in the broader design space, both.

[0:29] In the empirical comparison, conclusion-only communication reduced accuracy in two of the three model families we tested, but the failure was not the one I expected. The group did not simply converge on the wrong numerical majority. Instead, terminal beliefs became much more variable, so the system became unreliable rather than uniformly wrong. We then used a targeted intervention that held the evidence fixed while changing the conclusion an agent was exposed to, which showed that the communicated conclusion itself can causally move downstream belief.

[1:03] That means communication is not merely a conduit for existing information. What is transmitted, how often it is encountered, and how dependence forms among agents can change the reliability of the system itself.

## 10 · q-mutation · 0:11
That leads to a different question: what happens to information itself as it moves through a network of machines?

## 11 · mutation · 0:17
Here the important object is the message rather than the final answer. Every transmission or synthesis step creates another opportunity for transformation. Some information survives, some changes, some disappears, and new material can also appear downstream.

## 12 · mutation-process · 0:42
This creates an important distinction for credibility because preserving recognizable facts is not necessarily the same as preserving their evidentiary meaning. A conditional estimate can become an asserted fact, or an unresolved discrepancy can become a reconciled conclusion. The names and numbers may remain recognizable while what they are taken to support changes. Across the architectures we tested, we saw different profiles of drift, divergence, and unsupported content. So provenance is not only a question of identifying where information came from. It may also require understanding what happened to that information as it moved through the system.

## 13 · q-backtrace · 0:16
So far I have assumed that I can observe the production process, but many settings present the inverse problem: we see the artifact at the end and not the process that generated it.

## 14 · backtrace · 0:17
In that setting, the terminal artifact is observed and everything upstream has to be inferred. The question is whether residue in the output tells us anything about the communication structure or transformation history that produced it.

## 15 · backtrace-process · 0:37
Under controlled generating conditions, some of that hidden production structure is recoverable, although imperfectly, and some structures leave much more distinctive traces than others. That matters for credibility because agreement among several AI outputs can look like independent confirmation when it may actually reflect common ancestry, a shared hub, or the same source propagated through several intermediaries. Those outputs can look very similar while providing very different evidence, which means production history itself may matter for how much credibility we assign to apparent agreement.

## 16 · q-perturb · 0:08
Once structure is experimentally manipulable, robustness becomes a natural next question.

## 17 · perturb · 0:28
I can disrupt particular nodes or communication paths and ask whether the system degrades gracefully, reorganizes, or fails.

[0:10] Early results suggest that location matters, not simply the amount of disruption. Failures at structurally important points produce different system responses from comparable losses elsewhere. That turns robustness into a controlled test-and-evaluation problem rather than a general claim about whether a system simply “seems robust.”

## 18 · q-models · 0:08
Model capability is another part of the design space.

## 19 · models · 0:37
By holding tasks, structures, communication rules, and evaluation procedures relatively stable, I can ask how model capability interacts with task and structural position.

[0:12] One pattern I’m beginning to see is that capability and position may interact: a stronger model can matter more when it occupies an integration point than when it sits at the edge of the network. If that holds, component-level evaluation misses part of the system. Keeping the rest of the experimental procedure relatively stable also gives us comparability across model generations.

## 20 · q-selforg · 0:13
I can also stop specifying the network and let structure become an emergent outcome while the task, evidence, models, and communication constraints remain controlled.

## 21 · selforg · 0:17
The early runs suggest that the resulting networks are not arbitrary. Communication tends to concentrate around a smaller number of agents, and early choices about whom to consult can persist and shape what follows.

## 22 · selforg-emerge · 0:22
That matters for credibility because the system may create its own dependencies, bottlenecks, and apparent agreement. The question then becomes not only what structure does to the system, but what structure the system creates for itself and what those endogenous dependencies do to reliability, robustness, and provenance.

## 23 · close · 1:35
The larger question is whether credibility evaluation can become more durable and cumulative as the underlying models continue to change. Models will keep changing, and systems built from them will change as well, so some evaluation criteria may be tightly coupled to particular model generations, capability levels, or operating conditions.

[0:23] A more durable approach to credibility may require evidence at the level of the interacting system, not only the individual model. That evidence might include how information moves through a structure, how dependence forms among components, how failures propagate or are contained, and whether outputs can be traced back to the processes that produced them. If credibility is an evidentiary process, then the empirical question is which of those system-level properties, if any, remain informative across changes in models, tasks, capability levels, and operating conditions.

[0:57] Some may prove sufficiently stable to support reproducible tests, common evaluation criteria, rubrics, benchmarks, or assurance procedures, while others may turn out to be highly contingent. Distinguishing between those possibilities is itself part of the research problem. It may also require research systems that preserve enough experimental control, measurement consistency, provenance, and traceability for evidence to accumulate across studies and model generations.

[1:22] If sufficiently stable regularities exist, they may provide a basis for cumulative credibility evidence about when reliance is warranted, rather than requiring the evaluation problem to be reconstructed around each new model generation.
