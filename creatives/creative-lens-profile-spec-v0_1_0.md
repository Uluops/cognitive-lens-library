# Creative Lens Profile Specification

**Version:** 0.1.0
**Status:** Draft
**Date:** March 14, 2026
**Author:** Alex Self, Ulu Labs Inc.
**Depends on:** Cognitive Lens Library Spec v0.3.0, ADL v1.10.0, Thinker Profile Spec v0.1.0

---

## 1. Purpose

This specification defines the structure, content requirements, and quality criteria for **Creative Lens Profile** documents — the intermediate design artifact between a Cognitive Lens Library catalog entry and an ADL agent definition for creative cognitive operations.

### 1.1 The Problem

The Cognitive Lens Library encodes epistemological engines — structured reasoning patterns developed across civilizations. Through v0.3.0, every entry in the library operates through verbal-propositional reasoning: argument, analysis, logical structure. The library's selection criteria (§1.2) are medium-agnostic, but every thinker who passes them so far shares a common register: they decompose, evaluate, and conclude using language about language.

This leaves an entire class of cognitive operations unencoded: operations developed through *making* — design, composition, craft, artistic practice. These operations satisfy all four selection criteria. Cubist simultaneous multi-perspective rendering is a distinct cognitive operation. Dieter Rams's reductive functionalism is operationally encodable. Kintsugi's repair-as-revelation produces findings with low overlap to any philosophical lens. Each has identifiable boundaries where it distorts.

What they share is a structural property the philosophical lenses lack: they were developed in and for a **specific medium** — visual art, industrial design, ceramics, music, architecture. Pointing them at software artifacts requires an explicit translation step that philosophical lenses skip. Aristotle's four-cause analysis is medium-agnostic by construction. Rams's "less but better" was built for manufactured objects. The translation from physical product to software artifact is where the intellectual work lives, and where the profile must do its heaviest lifting.

### 1.2 Relationship to the Thinker Profile Spec

This specification is a **sibling** of the Thinker Profile Spec v0.1.0, not a fork. Both occupy the same pipeline position:

```
Library Spec Entry  →  Profile  →  ADL YAML  →  Rendered Agent Prompt
   (~20 lines)         (this document)      (schema)       (runtime)
   
   WHAT & WHY          HOW (design)         HOW (formal)   HOW (execution)
   Selection &         Cognitive machinery  Schema-native   LLM-consumable
   justification       elaboration          encoding        prompt
```

The Creative Lens Profile shares 80% of its structure with the Thinker Profile. The differences are concentrated in four areas:

| Structural Difference | Section | Nature of Change |
|---|---|---|
| Medium Translation | §2.1 (new subsection) | Added — creative operations need explicit medium mapping |
| Core Principles | §2.2 (renamed + modified quality tests) | Adapted — creative commitments differ from epistemic axioms |
| Move Register | §2.3 (new field per move) | Added — creative moves operate in multiple output registers |
| Compositional Logic | §2.X (new section) | Added — how the creative arranges elements in relationship |

Sections §2.4 through §2.13 are structurally identical to the Thinker Profile Spec. This spec inherits those sections by reference and does not redefine them. Where a creative profile requires modification to an inherited section, the modification is documented in §2.14 (Creative Adaptations to Inherited Sections).

### 1.3 What We Are Encoding

For each creative source, we extract:

- **Core Creative Operation** — The fundamental perceptual or compositional move that defines this lens's contribution. What does this lens *do* to its input that no other lens does?
- **Medium Translation** — How the operation, developed for [original medium], maps onto analysis of text-based artifacts (code, specifications, definitions, documentation). This is the load-bearing section — without it, the agent produces vocabulary decoration.
- **Compositional Logic** — How the creative arranges elements in relationship to each other. Proportion, rhythm, hierarchy, tension, balance, negative space — the grammar of arrangement that defines what "well-composed" means for this lens.
- **Decision Vocabulary** — Native judgment categories, replacing generic PASS/FAIL with framework-native assessments.
- **Move Register** — Whether each characteristic move operates in analytical, perspectival, or transformative register.
- **Structural Blind Spots** — Where the lens distorts. Critical for honest composition with philosophical lenses.
- **Composition Affinity** — Which philosophical and creative lenses complement, challenge, or extend this one.

### 1.4 Source Types

Creative lens sources come in three forms that the philosophical library rarely encounters:

| Source Type | Description | Examples | Profile Implications |
|---|---|---|---|
| **Individual** | A single practitioner with documented methodology | Dieter Rams, Picasso, Miles Davis | Profile follows individual attribution; "What This Is Not" distinguishes from contemporaries |
| **Practice** | A cultural or craft practice with no single author | Kintsugi, Wabi-sabi, Ikebana | Profile attributes to the practice, not practitioners; "Core Principles" derive from the tradition's accumulated logic, not an individual's stated beliefs |
| **School / Movement** | A named movement with multiple practitioners and documented principles | Bauhaus, De Stijl, Brutalism | School Inheritance Model may apply (see Cognitive Lens Library Spec §4.1); profile establishes the school-level operation, individual practitioners may specialize via fork |

The Thinker Profile Spec handles individuals exclusively (with School-level profiles deferred per §7.4). The Creative Lens Profile must handle all three source types from the start, because practices and movements are more common in creative traditions than in philosophical ones.

### 1.5 Selection Criteria

Creative lens sources use the same four selection criteria as philosophical entries (Cognitive Lens Library Spec §1.2):

1. **Distinct cognitive operation** — The source contributes a perceptual, compositional, or making pattern that is not reducible to another entry in the library.
2. **Operational encodability** — The pattern can be described as a structured operation on inputs, not merely as an aesthetic preference or stylistic tendency.
3. **Productive divergence** — When pointed at the same artifact as other lenses (philosophical or creative), this one produces findings with low overlap and high complementary value.
4. **Self-limiting honesty** — The framework has identifiable boundaries where it distorts, enabling principled composition rather than false omniscience.

One additional criterion applies to creative sources only:

