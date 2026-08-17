# Cognitive Lens Library

Philosophical and historical cognitive frameworks encoded as structured thinker profiles — the intermediate design artifact between a cognitive lens catalog entry and a deployable AI agent definition.

Each profile elaborates a thinker's cognitive machinery in enough detail that agent encoding becomes mechanical translation rather than creative interpretation. Axioms are articulated, characteristic moves are named, decision criteria are specified, failure modes are anticipated, and blind spots are documented.

## Pipeline Position

```
Library Spec Entry  →  Thinker Profile  →  ADL YAML  →  Rendered Agent Prompt
   (~20 lines)         (this repo)          (schema)       (runtime)

   WHAT & WHY          HOW (design)         HOW (formal)   HOW (execution)
```

## Profiles

35 thinker profiles across 21 intellectual traditions, plus 1 creative lens.

### Greek Classical & Pre-Socratic

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Aristotle](thinkers/aristotle-thinker-profile-v0_2_0.md) | Classical Philosophy | 0.2.0 | Validated |
| [Plato](thinkers/plato-thinker-profile-v0_1_0.md) | Classical / Academy | 0.1.0 | Draft |
| [Socrates](thinkers/socrates-thinker-profile-v0_1_0.md) | Classical / Athenian | 0.1.0 | Draft |
| [Archimedes](thinkers/archimedes-thinker-profile-v0_2_0.md) | Engineering-Mathematics | 0.2.0 | Draft |
| [Democritus](thinkers/democritus-thinker-profile-v0_1_0.md) | Pre-Socratic / Atomist | 0.1.0 | Draft |
| [Heraclitus](thinkers/heraclitus-thinker-profile-v0_1_0.md) | Pre-Socratic / Ephesian | 0.1.0 | Draft |

### Hellenistic & Roman Stoicism

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Epictetus](thinkers/epictetus-thinker-profile-v0_1_0.md) | Roman Stoicism | 0.1.0 | Draft |
| [Marcus Aurelius](thinkers/marcus-aurelius-thinker-profile-v0_1_0.md) | Roman Stoicism | 0.1.0 | Draft |
| [Seneca](thinkers/seneca-thinker-profile-v0_1_0.md) | Roman Stoicism | 0.1.0 | Draft |
| [Epicurus](thinkers/epicurus-thinker-profile-v0_1_0.md) | Hellenistic / Garden | 0.1.0 | Draft |

### Chinese Classical

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Confucius](thinkers/confucius-thinker-profile-v0_1_0.md) | Confucian | 0.1.0 | Draft |
| [Laozi](thinkers/laozi-thinker-profile-v0_1_0.md) | Daoist | 0.1.0 | Draft |
| [Sunzi](thinkers/sunzi-thinker-profile-v0_1_0.md) | Military Strategy | 0.1.0 | Draft |
| [Wang Yangming](thinkers/wang-yangming-thinker-profile-v0_1_0.md) | Neo-Confucian / School of Mind | 0.1.0 | Draft |
| [Zhu Xi](thinkers/zhu-xi-thinker-profile-v0_1_0.md) | Neo-Confucian / School of Principle | 0.1.0 | Draft |
| [Zhuangzi](thinkers/zhuangzi-thinker-profile-v0_1_0.md) | Daoist | 0.1.0 | Draft |
| [Mòzǐ](thinkers/mozi-thinker-profile-v0_1_0.md) | Mohism / Impartial Consequentialism | 0.1.0 | Draft |

### Indian Philosophical

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Nagarjuna](thinkers/nagarjuna-thinker-profile-v0_1_0.md) | Madhyamaka Buddhism | 0.1.0 | Draft |

### Islamic Golden Age

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Ibn Khaldūn](thinkers/ibn-khaldun-thinker-profile-v0_2_0.md) | Historical Sociology / ʿIlm al-ʿUmrān | 0.2.0 | Draft |

### Continental & German Idealism

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Descartes](thinkers/descartes-thinker-profile-v0_1_0.md) | Continental Rationalism | 0.1.0 | Draft |
| [Hegel](thinkers/hegel-thinker-profile-v0_1_0.md) | German Idealism | 0.1.0 | Draft |
| [Nietzsche](thinkers/nietzsche-thinker-profile-v0_1_0.md) | Post-Hegelian | 0.1.0 | Draft |
| [Machiavelli](thinkers/machiavelli-thinker-profile-v0_1_0.md) | Renaissance Political Philosophy | 0.1.0 | Draft |

