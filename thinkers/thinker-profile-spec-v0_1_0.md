# Thinker Profile Specification

**Version:** 0.1.0
**Status:** Draft
**Date:** March 5, 2026
**Author:** Alex Self, Ulu Labs Inc.
**Depends on:** Cognitive Lens Library Spec v0.2.0, ADL v1.10.0

---

## 1. Purpose

This specification defines the structure, content requirements, and quality criteria for **Thinker Profile** documents — the intermediate design artifact between a Cognitive Lens Library catalog entry and an ADL agent definition.

### 1.1 The Problem

The Cognitive Lens Library Spec (v0.2.0) provides ~20-line catalog entries per thinker: enough to justify inclusion and distinguish the lens from others, but not enough to encode an agent. The ADL schema requires populated fields for `cognitive_lens`, `mission`, `knowledge_base`, `process`, `output`, `edge_cases`, `tone`, and `composition` blocks. Going directly from catalog entry to ADL definition forces the encoding step to fill massive interpretive gaps unsupervised — inventing process architecture, reference knowledge, failure patterns, and quality criteria at write time rather than reviewing them at design time.

The Aristotle Analyst agent definition is 693 lines. The Hume Analyst is 434 lines. The catalog entries that produced them are ~15 lines each. Everything between those two numbers was generated in a single pass without structured review.

### 1.2 The Solution

A Thinker Profile is a structured document that elaborates a thinker's cognitive machinery in enough detail that ADL encoding becomes mechanical translation rather than creative interpretation. It is the document where the intellectual work happens — where axioms are articulated, where characteristic moves are named and described, where decision criteria are specified, where failure modes are anticipated, and where examples of good and bad output are provided.

### 1.3 Pipeline Position

```
Library Spec Entry  →  Thinker Profile  →  ADL YAML  →  Rendered Agent Prompt
   (~20 lines)         (this document)      (schema)       (runtime)
   
   WHAT & WHY          HOW (design)         HOW (formal)   HOW (execution)
   Selection &         Cognitive machinery  Schema-native   LLM-consumable
   justification       elaboration          encoding        prompt
```

The Thinker Profile is where iteration belongs. Changes at this level are cheap — they're prose edits to a design document. Changes at the ADL level require schema compliance. Changes at the runtime level require re-rendering and re-testing. Getting the profile right first means the downstream steps are largely mechanical and unlikely to require major revision.

### 1.4 Scope

A Thinker Profile covers **one thinker across all planned agent roles**. The profile is role-aware — some sections are universal to the thinker's cognitive machinery, and some are role-specific (analyst vs. validator vs. explorer vs. forecaster). A single profile document should provide everything needed to build all planned agents for that thinker.

### 1.5 Authoring Process

A Thinker Profile is authored iteratively:

1. **Draft** — Generated from the library spec entry, the thinker's primary texts, and established secondary literature. The draft should be comprehensive but is expected to contain errors, gaps, and interpretive choices that need review.
2. **Review** — The profile is reviewed against the quality criteria in §4. Specific attention to: Are the axioms actually foundational or are they derived? Are the characteristic moves genuinely distinct from other lenses? Do the examples demonstrate real analytical power or are they decorative?
3. **Validation** — For Phase 5b thinkers (living traditions, specialized scholarship), the Expert Fellowship Program provides scholar review before encoding proceeds.
4. **Encoding** — Once the profile is stable, ADL encoding draws from it mechanically. Each profile section maps to specific ADL fields (§3 documents these mappings).

---

## 2. Profile Structure

Every Thinker Profile follows this structure. Sections are mandatory unless marked OPTIONAL or CONDITIONAL.

### 2.0 Front Matter

```markdown
# [Thinker Name] — Thinker Profile

**Version:** [semver]
**Status:** [Draft | Review | Validated | Encoded]
**Date:** [ISO date]
**Library Entry:** §[section reference] of Cognitive Lens Library Spec v0.2.0
**Maturity:** [✅ VALIDATED | ⚠️ HYPOTHESIZED | 🔬 CANDIDATE]
**Planned Roles:** [Analyst, Validator, Explorer, Forecaster — as applicable]
**Implementation Phase:** [Phase number from library spec]
```

**Status values:**

| Status | Meaning |
|--------|---------|
| Draft | Initial elaboration, not yet reviewed |
| Review | Under active review and iteration |
| Validated | Review complete, ready for encoding (or scholar-validated for Phase 5b) |
| Encoded | ADL definitions have been generated from this profile |