5. **Medium translatability** — The operation, developed for its native medium, can be mapped onto text-based artifact analysis in a way that produces genuinely different observations — not metaphorical observations wearing aesthetic labels.

A creative source that satisfies criteria 1–4 but fails criterion 5 may still be cataloged in the library spec, but it cannot proceed to profile development until a credible medium translation is documented. This is the creative equivalent of the philosophical library's "operational encodability" gate — the question is not "is this interesting?" but "can the agent *do* something with it?"

### 1.6 Agent Type Taxonomy — Extended

The philosophical library uses four agent roles: Analyst, Validator, Explorer, Forecaster. Creative lenses use all four and add two that philosophical lenses underutilize:

| Role | Function | Output | Philosophical Lenses | Creative Lenses |
|---|---|---|---|---|
| **Analyst** | Reads an artifact through the lens; produces structured observations | Findings with framework-native categories | Primary role | Supported |
| **Validator** | Evaluates whether an artifact meets the lens's standards | Score + decision vocabulary verdict | Supported | Supported |
| **Explorer** | Generates questions, hypotheses, or maps territory | Structured inquiry agenda or map | Supported | Often primary |
| **Forecaster** | Projects futures, risks, or consequences | Scenario analysis with confidence markers | Supported | Supported |
| **Generator** | Produces a new or modified artifact embodying the lens's principles | Artifact (redesigned, reduced, systematized, or re-rendered) | Rarely useful | Often primary |
| **Executor** | Performs transformations on artifacts with completion criteria and rollback | Modified artifact with verification | Rarely useful | High-impact when safe |

> **Note on Generator and Executor roles:** These roles exist in ADL v1.10.0 and are used extensively in the planning agent family (test-plan-generator, migration-plan-generator). They are underutilized in the philosophical library because philosophical lenses analyze — they decompose, evaluate, and conclude, but they rarely *make* things. Creative lenses both analyze and make. A Rams Generator that takes a 15-endpoint API spec and produces a 4-endpoint redesign, or a Bauhaus Generator that takes ad hoc configuration patterns and produces a systematic design language, are natural expressions of creative cognitive operations that philosophical lenses cannot replicate.

> **Validation gap:** Generator and Executor roles for cognitive lens agents have zero production data. The first creative lens build SHOULD include at least one Generator to validate the role before expanding. If Generator output quality requires different ADL patterns (e.g., the `tasks` block needs a `register` field), this should surface early.

---

## 2. Profile Structure

Every Creative Lens Profile follows this structure. Sections marked **NEW** or **MODIFIED** differ from the Thinker Profile Spec. Sections marked **INHERITED** are structurally identical to the Thinker Profile Spec and are referenced here for completeness but not redefined.

### 2.0 Front Matter

```markdown
# [Source Name] — Creative Lens Profile

**Version:** [semver]
**Status:** [Draft | Review | Validated | Encoded]
**Date:** [ISO date]
**Library Entry:** §[section reference] of Cognitive Lens Library Spec v[version]
**Source Type:** [Individual | Practice | School]
**Native Medium:** [The medium in which the operation was originally developed]
**Maturity:** [✅ VALIDATED | ⚠️ HYPOTHESIZED | 🔬 CANDIDATE]
**Planned Roles:** [Analyst, Validator, Explorer, Forecaster, Generator, Executor — as applicable]
**Implementation Phase:** [Phase number from library spec]
```

**Differences from Thinker Profile:**
- **Source Type** field added (Individual / Practice / School)
- **Native Medium** field added (industrial design, visual art, ceramics, music, architecture, etc.)
- **Planned Roles** may include Generator and Executor

**Status values:** Same as Thinker Profile Spec §2.0.

---

### 2.1 Creative Identity — MODIFIED

**Purpose:** Establish what this lens IS — its core creative contribution, irreducible to any other entry in the library (philosophical or creative).

**Contents:**

- **Core Creative Operation** — Expanded from the library entry's one-sentence description into a 2–3 paragraph explanation of what the lens does to its input. This should be concrete enough that someone unfamiliar with the source could understand the operation being performed. Avoid biographical framing for individuals, historical framing for movements, and romantic framing for practices. Describe the operation, not the story.

- **Medium Translation** — NEW. 2–4 paragraphs documenting how the creative operation, originally developed for [native medium], maps onto text-based artifact analysis. This is the profile's most important section. It must:

  1. **Name the native medium** and state what the operation does within it. "Rams's reductive functionalism, developed for industrial product design, removes components that don't serve the product's core function."
  2. **Identify the structural parallel** between the native medium and software artifacts. "In industrial design, 'components that don't serve function' are physical parts. In software artifacts, 'components that don't serve function' are abstractions, configuration layers, process steps, API endpoints, or structural elements that exist for historical, ceremonial, or defensive reasons rather than operational ones."
  3. **State the translation explicitly for each core principle.** Do not assume the reader will map "honest materials" to "honest abstractions" on their own. Each principle gets its own translation with at least one concrete software example.
  4. **Identify where the translation breaks.** Not every aspect of the native medium maps cleanly. "Rams's principle of environmental harmony (products should not pollute the visual environment) has no clean software equivalent — code has no visual environment in the same sense. The closest analogue is API surface pollution: whether the artifact introduces unnecessary concepts into the consuming codebase's namespace." Name the stretch. Name what doesn't translate.

- **What This Is Not** — Explicitly distinguish this lens from the most likely confusions. Name both creative and philosophical entries it could be mistaken for. Creative lenses carry a high risk of being confused with each other when they share a medium (Rams vs. Bauhaus, Kintsugi vs. Wabi-sabi) or when they share a surface principle (Rams's reduction vs. Epicurus's ataraxia — both value simplicity, but for different reasons producing different analytical moves).

- **Controversy** — CONDITIONAL: Same policy as Thinker Profile Spec §2.1. Required for sources with significant ethical controversy. Factual statement, not editorial.

**ADL mapping:** Informs `interface.description`, `mission`, `context`, `knowledge_base`.