### Phenomenology

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Husserl](thinkers/husserl-thinker-profile-v0_1_0.md) | Transcendental Phenomenology | 0.1.0 | Draft |
| [Heidegger](thinkers/heidegger-thinker-profile-v0_2_0.md) | Fundamental Ontology / Existential Phenomenology | 0.2.0 | Draft |

### Empiricism & Enlightenment

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Bacon](thinkers/bacon-thinker-profile-v0_1_0.md) | Empiricism / Scientific Method | 0.1.0 | Draft |
| [Hume](thinkers/hume-thinker-profile-v0_1_0.md) | Scottish Enlightenment / Empiricism | 0.1.0 | Draft |

### Philosophy of Science

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Popper](thinkers/popper-thinker-profile-v0_1_0.md) | Critical Rationalism | 0.1.0 | Draft |
| [Kuhn](thinkers/kuhn-thinker-profile-v0_1_0.md) | Historical Epistemology | 0.1.0 | Draft |

### American Pragmatism

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Peirce](thinkers/peirce-thinker-profile-v0_1_0.md) | Pragmaticism | 0.1.0 | Draft |
| [William James](thinkers/william-james-thinker-profile-v0_1_0.md) | Pragmatism | 0.1.0 | Draft |
| [Dewey](thinkers/dewey-thinker-profile-v0_1_0.md) | Instrumentalism | 0.1.0 | Draft |

### Analytic Philosophy

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Wittgenstein](thinkers/wittgenstein-thinker-profile-v0_1_0.md) | Ordinary Language | 0.1.0 | Draft |

### Systems Theory

| Profile | Tradition | Version | Status |
|---------|-----------|---------|--------|
| [Bateson](thinkers/bateson-thinker-profile-v0_1_0.md) | Cybernetics / Systems Theory | 0.1.0 | Draft |
| [Meadows](thinkers/meadows-thinker-profile-v0_1_0.md) | Systems Dynamics / Sustainability | 0.1.0 | Draft |

## Creative Lenses

Cognitive operations developed through *making* — design, composition, craft — rather than verbal-propositional reasoning. Unlike the thinker profiles, a creative lens carries a load-bearing **Medium Translation** step: the operation must survive the move from its native medium to software artifacts without collapsing into aesthetic decoration. Creative lenses follow the [Creative Lens Profile Specification](creatives/creative-lens-profile-spec-v0_1_0.md), a sibling of the Thinker Profile Spec.

| Profile | Native Medium | Tradition | Version | Status |
|---------|---------------|-----------|---------|--------|
| [Dieter Rams](creatives/dieter-rams-creative-lens-profile-v0_1_0.md) | Industrial Product Design | German Modernism / Braun School | 0.1.0 | Draft |

## Profile Structure

Each profile follows the [Thinker Profile Specification](thinkers/thinker-profile-spec-v0_1_0.md) and includes:

- **Cognitive Identity** — core operation, what distinguishes this lens from adjacent ones
- **Core Axioms** — foundational commitments with implications and tension points against other lenses
- **Characteristic Moves** — the specific analytical operations the lens performs
- **Decision Vocabulary** — the verdict language (e.g., TELEOLOGICAL/ATELEOLOGICAL, EMPTY/REIFIED, GROUNDED/UNGROUNDED)
- **Blind Spots** — what the lens structurally cannot see
- **Composition Affinity** — which other lenses complement, tension, or mitigate
- **Role-Specific Sections** — how the cognitive machinery maps to analyst, validator, explorer, and forecaster agent roles
- **Examples** — demonstrations of the lens applied to real artifacts

## Related

- [Agents & Pipelines](https://github.com/aself101/agents-and-pipelines) — Agent definitions, commands, and workflows that consume these profiles
- [UluOps](https://uluops.ai) — The platform infrastructure for versioning, tracking, and composing agents
- [Recursive Appreciation Hypothesis](https://docs.uluops.ai/concepts/recursive-improvement) — The research framework behind multi-lens composition

## License

This work is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). Copyright 2025-2026 Ulu Labs Inc.