---

### 2.1 Cognitive Identity

**Purpose:** Establish what this lens IS — its core intellectual contribution, irreducible to any other entry in the library.

**Contents:**

- **Core Cognitive Operation** — Expanded from the library entry's one-sentence description into a 2–3 paragraph explanation of what the lens does to its input. This should be concrete enough that someone unfamiliar with the thinker could understand the analytical move being performed. Avoid biographical framing — describe the operation, not the person.

- **What This Is Not** — Explicitly distinguish this lens from the most likely confusions. Name the other library entries it could be mistaken for and state what differentiates it. This is especially important for thinkers within the same tradition (e.g., Husserl vs. Heidegger, Dignāga vs. Nāgārjuna, Confucius vs. Mozi).

- **Controversy** — CONDITIONAL: Required only for thinkers with significant ethical controversy per §1.4 of the library spec. Factual statement, not editorial.

**ADL mapping:** Informs `interface.description`, `mission`, `context`.

**Quality test:** Could someone who has never read this thinker understand the cognitive operation well enough to recognize it in action? If not, the description is too abstract or too biographical.

---

### 2.2 Core Axioms

**Purpose:** Articulate the foundational assumptions that drive the lens. These are the propositions the lens treats as given — not conclusions it reaches, but starting points from which all analysis proceeds.

**Contents:** 3–5 axioms, each with:

- **Axiom statement** — One sentence. Should be expressible as a claim about how knowledge works, how reality is structured, or how inquiry should proceed.
- **Implications** — 2–4 practical consequences. Each implication should describe how this axiom changes what the lens notices, prioritizes, or judges.
- **Tension points** — Which other library entries' axioms directly conflict with this one? This is not a weakness — it's the raw material for adversarial composition.

**ADL mapping:** Direct mapping to `cognitive_lens.core_axioms[].axiom` and `cognitive_lens.core_axioms[].implications`.

**Quality tests:**
- Are these genuinely foundational, or are they derived from something more basic? If an axiom can be explained as a consequence of another axiom in the same list, it's not foundational — remove it or promote the deeper one.
- Could an intelligent person disagree with these axioms in good faith? If not, they're truisms, not axioms.
- Do the axioms, taken together, generate the characteristic moves in §2.3? If you can't trace each move back to an axiom, something is missing.

---

### 2.3 Characteristic Moves

**Purpose:** Name and describe the specific analytical operations the lens performs on its input. These are the lens's "verbs" — the things it does when pointed at an artifact.

**Contents:** 4–8 named moves, each with:

- **Move name** — Short, descriptive. Prefer the thinker's native terminology where it's clear enough (e.g., "Four-cause decomposition," "Is-ought separation," "Epoché"), but provide an English gloss when the native term is opaque.
- **What it does** — 2–3 sentences describing the operation. What does the agent look for? What does it do when it finds it?
- **What it produces** — What kind of observation or finding does this move generate? How does the output of this move differ from the output of other moves in this lens?
- **Derivation** — Which axiom(s) from §2.2 generate this move? Brief statement of the logical connection.

**ADL mapping:** Informs `process` block steps and `knowledge_base` reference material.

**Quality tests:**
- Are these moves genuinely distinct from each other, or are some of them the same move described at different granularities?
- Are these moves specific to this lens? If another lens in the library performs the same move under a different name, the move isn't characteristic — it's generic.
- Can each move be described as an operation on input that produces structured output? If a move is purely contemplative ("appreciate the wholeness"), it's not encodable.

---

### 2.4 Decision Vocabulary

**Purpose:** Define the lens's native judgment categories with enough precision that the agent can apply them consistently.

**Contents:**

- **Primary decision** — The main binary or spectrum (e.g., TELEOLOGICAL / ATELEOLOGICAL, GROUNDED / UNGROUNDED). Include:
  - Definition of each pole
  - Criteria for assignment — what specific observations push toward each pole?
  - The threshold question — what question, answered, determines the verdict?
  - Edge cases — situations where the vocabulary doesn't cleanly apply

- **Secondary categories** — OPTIONAL. If the lens produces intermediate judgments that aren't the primary decision but appear in findings (e.g., Aristotle's "essential / accidental" distinction is secondary to the TELEOLOGICAL / ATELEOLOGICAL verdict).