**Quality tests:**
- Could someone who has never encountered this creative source understand the operation well enough to recognize it in action? If not, the description is too abstract or too romantic.
- Does the Medium Translation produce genuinely different observations when applied to a software artifact, or does it produce generic analysis with aesthetic labels? Test: remove the creative vocabulary and check if the observations survive. If they do, the translation is real. If they collapse into generic analysis, it's decoration.
- Is every principle translated individually with a concrete software example? If any principle is left at the metaphorical level ("code should breathe"), the translation is incomplete.
- Does the "where the translation breaks" subsection identify at least one principle that doesn't map cleanly? If every principle translates perfectly, the author hasn't looked hard enough.

---

### 2.2 Core Principles — MODIFIED

**Purpose:** Articulate the foundational commitments that drive the lens. These are the propositions the lens treats as given — not conclusions it reaches, but starting points from which all operation proceeds.

**Terminology change:** The Thinker Profile uses "axioms" — propositions about how knowledge works, how reality is structured, or how inquiry should proceed. Creative lenses operate from **principles** — commitments about the relationship between form, function, material, maker, and context. This is not merely a rename. The quality tests differ because the epistemic status differs.

**Contents:** 3–7 principles, each with:

- **Principle statement** — One sentence. Should be expressible as a commitment about how artifacts should relate to their materials, their users, their function, or their context. Principles are normative where axioms are descriptive: "form follows function" is a commitment to a relationship between form and function, not a claim about reality.
- **Implications** — 2–4 practical consequences. Each implication should describe how this principle changes what the lens notices, prioritizes, or judges when analyzing a software artifact. Implications must use the Medium Translation vocabulary — not the native medium vocabulary.
- **Tension points** — Which other library entries' axioms or principles directly conflict with this one? Creative-to-philosophical tensions are especially valuable: Rams's reductive principle is in direct tension with Aristotle's completeness instinct (every part serves telos — but Rams asks whether every part *should exist*). Rams-to-Gap-Analyst tension is productive: Rams says "remove this," Gap Analyst says "but it's structurally required."

**ADL mapping:** Direct mapping to `cognitive_lens.core_axioms[].axiom` and `cognitive_lens.core_axioms[].implications`. (The ADL field is named `core_axioms` for schema compatibility; the profile uses "principles" for conceptual accuracy.)

**Quality tests:**
- Does negating this principle produce a *different artifact*? If "less but better" were replaced with "more and richer," would the agent's analysis change? If negating the principle doesn't change the output, the principle is decorative.
- Are these genuinely foundational, or are they derived from something more basic? If a principle can be explained as a consequence of another principle in the same list, it's not foundational.
- Can an intelligent person endorse a different principle in good faith? If not, it's a truism. "Good design should serve users" is a truism. "Good design removes everything that isn't essential to function" is a principle — a Maximalist lens would disagree.
- Do the principles, taken together, generate the characteristic moves in §2.3? If you can't trace each move back to a principle, something is missing.
- Are the implications stated in software terms, not native medium terms? "Remove unnecessary physical components" belongs in the native medium description. "Remove abstraction layers that exist for organizational ceremony rather than operational function" belongs in the implications.

---

### 2.3 Characteristic Moves — MODIFIED

**Purpose:** Name and describe the specific operations the lens performs on its input. These are the lens's "verbs" — the things it does when pointed at an artifact.

**Contents:** 4–8 named moves, each with:

- **Move name** — Short, descriptive. Prefer the source's native terminology where it's clear enough (e.g., "Reductive audit," "Multi-perspective rendering," "Repair mapping"), but provide an English gloss when the native term is opaque.
- **What it does** — 2–3 sentences describing the operation. What does the agent look for? What does it do when it finds it?
- **What it produces** — What kind of observation or output does this move generate? How does the output differ from other moves in this lens?
- **Derivation** — Which principle(s) from §2.2 generate this move? Brief statement of the logical connection.
- **Move Register** — NEW. Which output register this move operates in. One of:

| Register | What the move does | Output type | Example |
|---|---|---|---|
| **Analytical** | Decomposes the artifact using the creative framework | Propositional finding — same as philosophical lenses | "This abstraction layer is ornamental — it adds indirection without adding function" |
| **Perspectival** | Re-presents the artifact from an alternative viewpoint | Rendering — a re-description that reveals structure the original perspective hides | "From the operator's perspective, this API surface looks like: [re-description]" |
| **Transformative** | Produces a modified version of the artifact or a portion of it | Artifact delta — "here is what this looks like if you apply [principle]" | "Reduced endpoint set: [4-endpoint alternative to the original 15]" |

A single move may operate in multiple registers depending on the agent type. Document the primary register and note which roles activate secondary registers.

**ADL mapping:** Informs `process` block steps and `knowledge_base` reference material.

**Quality tests:**
- All quality tests from Thinker Profile Spec §2.3 apply.
- Additionally: Is the move register correctly identified? An "analytical" move that only produces observations ("this is ornamental") should not be labeled "transformative." A "transformative" move that produces a new artifact must specify what form the output takes.
- Does at least one move operate in a register other than analytical? If all moves are analytical, the creative lens is being reduced to a philosophical one — the creative-specific cognitive operations are missing.
- For perspectival moves: whose perspective? The move must name the viewpoint it renders from — "the implementor," "the operator," "the new hire reading this in six months." An unnamed perspective is a generic re-read, not a perspectival rendering.
- For transformative moves: what are the constraints? "Produce a simpler version" is under-specified. "Produce a version with fewer than half the endpoints that preserves all documented use cases" is constrained.

---

### 2.X Compositional Logic — NEW

**Purpose:** Document how the creative source arranges elements in relationship to each other — the grammar of arrangement that defines what "well-composed" means for this lens. This section has no equivalent in the Thinker Profile Spec because philosophical lenses don't have compositional logics — they have argumentative structures, which are captured by the Process Architecture section.

**Why this section exists:** Two creative lenses can share a surface principle (both value "honesty") while having completely different compositional logics. Rams's compositional logic emphasizes proportion and harmony — elements should be sized according to their importance and arranged to produce visual calm. Brutalism's compositional logic emphasizes confrontation and weight — elements should assert their presence, and concealment is dishonesty. Same principle of honesty, opposite compositional instincts. The compositional logic is what makes each lens produce structurally different analysis from lenses that share its vocabulary.

