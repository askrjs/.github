# AGENTS.md

Operational guide for organization-wide Askr contribution policy and templates.

## Scope

This repository owns the guidance inherited by Askr repositories. Keep it
package-neutral; implementation details belong in the repository that owns the
behavior.

## Askr North Star

Askr is an opinionated, batteries-included framework for building apps that
stay understandable to the human who owns them and the agent that edits them as
both keep changing the code.

- Prefer a causal flow a reader can narrate over a clever mechanism that is
  merely faster or more flexible.
- Enforce important invariants at runtime with specific errors that identify
  the misuse and the corrective action.
- Define and test the distinguishable failure modes of every new primitive.
- Keep package seams visible; included packages must remain independently
  understandable.
- Prefer explicit configuration over inference when inference would make
  behavior harder to predict.
- Treat every new API, option, and escape hatch as a lasting legibility cost.
- Do not pursue fine-grained reactivity, ecosystem parity, or configurability
  as goals independent of a demonstrated Askr application need.

An implementation is ready only when its behavior has a one-sentence causal
explanation, misuse is caught where it occurs, errors tell a context-free reader
how to fix the problem, tests cover failure paths, and documentation describes
the behavior without an unacknowledged limitation.

## Validation

Review the inherited contribution policy and pull request template together.
Keep their readiness questions aligned whenever either changes.

## Optimization Gate

A benchmark number is only half of an optimization's success criterion. The
change must also preserve a causal path that a human or agent can narrate in one
sentence.

Every benchmark-driven change must include:

1. the one-sentence causal description of the optimized path;
2. the exact fallback trigger and proof that optimized and fallback paths have
   identical observable behavior and error surfaces;
3. an explicit legibility-cost statement, including `none` when no new path or
   concept is introduced; and
4. evidence that a measured bottleneck in a real application justifies the
   optimization now.

Prefer making the existing single path faster. New caches, inference,
memoization, shortcuts, fast paths, or scheduler states require an explicit
legibility decision; a speedup alone does not justify them.