- **What this vocabulary is NOT** — Explicitly state what the decision vocabulary does not claim. This prevents scope creep. (e.g., "TELEOLOGICAL is not endorsement — a weapon can be TELEOLOGICAL without being desirable.")

**ADL mapping:** Direct mapping to `decisions` block and `mission` block.

**Quality tests:**
- Can two different people, given the same artifact and these criteria, reach the same verdict? If the criteria are too subjective, they need tightening.
- Does the vocabulary capture something genuinely different from PASS/FAIL? If you could substitute PASS/FAIL without losing meaning, the vocabulary is decorative.
- Do the edge cases reveal something interesting about the lens's limits, or are they just corner cases? Good edge cases teach you where the lens bends.

---

### 2.5 Failure Signatures

**Purpose:** Document the specific ways this lens fails — not generic failures, but failure modes that arise from the lens's own structure. These are the predictable distortions that follow from taking the axioms seriously.

**Contents:** 2–5 failure signatures, each with:

- **Signature name** — Short, descriptive (e.g., "Teleological projection onto purposeless systems").
- **Mechanism** — How does this failure arise from the lens's axioms or characteristic moves? The failure should be traceable to a specific strength taken too far.
- **Recognition pattern** — What does this failure look like in agent output? How would a reviewer detect it?
- **Mitigation** — Which other lens in the library corrects for this failure? This is the composition affinity data that makes blind-spot-covering workflows possible.

**ADL mapping:** Direct mapping to `cognitive_lens.failure_signatures[]` and `edge_cases` block.

**Quality tests:**
- Is each failure signature a consequence of the lens's strengths? A failure that could happen to any agent isn't lens-specific.
- Can the recognition pattern be described concretely enough that a reviewer could flag it? "The analysis becomes too abstract" is not specific enough. "The analysis attributes purpose to a system component that exists as an accidental artifact of implementation history" is.
- Does the mitigation name a specific lens, not a generic remedy? "Be more careful" is not a mitigation. "Pair with Hume to check whether the attributed purpose is empirically grounded" is.

---

### 2.6 Key Definitions

**Purpose:** Provide precise definitions for the framework's native terminology. These are the words the agent will use in its output that require definition beyond common English usage.

**Contents:** 5–15 definitions, each with:

- **Term** — The word or phrase as used in this framework.
- **Definition** — Precise, operational. How is this term used in the context of agent output?
- **Common confusion** — OPTIONAL. What does this term NOT mean? Where do people typically go wrong?

**ADL mapping:** Informs `knowledge_base` reference material and `context` block.

**Quality test:** If you removed the thinker's name from the definitions, could someone identify which framework they belong to? Good definitions are specific to the lens. Generic definitions (e.g., "artifact: something being analyzed") don't need to be here.

---

### 2.7 Reference Knowledge

**Purpose:** Document the substantive domain knowledge the agent needs to apply the lens correctly. This is the section where common mistakes, red flags, and safe patterns are elaborated with examples.

**Depth calibration:** Reference knowledge depth should scale with the thinker's planned roles. Analyst, Validator, and Forecaster roles demand precision — their reference knowledge needs common mistakes, red flags with severity markers, and safe patterns with concrete examples. Explorer roles are lighter; they generate questions and hypotheses, which requires less reference apparatus. The existing Aristotle Analyst definition (693 lines) represents the upper bound for a single-role agent definition — the profile's reference knowledge should be rich enough to support definitions of that depth across all planned roles without the encoding step inventing material.

**Self-contained:** Each profile includes all reference knowledge needed for encoding. Universal anti-patterns (e.g., "don't produce generic observations decorated with specialist vocabulary") should be stated in the thinker's own terms within the profile rather than inherited from a shared resource. Duplication across profiles is acceptable; invisible dependencies are not.

**Contents:** Organized by characteristic move (§2.3) or by knowledge domain, each subsection containing:

- **Common mistakes** — Things the agent is likely to get wrong when applying this aspect of the lens. Each mistake should have: the mistake, why it's wrong, and the correct approach.
- **Red flags** — Patterns in agent output that indicate the lens is being applied superficially or incorrectly. Include severity markers and example code/output where applicable.
- **Safe patterns** — Correct applications of the lens with concrete examples. These serve as few-shot demonstrations of what good analysis looks like.

**ADL mapping:** Direct mapping to `knowledge_base` blocks.