**Contents:**

- **Arrangement Grammar** — How does this lens relate elements to each other? 3–5 compositional principles, each stated as a rule about arrangement. Examples:
  - *Proportion*: "Element prominence should be proportional to element importance. A 3-line configuration should not require a 47-line abstraction hierarchy."
  - *Rhythm*: "Alternate complexity and simplicity. Dense logic should be followed by clear interfaces. A codebase that is uniformly complex is as poorly composed as one that is uniformly trivial."
  - *Negative space*: "What is deliberately absent is as important as what is present. The spec should leave room — sections that are intentionally empty, extension points that are intentionally unimplemented, decisions that are intentionally deferred."
  - *Tension*: "Productive dissonance between elements reveals structure. Complementary components should create contrast, not redundancy."

- **Software Translation** — For each compositional principle: what does it mean when applied to code, specifications, agent definitions, API surfaces, or documentation? Each translation needs a concrete example and a counter-example. "Proportion in an API means: a CRUD resource with 4 operations should not have 12 configuration options. Counter-example: a CRUD resource where the configuration surface is larger than the operational surface — the configuration has become the product."

- **What "Well-Composed" Means** — A 1–2 paragraph synthesis: for this lens, when is an artifact well-composed? This should be a description of the compositional *quality* the lens seeks, distinct from correctness (validators), purpose (Aristotle), evidence (Hume), or falsifiability (Popper). Compositional quality is about *arrangement* — the relationships between parts — and the creative lenses are the only entries in the library that make this their primary concern.

**ADL mapping:** Informs `knowledge_base` reference material, `process` analysis phases, and `scoring` criteria for Validators.

**Quality tests:**
- Are the compositional principles genuinely about *arrangement* — relationships between elements — or are they about individual element quality? "Code should be readable" is about individual quality. "Complex modules should be adjacent to their simplest consumers" is about arrangement.
- Does the Software Translation produce a judgable claim? "This API has good proportion" is unjudgable. "This API's configuration surface is 3x larger than its operational surface" is judgable.
- Could a different creative lens with the same principles produce different compositional judgments? If two lenses with "honesty" principles have the same compositional logic, they're the same lens. The compositional logic is the differentiator.

---

### 2.4 Decision Vocabulary — INHERITED

Structurally identical to Thinker Profile Spec §2.4. No modifications.

Creative decision vocabularies follow the same pattern: a primary binary or spectrum (ESSENTIAL / ORNAMENTAL, HONORED / CONCEALED, INTEGRATED / PRIVILEGED), with criteria, threshold question, and edge cases.

**Additional quality test for creative lenses:** Does the decision vocabulary describe a *compositional* or *material* quality rather than a logical one? If the vocabulary could be applied by a philosophical lens without the creative framework, it's not creative-specific. ESSENTIAL / ORNAMENTAL is creative — it judges the relationship between presence and function. CONSISTENT / CONTRADICTED is philosophical — it judges logical coherence. A creative lens that produces a philosophical vocabulary hasn't been translated; it's been absorbed.

---

### 2.5 Failure Signatures — INHERITED

Structurally identical to Thinker Profile Spec §2.5. No modifications.

Creative lenses have one additional failure mode not common in philosophical lenses:

**Medium Leakage** — The agent applies native-medium judgment directly instead of using the translated operation. A Rams agent that talks about "visual clutter" in a YAML file, a Kintsugi agent that discusses "golden lacquer" in an API spec, a Jazz agent that evaluates whether code "swings." The agent is simulating the creative persona rather than applying the translated operation. This is the creative equivalent of the vocabulary decorator anti-pattern, and every creative profile should include a Medium Leakage failure signature with a recognition pattern and mitigation.

---

### 2.6 Key Definitions — INHERITED

Structurally identical to Thinker Profile Spec §2.6. No modifications.

Creative profiles will typically have more definitions than philosophical profiles because two vocabularies are in play: the native-medium vocabulary (which the agent should understand but rarely use directly) and the translated vocabulary (which the agent uses in output). Definitions should clearly mark which vocabulary a term belongs to and when the native-medium term is acceptable in output versus when the translated term must be used.

---

### 2.7 Reference Knowledge — INHERITED

Structurally identical to Thinker Profile Spec §2.7. No modifications.

**Depth calibration note for creative lenses:** Generator and Executor roles demand higher reference knowledge depth than Analyst roles — the agent needs enough knowledge to *produce* artifacts that embody the creative principles, not just analyze artifacts against them. A Rams Analyst needs to know what "ornamental" looks like in software. A Rams Generator needs to know what "essential" looks like in software — with enough detail to produce a reduced alternative that is actually functional.

---

### 2.8 Process Architecture — INHERITED

Structurally identical to Thinker Profile Spec §2.8. No modifications.

**Process note for multi-register lenses:** When a lens's characteristic moves operate in different registers (analytical, perspectival, transformative), the process architecture should specify which register each phase operates in and how outputs from one register feed into another. A typical creative process might be: Phase 1 (Analytical — inventory the artifact's elements), Phase 2 (Perspectival — re-render from alternative viewpoints), Phase 3 (Analytical — identify where perspectives diverge), Phase 4 (Transformative — produce modified version based on findings from Phases 1–3). The register transitions are the creative process's distinguishing feature.

---

### 2.9 Output Structure — INHERITED

Structurally identical to Thinker Profile Spec §2.9. No modifications.

**Output note for creative lenses:** The existing implications section labels (AUDIT IMPLICATIONS, VALIDATION IMPLICATIONS, DISCOVERY IMPLICATIONS, TRAJECTORY IMPLICATIONS) are role-specific, not lens-specific. Creative lenses use the same labels. However, Generator and Executor roles need output sections not covered by the current label set:

