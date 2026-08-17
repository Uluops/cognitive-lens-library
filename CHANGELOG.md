# Changelog

All notable changes to the Cognitive Lens Library are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

> **Note on provenance.** This repository is a curated public mirror. Profiles are authored
> upstream and copied here, which means it can drift from its source without anything
> failing — no build reads these files and no check compares them. Both entries below are
> instances of exactly that. This changelog exists so the next drift is at least legible
> after the fact; it starts at 2026-08-17 and does not reconstruct history before that date.

## [Unreleased]

### Added — Husserl, Heidegger and Ibn Khaldūn, closing a three-profile mirror gap

All three had been authored and committed upstream, and all three have shipping agent
definitions — 3 for Husserl, 2 for Heidegger, 3 for Ibn Khaldūn. None had ever reached this
mirror. The lenses were reachable in the product while the public library said they did not
exist.

Two new sections were added to hold them rather than stretching an existing one:

- **Phenomenology** — Husserl (Transcendental Phenomenology, 0.1.0) and Heidegger
  (Fundamental Ontology / Existential Phenomenology, 0.2.0). The two profiles were written
  deliberately against each other as a divergence test: Husserl reads *constitution and
  fulfillment* (the design solicits X and delivers Y), Heidegger reads *breakdown and
  disclosure* (the abstraction is invisible until it fails, and its failure either strands
  the user or teaches them). Shipping one without the other would have published half of a
  designed pair.
- **Islamic Golden Age** — Ibn Khaldūn (Historical Sociology / ʿIlm al-ʿUmrān, 0.2.0), the
  library's first lens that reads time as a one-way arc of cohesion rather than as flux,
  dialectical ascent, or paradigm lifecycle.

The README profile count moves 32 → 35.

**Verified before publishing:** every failure code cited across the three profiles is a
canonical member of the 28-mode taxonomy. The check was run with a two-sided control —
`STR-OMI` and `EPI-VER` must read canonical, `SEM-VER` and a bogus `ZZZ-QQQ` must not. An
earlier run of that same check was inert (it concatenated the domain onto an
already-qualified code, yielding `EPI-EPI-FAL`, so every code read as non-canonical) and was
discarded rather than trusted.

Foucault (0.1.0) exists upstream and is **not** included here: it has no agent definition
yet, and this mirror tracks profiles whose lenses are reachable.

### Fixed — Hume and Popper taught two invalid failure codes as worked examples

Both profiles illustrated the failure-code field with `(e.g., EPI-VER, SEM-VER, SEM-OMI)`.
`SEM-VER` and `SEM-OMI` are not members of the taxonomy: modes are bound to their domains,
so `EPI-VER` is a code and `SEM-VER` is not. Presenting the two alongside a valid `EPI-VER`
reads as confirmation that domain and mode compose freely — which is the misconception that
produces out-of-taxonomy codes at runtime, and this is authoring guidance in a public
library, so it was teaching that misconception to outside readers.

Corrected to `(e.g., EPI-VER, EPI-GRN, EPI-FAL)` — copied verbatim from the upstream
originals, which had already been fixed, so the two are byte-identical at these lines.

Control on the fix: grep for `SEM-VER|SEM-OMI` across `thinkers/` returns 0, while the same
grep for `EPI-VER` returns both files. Two zeros would have meant a broken search rather
than a clean repository.

## Known gaps

- **The README's "21 intellectual traditions" is not verifiable and was already inconsistent
  before these changes.** The profile tables list 30 distinct `Tradition` strings across 12
  sections. The profile *count* is checked and correct (35); the tradition count is left
  as-is because what counts as a "tradition" here is an editorial judgment, not something
  that can be derived from the tables. Flagged rather than silently changed to a number
  nobody chose.
- **Nothing detects mirror drift.** No build, test, or check compares this repository
  against its upstream source. The three-profile gap closed above went unnoticed for as long
  as it existed, and the same failure will recur silently on the next upstream profile.