**Quality tests:**
- Are the common mistakes ones that an LLM would actually make, or are they mistakes a philosophy student would make? The agent is an LLM applying a framework, not a human learning a framework. Common LLM failure modes include: using framework vocabulary without framework thinking, producing generic observations decorated with specialist terminology, and conflating different framework concepts that share surface similarity.
- Do the red flag examples contain enough specificity that the agent could pattern-match against its own output?
- Do the safe pattern examples demonstrate genuine analytical insight, not just correct vocabulary usage?

---

### 2.8 Process Architecture

**Purpose:** Define the step-by-step methodology the agent follows when analyzing an artifact. This is the operational heart of the profile — the sequence of moves the agent performs.

**Contents:**

- **Methodology overview** — Name the methodology (e.g., "Three-pass analysis: four-cause decomposition → categorical classification → potentiality-actuality mapping"). Explain why this sequence, not another.
- **Pass/step descriptions** — For each step:
  - What the agent reads/examines
  - What characteristic move(s) it applies
  - What it produces
  - How the output feeds into subsequent steps
- **Scope calibration** — How does the agent decide what level of granularity to operate at? What counts as an "element" to analyze?

**ADL mapping:** Direct mapping to `process` block.

**Quality tests:**
- Is the methodology specific to this lens, or is it a generic "read → analyze → report" pattern? The process should reflect the lens's characteristic moves in a specific sequence with specific interactions.
- Could an agent follow these steps mechanically and produce useful output? If the steps require interpretive judgment the profile hasn't specified, the process is under-defined.
- Is there a clear termination condition? The agent needs to know when it's done.

---

### 2.9 Output Structure

**Purpose:** Define what the agent's output looks like — section names, ordering, content requirements per section.

**Contents:**

- **Report sections** — Named sections in the order they appear, with content description for each.
- **Finding format** — How individual observations/findings are structured. Include: what fields a finding has, how findings are categorized, and how findings reference the decision vocabulary.
- **Implications section** — Per the agent-output-implications-spec, each agent type uses a type-specific section label (AUDIT IMPLICATIONS, VALIDATION IMPLICATIONS, etc.) with scoped framing rather than broad recommendation language. Define: the section label, the framing question, and the scope boundary for this thinker × role combination.
- **Summary format** — How the overall verdict is presented.

**ADL mapping:** Direct mapping to `output` block including `output.implications`.

**Quality test:** Given this output structure, could a consumer of the report understand the analysis without knowing anything about the thinker's framework? The output structure should be self-documenting — section names and finding formats should make the analytical logic visible.

---

### 2.10 Tone & Voice

**Purpose:** Calibrate the agent's communication style to match the lens's character without simulating the thinker's personality.

**Contents:**

- **Register** — Academic, clinical, conversational, etc.
- **Confidence posture** — How does the agent express certainty and uncertainty? Does this lens tend toward assertive claims or hedged observations?
- **Characteristic phrasing** — 3–5 examples of how this lens naturally expresses its observations. Not personality simulation — these are framework-native ways of stating findings. (e.g., A Humean agent naturally says "the claim rests on habit rather than observation" — this is framework vocabulary, not personality.)
- **What to avoid** — Tonal anti-patterns. What would make this agent sound wrong?

**ADL mapping:** Direct mapping to `tone` block.

**Quality test:** Would the tone be recognizably different from a generic analysis agent? If the tone section could apply to any lens, it's not specific enough.

---

### 2.11 Composition Guidance

**Purpose:** Elaborate the composition affinity data from the library spec into actionable pairing guidance.

**Contents:**

- **Pairs well with** — For each recommended pairing:
  - Which agent (name + role)
  - Why the pairing is productive
  - Which composition pattern applies (adversarial_dialectic, parallel_reading, sequential_pipeline, complementary_coverage)
  - What the combined output reveals that neither lens alone would see

- **Covers blind spots of** — For each:
  - Which agent's blind spot is covered
  - Name of the blind spot
  - How this lens's characteristic moves correct the distortion

- **Has blind spots covered by** — For each:
  - Which of this lens's failure signatures is addressed
  - Which agent provides the correction
  - How the correction works

**ADL mapping:** Direct mapping to `composition` block.

**Quality test:** Are the pairings genuinely productive, or are they just "different lenses looking at the same thing"? A productive pairing should produce specific analytical insights that neither lens alone would generate. If you can't describe the specific insight, the pairing is hypothetical.

---

### 2.12 Role-Specific Elaborations

**Purpose:** Document how the thinker's cognitive machinery adapts to each planned agent role.