| Agent Type | Default Section Label | Creative Extension |
|---|---|---|
| `analyst` | AUDIT IMPLICATIONS | — |
| `validator` | VALIDATION IMPLICATIONS | — |
| `explorer` | DISCOVERY IMPLICATIONS | — |
| `forecaster` | TRAJECTORY IMPLICATIONS | — |
| `generator` | GENERATION OUTPUT | New — the produced artifact, with rationale for each transformation |
| `executor` | EXECUTION REPORT | New — what was changed, verification results, rollback state |

---

### 2.10 Tone & Voice — INHERITED

Structurally identical to Thinker Profile Spec §2.10. No modifications.

**Tone note for creative lenses:** Creative lenses carry a higher risk of persona simulation than philosophical lenses. A philosophical agent that "speaks like Aristotle" is distracting but rarely harmful. A creative agent that "speaks like Miles Davis" is actively misleading — it simulates personality rather than applying methodology. The tone section must calibrate register and confidence posture without adopting the source's personal voice. The agent speaks *through* the framework, not *as* the creator.

For practice-type sources (Kintsugi, Wabi-sabi), the tone risk is different: romanticization. The agent should not describe software artifacts in reverent, contemplative language that belongs to the craft tradition. Clinical precision is more honest than borrowed poetry.

---

### 2.11 Composition Guidance — INHERITED

Structurally identical to Thinker Profile Spec §2.11. No modifications.

**Composition note for creative lenses:** The most productive compositions pair creative and philosophical lenses — these produce findings that neither tradition generates alone. Creative-to-creative pairings risk overlapping medium assumptions. Creative-to-philosophical pairings produce genuine cognitive parallax because the two traditions don't share a common register.

Priority composition pairings to document:

| Pairing Type | What It Produces | Example |
|---|---|---|
| Creative ↔ Philosophical (Adversarial) | Productive tension between arrangement and purpose/evidence/falsifiability | Rams Analyst ↔ Gap Analyst: "Remove this" vs. "This is structurally required" |
| Creative ↔ Philosophical (Sequential) | Creative analysis enriched by philosophical rigor, or vice versa | Kintsugi Explorer → Aristotle Analyst: Find repairs, then ask if repairs serve telos |
| Creative ↔ Meta-Layer (Complementary) | Creative perspective on meta-analytical blind spots | Picasso Analyst → Bias & Prejudice Detector: Multi-perspective rendering reveals default perspective |
| Creative ↔ Creative (Parallel) | Compositional parallax — how different creative logics read the same artifact | Rams ∥ Brutalism: Minimal harmony vs. assertive honesty on the same spec |

---

### 2.12 Role-Specific Elaborations — INHERITED (EXTENDED)

Structurally identical to Thinker Profile Spec §2.12, but the role list is extended to include Generator and Executor.

**Contents:** One subsection per planned role, each containing:

- **Role fit assessment** — Why is this source's creative operation suited to this role? What aspect of the machinery maps to the role's function?
- **Role-specific characteristic moves** — Do any moves from §2.3 change when operating in this role? Do any moves change register? (A move that is analytical in the Analyst role may become transformative in the Generator role.)
- **Role-specific output modifications** — How does the output structure (§2.9) change for this role?
- **Role-specific failure signatures** — Are there failure modes unique to this source × role combination?

**Generator-specific elaboration requirements:**
- What artifact does the Generator produce? A reduced version? A systematized version? A re-rendered version? A version from an alternative perspective?
- What are the constraints on generation? The Generator cannot produce arbitrary artifacts — it must produce artifacts that embody the lens's principles under stated constraints.
- How is the generated artifact verified? What makes a Rams-reduced API spec *valid* (all use cases preserved) versus *mutilated* (essential functionality removed)?
- What is the relationship between the generated artifact and the original? Reduction (subset)? Translation (same content, different structure)? Synthesis (new structure from pattern extraction)?

**Executor-specific elaboration requirements:**
- What transformation does the Executor perform?
- What are the completion criteria? How does the Executor know it's done?
- What is the rollback strategy? If the transformation breaks something, what is the undo path?
- What safeguards prevent the creative operation from exceeding its scope? A Rams Executor that removes "ornamental" code needs guardrails preventing it from removing code that is essential but *looks* ornamental.

**Conditional:** Only include roles listed in the library spec's Priority Roles for this source. Do not speculatively elaborate roles that aren't planned.

---

### 2.13 Exemplar Findings — INHERITED

Structurally identical to Thinker Profile Spec §2.13. No modifications.

**Exemplar note for creative lenses:** Exemplar findings should include at least one finding from each active move register. If the lens has analytical, perspectival, and transformative moves, the exemplars should demonstrate what each register produces. A profile with only analytical exemplars hasn't demonstrated its creative-specific capabilities.

---

### 2.14 Creative Adaptations to Inherited Sections — REFERENCE

This section does not contain profile content. It documents, for profile authors, where the inherited sections (§2.4–§2.13) require creative-specific attention that goes beyond the Thinker Profile Spec's guidance. These notes are summarized within each inherited section above and collected here for reference:

| Section | Creative Adaptation |
|---|---|
| §2.4 Decision Vocabulary | Additional quality test: vocabulary must describe compositional/material quality, not logical quality |
| §2.5 Failure Signatures | Must include Medium Leakage failure signature |
| §2.6 Key Definitions | Must distinguish native-medium vs. translated vocabulary |
| §2.7 Reference Knowledge | Generator/Executor roles demand higher depth than Analyst |
| §2.8 Process Architecture | Must specify register transitions between phases |
| §2.9 Output Structure | Generator and Executor need new section labels |
| §2.10 Tone & Voice | Higher persona simulation and romanticization risk |
| §2.11 Composition Guidance | Creative ↔ philosophical pairings are highest priority |
| §2.12 Role Elaborations | Generator and Executor roles need additional fields |
| §2.13 Exemplar Findings | Should include exemplars from each active move register |

---

## 3. ADL Field Mapping Summary

