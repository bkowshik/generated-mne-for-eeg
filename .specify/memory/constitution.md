<!--
SYNC IMPACT REPORT
==================
Version change: 2.0.0 → 2.0.1
Bump rationale: PATCH — clarification only. Principle II's "Total notebook count is
unbounded" was tightened to a soft cap of ~50 for the first iteration, with an
explicit cross-link back to Principle IV (Curated EEG-Only Scope) so that hitting
the cap acts as a scope-discipline signal rather than a hard ceiling. No principle
was added, removed, or redefined; no governance rule changed.

Principles: unchanged from 2.0.0.
- I.   Beginner-to-Advanced Journey
- II.  One Concept Per Notebook                 (wording tightened)
- III. Show, Don't Tell (Visual & Example-Driven)
- IV.  Curated EEG-Only Scope

Added sections: None.
Removed sections: None.

Templates / artifacts requiring updates:
- ✅ .specify/templates/plan-template.md — No edit needed; Constitution Check
  resolves at plan-time against current text.
- ✅ .specify/templates/spec-template.md — No principle-specific bindings.
- ✅ .specify/templates/tasks-template.md — Compatible.
- ✅ CLAUDE.md — Minimal; no references to amend.

Deferred items: None. Ratification date unchanged (2026-05-07); Last Amended
remains 2026-05-07 (same-day clarification of v2.0.0).
-->

# The Generated Guide to MNE for EEG Constitution

## Core Principles

### I. Beginner-to-Advanced Journey

The guide MUST be structured as a single coherent journey: a reader who arrives with
only a basic background in EEG (knows what an electrode, a trial, and an event are)
should be able to start at chapter one and progress to advanced MNE workflows by
following the chapters in order. Concepts MUST be introduced layer by layer — no
chapter may open with a fully-realized end-to-end pipeline before its constituent
concepts have been taught. Tone MUST favor "fun and approachable" over formal; learning
momentum is the primary success metric, not exhaustive correctness. Where a clean
explanation and a maximally rigorous explanation conflict, the clean one wins, with a
brief pointer to deeper material for readers who want it.

**Rationale**: This is a guide, not a textbook or a paper. The author's explicit goal
is to take readers on a journey from beginner to intermediate to advanced — that goal
collapses if the early chapters are intimidating, and it collapses just as fast if
later chapters never escape the basics.

### II. One Concept Per Notebook

The guide is delivered as nbdev notebooks. Each notebook MUST teach exactly one
concept that is (a) important for working with EEG data and (b) realized by a
specific feature of MNE-Python. Notebooks MUST be kept small enough that the whole
concept fits in one place — a reader should be able to read, run, and re-edit a
notebook in a single sitting. Splitting a concept across notebooks is FORBIDDEN;
bundling multiple concepts into one notebook is FORBIDDEN. Total notebook count is
soft-capped at ~50 for the first iteration of the guide — many small notebooks are
preferred to a few large ones, but if a candidate notebook would push the count
past ~50 it is a signal to re-check Principle IV (Curated EEG-Only Scope) and
either drop a less-essential notebook or defer the new one to a later iteration.

**Rationale**: One-concept-per-notebook is what makes nbdev a good fit: notebooks
become individually editable, individually runnable, and individually skippable. It
also keeps each unit of learning bounded so the reader gets a "win" finishing each
one. Large notebooks are harder to maintain and harder to learn from.

### III. Show, Don't Tell

Every concept MUST be taught primarily through worked examples and visualizations,
not prose definitions. Each notebook MUST contain at least one runnable code example
producing at least one figure (plot, topomap, raw trace, time-frequency
representation, etc.) that illustrates the concept. Prose exists to frame the
example, not to substitute for it. When a written description and a figure could
both convey a point, the figure wins; the prose annotates it.

**Rationale**: The author is a visual learner and is writing for readers like
themselves. EEG is an inherently visual domain — the field thinks in waveforms,
topomaps, and time-frequency plots — so teaching it without dense visuals is
needlessly hard.

### IV. Curated EEG-Only Scope

Coverage MUST be curated, not exhaustive. Before drafting, every proposed notebook
MUST be justified by answering: "Is this among the most important MNE features for a
practitioner working with EEG data?" If not, it is out of scope for the first
iteration. MNE features specific to other modalities (MEG, fNIRS, sEEG, ECoG, source
localization that materially relies on MEG-style sensors, etc.) MUST NOT be covered
here unless they are unavoidable to make an EEG concept land. Out-of-scope topics
MAY be acknowledged with a one-line pointer to the upstream MNE docs but MUST NOT
get their own chapter.