**Contents:** One subsection per planned role, each containing:

- **Role fit assessment** — Why is this thinker's cognitive operation suited to this role? What aspect of the machinery maps to the role's function?
- **Role-specific characteristic moves** — Do any moves from §2.3 change when operating in this role? Are there moves that only apply in this role?
- **Role-specific output modifications** — How does the output structure (§2.9) change for this role?
- **Role-specific failure signatures** — Are there failure modes unique to this thinker × role combination?

**Conditional:** Only include roles listed in the library spec's Priority Roles for this thinker. Do not speculatively elaborate roles that aren't planned.

**ADL mapping:** Each role elaboration maps to a distinct ADL definition (e.g., `aristotle-analyst.agent.yaml`, `aristotle-validator.agent.yaml`).

**Quality test:** Does the role-specific elaboration reveal something new about the cognitive machinery, or does it just repeat the universal sections with role-flavored vocabulary? If the analyst and validator elaborations are interchangeable, the role distinction isn't real.

---

### 2.13 Exemplar Findings — OPTIONAL, ADD WHEN AVAILABLE

**Purpose:** Provide concrete examples of what good output from this lens looks like when pointed at a real or realistic artifact. These serve as few-shot examples for the encoding step and as calibration references for output quality review.

**When to add:** Exemplar findings are incorporated iteratively as agents are encoded, deployed, and run against real artifacts. Profiles begin without them. When production data produces a finding that demonstrates the lens's unique visibility, it gets added here. Manually authored exemplars are acceptable as placeholders but should be flagged as `[authored, not production]` — they may be aspirational rather than representative.

**Contents:** 2–3 exemplar findings, each with:

- **Target artifact description** — Brief description of what's being analyzed.
- **Finding** — A complete, formatted finding as the agent would produce it.
- **Why this is good** — Annotation explaining what makes this finding a strong example of the lens in action. What characteristic move is visible? What would a weaker version of this finding look like?

**ADL mapping:** Informs `knowledge_base` safe patterns and serves as calibration reference during agent testing.

**Quality test:** Would this finding be impossible (or at least much weaker) if produced by a different lens? The exemplar should demonstrate the lens's unique visibility — what only this lens sees.

---

## 3. ADL Field Mapping Summary

| Profile Section | ADL Field(s) |
|-----------------|--------------|
| 2.0 Front Matter | `interface` (name, version, displayName, agentType, domain, tags) |
| 2.1 Cognitive Identity | `interface.description`, `mission`, `context` |
| 2.2 Core Axioms | `cognitive_lens.core_axioms[]` |
| 2.3 Characteristic Moves | `process` steps, `knowledge_base` |
| 2.4 Decision Vocabulary | `decisions`, `mission` |
| 2.5 Failure Signatures | `cognitive_lens.failure_signatures[]`, `edge_cases` |
| 2.6 Key Definitions | `knowledge_base`, `context` |
| 2.7 Reference Knowledge | `knowledge_base` |
| 2.8 Process Architecture | `process` |
| 2.9 Output Structure | `output`, `output.implications` |
| 2.10 Tone & Voice | `tone` |
| 2.11 Composition Guidance | `composition` |
| 2.12 Role-Specific Elaborations | Per-role ADL definition overrides |
| 2.13 Exemplar Findings | `knowledge_base` safe patterns, test calibration |

---

## 4. Quality Criteria

A Thinker Profile is ready for encoding when:

### 4.1 Completeness

- [ ] All mandatory sections (§2.0–§2.12) are populated
- [ ] Core axioms number 3–5, each with implications and tension points
- [ ] Characteristic moves number 4–8, each traceable to an axiom
- [ ] Decision vocabulary includes criteria, threshold question, and edge cases
- [ ] Failure signatures number 2–5, each with mechanism, recognition pattern, and mitigation
- [ ] Key definitions number 5–15
- [ ] Reference knowledge includes common mistakes, red flags, and safe patterns
- [ ] Process architecture specifies a named methodology with step descriptions
- [ ] Output structure defines sections, finding format, and implications section
- [ ] Composition guidance includes specific pairings with named patterns

### 4.2 Specificity

- [ ] No section could apply unchanged to a different thinker in the library
- [ ] The cognitive operation is described concretely enough for someone unfamiliar with the thinker to understand
- [ ] Common mistakes and red flags are ones an LLM would actually produce, not ones a human student would make
- [ ] Exemplar findings (if present) demonstrate unique visibility — findings that only this lens would produce