| Profile Section | ADL Field(s) | Notes |
|---|---|---|
| 2.0 Front Matter | `interface` (name, version, displayName, agentType, domain, tags) | `domain: cognitive-lens`; `tags` should include source type and native medium |
| 2.1 Creative Identity | `interface.description`, `mission`, `context`, `knowledge_base` | Medium Translation maps primarily to `knowledge_base` |
| 2.2 Core Principles | `cognitive_lens.core_axioms[]` | ADL field retains `core_axioms` name for schema compatibility |
| 2.3 Characteristic Moves | `process` steps, `knowledge_base` | Move Register informs process step metadata |
| 2.X Compositional Logic | `knowledge_base`, `process`, `scoring` (Validators) | Compositional principles → reference knowledge; arrangement grammar → scoring criteria |
| 2.4 Decision Vocabulary | `decisions`, `mission` | Same mapping as Thinker Profile |
| 2.5 Failure Signatures | `cognitive_lens.failure_signatures[]`, `edge_cases` | Same mapping; Medium Leakage is a required entry |
| 2.6 Key Definitions | `knowledge_base`, `context` | Same mapping |
| 2.7 Reference Knowledge | `knowledge_base` | Same mapping |
| 2.8 Process Architecture | `process` | Same mapping |
| 2.9 Output Structure | `output`, `output.implications` | Generator/Executor use extended labels |
| 2.10 Tone & Voice | `tone` | Same mapping |
| 2.11 Composition Guidance | `composition` | Same mapping |
| 2.12 Role-Specific Elaborations | Per-role ADL definition overrides | Generator and Executor produce separate ADL files |
| 2.13 Exemplar Findings | `knowledge_base` safe patterns, test calibration | Same mapping |

---

## 4. Quality Criteria

A Creative Lens Profile is ready for encoding when:

### 4.1 Completeness

- [ ] All mandatory sections (§2.0–§2.13) are populated, including new sections (§2.1 Medium Translation, §2.X Compositional Logic)
- [ ] Core principles number 3–7, each with implications (in software terms) and tension points
- [ ] Characteristic moves number 4–8, each with move register declared and traceable to a principle
- [ ] At least one characteristic move operates in a non-analytical register (perspectival or transformative)
- [ ] Decision vocabulary includes criteria, threshold question, and edge cases
- [ ] Failure signatures number 2–5, each with mechanism, recognition pattern, and mitigation
- [ ] Failure signatures include a Medium Leakage entry
- [ ] Key definitions number 5–15, with native-medium vs. translated vocabulary clearly marked
- [ ] Reference knowledge includes common mistakes, red flags, and safe patterns
- [ ] Process architecture specifies a named methodology with register transitions documented
- [ ] Compositional logic includes 3–5 arrangement principles with software translations
- [ ] Output structure defines sections, finding format, and implications section
- [ ] Composition guidance includes at least one creative ↔ philosophical pairing

### 4.2 Specificity

- [ ] No section could apply unchanged to a different creative source in the library
- [ ] The creative operation is described concretely enough for someone unfamiliar with the source to understand
- [ ] Common mistakes and red flags are ones an LLM would actually produce, not ones a design student would make
- [ ] Exemplar findings (if present) demonstrate unique visibility — findings that only this lens would produce
- [ ] Medium Translation produces software-specific observations, not metaphorical observations with aesthetic labels

### 4.3 Internal Consistency

- [ ] Every characteristic move traces back to at least one principle
- [ ] Every failure signature traces back to a specific strength taken too far
- [ ] The process architecture uses the characteristic moves in a coherent sequence with register transitions
- [ ] The decision vocabulary criteria align with what the process architecture produces
- [ ] The output structure has a place for everything the process produces, including non-analytical register outputs
- [ ] The compositional logic principles are consistent with the core principles

### 4.4 Differentiation

- [ ] "What This Is Not" (§2.1) names specific other library entries (both philosophical and creative) and states clear distinctions
- [ ] No principle is a truism (a different creative lens could disagree)
- [ ] No characteristic move is generic (another lens could not perform the same operation)
- [ ] The decision vocabulary captures something PASS/FAIL would lose
- [ ] The compositional logic differs from other creative lenses with shared principles

### 4.5 Encodability

- [ ] Every section maps to at least one ADL field (per §3)
- [ ] No section requires interpretive judgment beyond what the profile specifies
- [ ] The process architecture is mechanical enough to follow — steps produce defined outputs
- [ ] Tone guidance is specific enough to produce recognizably different agent voice
- [ ] Generator and Executor role elaborations (if planned) include constraints, verification, and rollback

### 4.6 Medium Translation Fidelity — NEW

- [ ] Every core principle has an explicit software translation with a concrete example
- [ ] At least one principle is documented as having an imperfect or partial translation
- [ ] The translation produces genuinely different observations — removing the creative vocabulary leaves substantive analysis intact
- [ ] Native-medium language appears only in definitions and explanatory context, not in the process architecture or output structure
- [ ] The "where the translation breaks" subsection identifies at least one gap

---

## 5. Anti-Patterns

### 5.1 The Wikipedia Profile — INHERITED

Same as Thinker Profile Spec §5.1. Describes the source rather than what the lens does to an artifact.

### 5.2 The Vocabulary Decorator — INHERITED

Same as Thinker Profile Spec §5.2. Uses the creative framework's terminology without its thinking.

### 5.3 The Omniscient Lens — INHERITED

Same as Thinker Profile Spec §5.3. Failure signatures are perfunctory or absent.

### 5.4 The Clone Profile — INHERITED

Same as Thinker Profile Spec §5.4. Two creative profiles from the same tradition are structurally identical with minor vocabulary substitutions. Especially important for creative lenses that share a native medium: Rams and Bauhaus, Kintsugi and Wabi-sabi, Jazz and Blues.

### 5.5 The Metaphor Profile — NEW

**Symptom:** The entire profile operates through metaphor. "Code should breathe like jazz." "APIs should have the proportions of good furniture." "This specification has no negative space." The metaphors are evocative but the agent wouldn't know what to *do*. The process architecture says "assess the artifact's rhythm" without specifying what "rhythm" means in a codebase, how to detect it, or what finding to produce when it's absent.

**Root cause:** The Medium Translation was skipped or performed at the metaphorical level rather than the operational level. The author described the *feeling* of applying the creative lens instead of the *procedure*.