**Rationale**: MNE is large and mature; trying to cover it all guarantees the guide
never ships. Focusing on EEG specifically — and on the high-leverage subset of
MNE for EEG — gives the guide a defensible scope and gives readers a clear
expectation of what they will and will not learn.

## Tooling & Runtime

- **Notebook framework**: The guide is built with nbdev. Each chapter corresponds to
  a single nbdev notebook; chapter ordering is captured in the nbdev sidebar/index.
- **Runtime**: The canonical runtime is Google Colab. Notebooks MUST be runnable on
  a fresh Colab instance with only `pip install` setup cells the reader is told to
  execute. A "Open in Colab" badge SHOULD be added once the publishing flow is in
  place; the reader's path from "found the guide" to "running the first cell"
  should be one click plus one Run-all.
- **Local runtime**: Running notebooks locally is supported but not the canonical
  path; if local-only steps are unavoidable they MUST be marked clearly.
- **Dependencies**: MNE-Python and any direct dependencies SHOULD be installed at
  whatever version Colab carries by default unless a specific version is required
  for the example to work; in that case the version is pinned in the install cell
  with a one-line reason. Strict reproducibility (matching figures byte-for-byte
  across years) is NOT a goal of this guide.
- **Datasets**: Examples MUST use either MNE's bundled sample loaders
  (`mne.datasets.*`) or other openly downloadable datasets that work end-to-end
  inside Colab without authentication. Anything requiring user-supplied data is
  unsuitable for this guide.

## Authoring & Review Workflow

- **Scope gate (before authoring)**: Every new notebook starts with a one-paragraph
  pitch answering: (a) what single concept does this teach? (b) which MNE feature
  carries it? (c) why is it among the most important features for EEG? If any of
  the three is weak, the notebook is deferred or dropped, not written.
- **Author checklist (before merge)**:
  1. The notebook runs top-to-bottom on a fresh Colab instance.
  2. The notebook teaches exactly one concept (Principle II).
  3. The notebook contains at least one figure illustrating that concept
     (Principle III).
  4. The notebook fits in the journey: it does not assume content from a notebook
     that has not yet been written, and it does not duplicate something an earlier
     notebook already taught (Principle I).
  5. The notebook stays inside EEG scope (Principle IV); cross-modality digressions
     are removed or boxed off.
- **Accuracy and citations** (best effort, not a gate): Where a claim has a clean
  source — an MNE tutorial, an MNE API page, a well-known reference — link it.
  Missing a citation is not a blocker; making something up is.
- **Chapter sizing**: If a draft notebook grows past what feels editable in one
  sitting, the author MUST split it along its natural concept boundary rather than
  shipping the large version.

## Governance

This constitution supersedes ad-hoc preferences. Where a review comment conflicts
with a principle here, the principle wins unless the constitution is amended.

**Amendment procedure**: Proposed changes MUST be raised as a pull request that
edits this file and includes the Sync Impact Report block at the top. Amendments
require approval from at least one maintainer with a brief rationale. Drive-by
wording fixes MAY ship as PATCH bumps.

**Versioning policy**: This document follows semantic versioning.
- MAJOR: Principles removed, redefined, or scope narrowed/widened in a way that
  invalidates existing notebooks.
- MINOR: New principle or materially expanded section.
- PATCH: Wording, typo, or clarification fixes that do not change meaning.

**Compliance review**: Every `/speckit-plan` invocation runs a Constitution Check
gate against the principles above; violations MUST be either resolved or recorded
in the plan's Complexity Tracking table with explicit justification. Periodic
audits (at least once per MINOR content release) reread the published guide
against this document and open issues for drift — especially scope drift away
from EEG and chapter-bloat drift away from one-concept-per-notebook.

**Runtime guidance**: Day-to-day authoring guidance — install commands, the active
nbdev configuration, Colab-specific gotchas — lives in the project README and the
active feature plan (`specs/<feature>/plan.md`), not here. This file governs *what*
the work must satisfy; those documents describe *how* to do it.

**Version**: 2.0.1 | **Ratified**: 2026-05-07 | **Last Amended**: 2026-05-07