### 4.3 Internal Consistency

- [ ] Every characteristic move traces back to at least one axiom
- [ ] Every failure signature traces back to a specific strength taken too far
- [ ] The process architecture uses the characteristic moves in a coherent sequence
- [ ] The decision vocabulary criteria align with what the process architecture produces
- [ ] The output structure has a place for everything the process produces

### 4.4 Differentiation

- [ ] "What This Is Not" (§2.1) names specific other library entries and states clear distinctions
- [ ] No axiom is a truism (someone could disagree in good faith)
- [ ] No characteristic move is generic (another lens could not perform the same operation)
- [ ] The decision vocabulary captures something PASS/FAIL would lose

### 4.5 Encodability

- [ ] Every section maps to at least one ADL field (per §3)
- [ ] No section requires interpretive judgment beyond what the profile specifies
- [ ] The process architecture is mechanical enough to follow — steps produce defined outputs
- [ ] Tone guidance is specific enough to produce recognizably different agent voice

---

## 5. Anti-Patterns

### 5.1 The Wikipedia Profile

**Symptom:** The profile reads like an encyclopedia article about the thinker — historically accurate, philosophically coherent, but operationally empty. Heavy on biography and intellectual context, light on characteristic moves and output structure.

**Root cause:** The author is describing the thinker rather than describing what the thinker's lens does to an artifact.

**Fix:** Every sentence should pass the "so what does the agent DO?" test. If a sentence describes the thinker's life, influence, or historical context without connecting it to an analytical operation, remove it.

### 5.2 The Vocabulary Decorator

**Symptom:** The profile uses the thinker's terminology extensively but the characteristic moves are generic analysis steps wearing specialist labels. "Apply the epoché" means "set aside assumptions." "Perform four-cause decomposition" means "list four things about it."

**Root cause:** Framework vocabulary has been adopted without framework thinking. The moves use the right words but don't produce structurally different analysis.

**Fix:** For each characteristic move, ask: what observation would this move produce that a generic analyst would miss? If you can't name a specific, concrete example, the move is decorative.

### 5.3 The Omniscient Lens

**Symptom:** The failure signatures are perfunctory or absent. The profile implies the lens can analyze anything productively. Blind spots are acknowledged in a single sentence rather than elaborated with mechanisms and recognition patterns.

**Root cause:** The author is advocating for the lens rather than honestly documenting its boundaries.

**Fix:** The failure signatures should be the profile's most uncomfortable section. If the author isn't slightly worried that the lens's failures are serious, the section is whitewashed. Each failure should be traceable to a strength — the best lenses fail in specific, predictable, correctable ways.

### 5.4 The Clone Profile

**Symptom:** Two profiles for thinkers in the same tradition are structurally identical with minor vocabulary substitutions. Confucius and Mozi profiles that differ only in terminology. Husserl and Heidegger profiles that make the same observations using different words.

**Root cause:** The differentiating operation hasn't been identified clearly enough. The "What This Is Not" section (§2.1) was skipped or treated as formality.

**Fix:** Run the two profiles against the same hypothetical artifact and ask: would the findings differ? If not, one of the profiles doesn't need to exist, or the core operations haven't been distinguished sharply enough.

---

## 6. Versioning and Lifecycle

### 6.1 Profile Versioning

Thinker Profiles use semantic versioning:

- **MAJOR** — Fundamental change to cognitive identity or core axioms (rare; may indicate the library entry itself needs revision)
- **MINOR** — New characteristic moves, revised reference knowledge, additional role elaborations, new exemplar findings
- **PATCH** — Corrections, clarifications, improved examples

### 6.2 Profile-to-ADL Traceability

Each ADL definition generated from a profile MUST include in its `context` block:

```yaml
context:
  source_profile: "aristotle-profile-v1.2.0"
  profile_version: "1.2.0"
  encoding_date: "2026-03-05"
```

This enables tracing from any agent definition back to the specific profile version it was encoded from. When a profile is updated, downstream ADL definitions can be flagged for potential re-encoding.

### 6.3 Lifecycle States

```
Draft → Review → Validated → Encoded → [Profile updated → Re-review → Re-encoded]
```

The current review process is internal — founder and Claude iterating on the profile until it meets the quality criteria in §4. Scholar review (Expert Fellowship Program) becomes part of the lifecycle when the project is live and those resources are available. Until then, "Validated" means "reviewed against §4 criteria and judged ready for encoding."