**Fix:** For every metaphorical principle, state the literal software operation it maps to. "Rhythm" in a codebase might mean: alternation of interface definitions and implementations, regular patterns of test-beside-source, consistent module structure across a directory. If the literal operation can't be stated, the metaphor isn't translatable — document it in the "where the translation breaks" subsection and remove it from the process architecture.

### 5.6 The Persona Profile — NEW

**Symptom:** The agent definition simulates the creative source's personality rather than applying its methodology. A Miles Davis agent that speaks in cool, detached jazz-inflected prose. A Rams agent that is fastidiously tidy in its output formatting. A Kintsugi agent that describes findings with wistful reverence. The output is cosplay, not analysis.

**Root cause:** The Tone & Voice section was written to capture the source's *personality* rather than the framework's *communication register*. This is especially tempting for individual-type sources with strong personal identities.

**Fix:** The tone section describes how the *framework* naturally expresses its observations, not how the *person* would speak. A Rams-framework agent naturally says "this abstraction adds indirection without adding function" — that's framework-native observation. A Rams-personality agent says "we must have the courage to remove" — that's persona simulation. The quality test: if the source's name were removed from the output, would the reader mistake the agent for a personality chatbot or for a specialized analytical tool? It should be the latter.

### 5.7 The Untranslated Profile — NEW

**Symptom:** The profile's core principles, characteristic moves, and process architecture operate entirely in the native medium's vocabulary. "Evaluate the visual weight of each component." "Assess whether the golden ratio applies to the layout." "Map the color temperature of the error handling." The profile has not been translated — it has been transplanted, and the agent will produce native-medium judgments about a software artifact that doesn't exist in that medium.

**Root cause:** The Medium Translation section exists but was treated as a preamble rather than as the foundation every subsequent section must build on. The principles, moves, and process were written first (in native-medium terms) and the translation was added as a preface.

**Fix:** Reverse the authoring order. Write the Medium Translation first. Then derive the principles, moves, and process architecture from the translated operations. If a principle can only be expressed in native-medium terms, it hasn't been translated yet. The native-medium vocabulary belongs in §2.6 (Key Definitions) as reference — the rest of the profile operates in translated vocabulary.

---

## 6. Versioning and Lifecycle

### 6.1 Profile Versioning

Same as Thinker Profile Spec §6.1. Semantic versioning with MAJOR (fundamental change to creative identity or core principles), MINOR (new moves, revised reference knowledge, additional role elaborations), PATCH (corrections, clarifications, improved examples).

### 6.2 Profile-to-ADL Traceability

Same as Thinker Profile Spec §6.2. Each ADL definition includes source profile reference in its `context` block.

### 6.3 Lifecycle States

Same as Thinker Profile Spec §6.3:

```
Draft → Review → Validated → Encoded → [Profile updated → Re-review → Re-encoded]
```

**Additional lifecycle note for creative lenses:** The Expert Fellowship Program is even more important for creative profiles than for philosophical ones. Philosophical operations have extensive secondary literature for verification. Creative operations often have less structured documentation — the knowledge lives in practice, critique, and apprenticeship. A practicing industrial designer reviewing a Rams profile, or a ceramicist reviewing a Kintsugi profile, provides verification that secondary literature cannot.

---

## 7. Design Decisions

### 7.1 Sibling spec rather than fork — RESOLVED

**Decision:** The Creative Lens Profile Spec is a sibling of the Thinker Profile Spec, sharing structure through inheritance-by-reference rather than duplication.

**Rationale:** The two specs share ~80% of their structure. Duplicating the shared sections would create a maintenance burden — any improvement to the Thinker Profile Spec's common sections would need to be replicated here. Inheritance-by-reference means the shared sections evolve together. The creative-specific sections (Medium Translation, Core Principles, Move Register, Compositional Logic) are clearly marked as new or modified. If the two specs diverge enough to warrant full separation, that's a future refactoring.

### 7.2 Three source types from the start — RESOLVED

**Decision:** Support Individual, Practice, and School source types immediately rather than deferring Practice and School types (as the Thinker Profile Spec deferred School-level profiles per §7.4).

**Rationale:** Practices (Kintsugi, Wabi-sabi) and movements (Bauhaus, Brutalism) are among the most immediately valuable creative lenses. Deferring them would delay the most interesting entries. The profile structure accommodates all three types with minimal variation — the Front Matter declares the source type, and the Cognitive Identity section adjusts its attribution accordingly. Individual sources attribute to a person. Practice sources attribute to the tradition. School sources attribute to the movement and may later specialize via fork.

### 7.3 Move Register as profile field, not ADL schema change — RESOLVED

**Decision:** The Move Register (analytical, perspectival, transformative) is documented in the profile and informs ADL encoding, but does not require an ADL schema change in v1.10.0.

**Rationale:** The register is a design property that affects how process steps are written and how output is structured, but it doesn't require a new ADL field to function. The `process` block's step descriptions can express register naturally: "Phase 2: Render the artifact from the operator's perspective [perspectival]." If production data shows that register needs formal schema support (e.g., for automated output format adaptation), an ADL v1.11.0 change can add it. Schema changes should follow evidence, not speculation.

**Revisit condition:** If the first three creative profiles all struggle with register expression in the process block, the schema change should be reconsidered.

### 7.4 Generator and Executor roles included — RESOLVED

**Decision:** Document Generator and Executor roles for creative lenses despite zero production data for cognitive-lens Generators/Executors.

**Rationale:** Creative lenses' primary value proposition over philosophical lenses is that they *make*, not just analyze. Excluding Generator and Executor from the profile spec would defer the most differentiating capability. The planning agent family has validated these roles in the software domain. The creative lens extension adds a new *source of generation logic* (creative principles rather than analytical findings), not a new role mechanic. The ADL schema already supports both roles.

### 7.5 Medium Translation as load-bearing section — RESOLVED

**Decision:** Medium Translation is treated as the profile's most important section, with the strictest quality criteria.

**Rationale:** Every other section depends on it. If the translation is vague or metaphorical, the principles become decoration, the moves become generic, the process becomes a costume worn over standard analysis, and the output becomes vocabulary-decorated findings. The Medium Translation is where the creative profile either works or fails. It should be written first and reviewed most critically.

### 7.6 Compositional Logic as separate section — RESOLVED

**Decision:** Compositional Logic is a standalone section (§2.X) rather than a subsection of Core Principles (§2.2) or Reference Knowledge (§2.7).

**Rationale:** Compositional Logic is genuinely new conceptual content, not a specialization of existing content. Principles are *commitments* about the relationship between form and function. Compositional Logic is a *grammar* of arrangement — it describes relationships between elements, not properties of elements. It could have been embedded in Reference Knowledge, but it's load-bearing for Validators (where it becomes scoring criteria) and for Generators (where it becomes production constraints), and it's the section that most differentiates creative lenses from philosophical ones. It deserves first-class status.

---

## 8. Initial Build Recommendations

Based on analysis of maximum diversity across source type, move register, native medium, and primary agent role:

### 8.1 First Build: Dieter Rams (Individual, Industrial Design)

**Why first:** Most crisply encodable. Ten published principles already structured like axioms. Medium translation from industrial design to software is well-trodden (the "clean code" and "Unix philosophy" movements are essentially applied Rams without attribution). Analyst builds first (familiar territory), then Generator (proof-of-concept for creative generation — a Rams Generator that takes an overbuilt spec and produces a reduced alternative).

**Primary roles:** Analyst, Generator
**Primary register:** Analytical (Analyst), Transformative (Generator)
**Decision vocabulary:** ESSENTIAL / ORNAMENTAL
**Validates:** Medium Translation fidelity, Generator role viability

### 8.2 Second Build: Kintsugi (Practice, Ceramics / Japanese Craft)

**Why second:** Most orthogonal to everything in the philosophical library. No philosopher asks "where was this broken and how did it heal?" Strongest candidate for Explorer type, where creative lenses most differentiate from philosophical ones. Practice source type tests whether the profile structure handles non-individual creative sources.

**Primary roles:** Explorer, Analyst
**Primary register:** Analytical (Analyst), Perspectival (Explorer — re-presents the system through its repair history)
**Decision vocabulary:** HONORED / CONCEALED
**Validates:** Practice source type, Explorer role, creative ↔ philosophical composition (Kintsugi Explorer → Aristotle Analyst)

### 8.3 Third Build: Picasso / Cubism (Individual, Visual Art)

**Why third:** Structurally isomorphic to cognitive parallax — the library's most validated composition pattern. Proof case for the perspectival output register. Immediately plugs into existing composition workflows.

**Primary roles:** Analyst, Explorer
**Primary register:** Perspectival (primary for both roles)
**Decision vocabulary:** INTEGRATED / PRIVILEGED
**Validates:** Perspectival register viability, multi-perspective as single-lens operation, composition with cognitive parallax

### 8.4 Exit Criteria for Creative Lens Proof of Concept

The creative lens expansion is validated when:

- [ ] At least one creative profile has been encoded to ADL and run in production
- [ ] The Medium Translation section produced software-specific findings (not metaphorical decoration)
- [ ] At least one non-Analyst role (Generator or Explorer) has been built and run
- [ ] At least one creative ↔ philosophical composition has been executed, producing findings neither lens generates alone
- [ ] The Move Register field has been tested in practice — do multi-register processes produce coherent output?
- [ ] No ADL schema changes were required (or if they were, they've been scoped and documented)

---

## 9. Open Questions

1. **Register formalization** — The Move Register (analytical, perspectival, transformative) is currently a profile-level design property. If production data shows it needs ADL schema support, what's the minimal schema change? A `register` field on process steps? A `register` field on the output block? Both?

2. **Compositional Logic as scoring criteria** — For Validator roles, the Compositional Logic section naturally maps to scoring categories. But compositional quality is harder to quantify than logical quality. How should compositional Validators score? Weighted categories (like philosophical Validators), or a different scoring model?

3. **Generator output verification** — A Rams Generator produces a reduced artifact. A Bauhaus Generator produces a systematized artifact. How is the generated artifact verified? Human review? Automated test pass? A Validator downstream in a pipeline? The verification strategy may need to be role-specific or lens-specific.

4. **Creative ↔ creative composition value** — The spec prioritizes creative ↔ philosophical pairings. Are creative ↔ creative pairings productive, or do they overlap too much? Production data needed. Candidate test: Rams ∥ Kintsugi on the same artifact — does reductive analysis + repair mapping produce divergent findings?

5. **Fork mechanism for practitioner-authored lenses** — The Expert Fellowship Program is the natural vehicle for practitioner-encoded creative lenses. What minimal profile structure is required for a fork? Full profile? Abbreviated profile? Does the fork mechanism need creative-specific adaptations (e.g., Medium Translation is mandatory even for forks)?

6. **Living creative practices** — Some creative traditions are actively practiced and evolving (Kintsugi, various design disciplines). The same question applies as for living philosophical traditions (Library Spec Open Question #7): freezing the cognitive operation at a historical moment may misrepresent a living practice. How should the profile handle this? Version the tradition with a date? Explicitly scope which interpretation of the practice is being encoded?

---

## 10. Changelog

### v0.1.0 — March 14, 2026
- Initial specification
- 13 profile sections defined (§2.0–§2.13), with 3 new sections (§2.1 Medium Translation, §2.2 Core Principles, §2.X Compositional Logic) and 2 modified sections (§2.3 Move Register, §2.12 Extended Roles)
- ADL field mapping table (§3)
- Quality criteria checklist with new §4.6 Medium Translation Fidelity
- 7 anti-patterns documented (4 inherited, 3 new: Metaphor Profile, Persona Profile, Untranslated Profile)
- Versioning and lifecycle defined (§6)
- 6 design decisions resolved (§7)
- 3 initial build recommendations with exit criteria (§8)
- 6 open questions documented (§9)

---

*Prepared by Alex Self, Ulu Labs Inc. For internal use and Cognitive Lens Library development.*