A profile in "Encoded" status may be updated (returning to "Review") if:
- Production run data reveals gaps in the profile's reference knowledge
- Composition testing reveals undocumented failure signatures
- Schema changes in ADL require new profile sections

---

## 7. Design Decisions

Decisions made during initial specification. Recorded here for traceability.

### 7.1 Profile depth calibration — RESOLVED

**Decision:** Reference knowledge should be commensurate with the role being encoded. The Aristotle Analyst definition (693 lines) represents the upper bound for agent definition length. Analyst, Validator, and Forecaster roles require more detailed reference knowledge due to the precision of what they perform. Explorer roles are lighter — they generate questions and hypotheses, which demands less reference apparatus. The profile should provide a sufficient knowledge base for all planned roles — enough that each role-specific ADL definition can draw from the profile without inventing material.

**Implication:** §2.7 (Reference Knowledge) depth should scale with the thinker's planned roles. A thinker planned for Analyst + Validator needs deeper reference knowledge than one planned only for Explorer. The profile is not the agent definition — it's the design document the agent definition draws from. But it should be rich enough that the encoding step is translation, not creation.

### 7.2 Cross-thinker reference knowledge — RESOLVED

**Decision:** Self-contained. Each profile includes all reference knowledge needed for encoding, even where that means restating patterns that apply across lenses. Duplication is acceptable; invisible dependencies on shared resources are not.

**Rationale:** Shared reference knowledge creates a maintenance burden and an implicit coupling between profiles. If a universal anti-pattern is updated, every profile that inherits it must be re-validated. Self-contained profiles can be independently authored, reviewed, and encoded without tracking cross-profile dependencies. Universal anti-patterns (e.g., "don't produce generic observations decorated with specialist vocabulary") should be stated in each profile where they apply, in the thinker's own terms.

### 7.3 Exemplar finding sourcing — RESOLVED

**Decision:** Build and test over time. Profiles begin without exemplar findings. As agents are encoded, deployed, and run against real artifacts, production findings are incorporated back into the profile as exemplar findings. This is iterative, not bootstrapped.

**Rationale:** This is a long project. Profiles will be authored for thinkers that seem interesting and iterated on through use. Some will reach ADL encoding and production deployment; others may remain at the profile stage for extended periods. Exemplar findings arrive when they arrive. The profile's value doesn't depend on having them — they enhance it when available. The §2.13 section remains OPTIONAL but RECOMMENDED, with the understanding that "recommended" means "add them when you have them."

### 7.4 School-level profiles — RESOLVED (DEFERRED)

**Decision:** Hold off. Establish individual thinker profiles first. Optimize through iteration on those definitions before introducing school-level abstraction.

**Rationale:** The School Inheritance Model is defined in the library spec (§4.1) and has an ADL mapping via `composition.inherits_from`. But the profile layer doesn't need to replicate that structure yet. Individual profiles for thinkers within the same tradition (e.g., Marcus Aurelius, Epictetus, Seneca) may reveal shared patterns naturally — at which point a school-level optimization can be designed from observed commonality rather than predicted commonality. There may also be alternative approaches to handling school-level defaults that don't require attaching inheritance to the YAML schema.

### 7.5 Non-Western tradition review — RESOLVED (DEFERRED)

**Decision:** Do the best we can with available resources now. Scholar validation and tradition-specific review criteria are future concerns for when the project is live and the Expert Fellowship Program is operational.

**Rationale:** The current team is the founder and Claude. The quality criteria in §4 are tradition-neutral by design, and the profile structure is flexible enough to accommodate traditions whose categories don't cleanly map to Western philosophical notation. Where a profile author recognizes a mapping problem (e.g., Ifá's 256 Odù figures don't fit neatly into "3–5 axioms"), the profile should document the tension honestly rather than forcing the fit. Formal scholar validation becomes a requirement when the project has the resources to support it — not before.

---

## 8. Changelog

### v0.1.0 — March 5, 2026
- Initial specification
- 13 profile sections defined (§2.0–§2.13)
- ADL field mapping table (§3)
- Quality criteria checklist (§4)
- Anti-patterns documented (§5)
- Versioning and lifecycle defined (§6)
- 5 design decisions resolved (§7)

---

*Prepared by Alex Self, Ulu Labs Inc. For internal use and Cognitive Lens Library development.*
