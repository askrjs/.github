# Contributing to Askr

Thanks for your interest in Askr. We welcome focused contributions from people
and organizations with a genuine connection to the project.

## Implementation North Star

**Askr is an opinionated, batteries-included framework for building apps that
stay understandable—to the human who owns them and the agent that edits them—as
both keep changing the code.**

Apply these rules to APIs, defaults, errors, implementation boundaries, tests,
and documentation:

- Prefer a mechanism a reader can narrate over one that is merely faster or
  more flexible. A change should have a one-sentence causal explanation.
- Enforce important invariants at runtime. The error must identify what was
  violated and tell a context-free reader how to correct it.
- Define and test the distinguishable failure modes of every new primitive;
  happy-path coverage alone is incomplete.
- Keep package and subsystem seams visible even when Askr includes and composes
  the pieces.
- Prefer explicit configuration over inferred convention when inference would
  make behavior harder to predict.
- Treat each new API, option, and escape hatch as a lasting legibility cost and
  require a demonstrated application need.

Do not pursue fine-grained reactive graphs, ecosystem parity, or configurability
as goals in themselves. Performance work is welcome when it preserves the
narratable causal model. If verified behavior has a limitation, document it
when the behavior ships rather than allowing implementation and documentation
to disagree.

### Optimization gate

A benchmark number is not a complete success criterion. A benchmark-driven
change must also preserve a causal path a human or agent can narrate in one
sentence. Optimization pull requests are incomplete without all four items:

1. **Optimized path:** the one-sentence causal description of what runs, what
   changes, and why.
2. **Fallback:** the exact condition that selects the fallback, plus tests
   proving that optimized and fallback paths have identical observable behavior
   and error surfaces.
3. **Legibility cost:** an honest statement of the additional path, state, or
   concept a maintainer must understand, including `none` when the change adds
   none.
4. **Need now:** evidence that this path is a measured bottleneck in a real
   application or production-representative workload. A percentage improvement
   alone is not justification.

Single-path algorithm and allocation improvements remain welcome when they add
no second behavior to learn. Fixing an existing fast-path divergence and making
scheduling or batching easier to explain are also aligned improvements. New
caches, inference, memoization, shortcuts, fast paths, or scheduler states must
make their legibility tradeoff explicit before implementation is approved.

## Who should contribute

Contributions should come from someone who is:

- using Askr in an application, library, tool, or learning project;
- evaluating Askr for a concrete project or technical requirement; or
- maintaining an integration, documentation effort, or community resource that
  directly supports Askr users.

Your project does not need to be public or commercial. In the pull request,
briefly explain which Askr package or behavior you are using or evaluating and
how the change helps that work. Do not include confidential information.

Askr repositories are not a venue for indiscriminate contribution campaigns,
reputation farming, agent benchmarks, or mass-generated changes from parties
with no meaningful interest in using or supporting Askr.

## Before opening a pull request

- Search existing issues and pull requests before starting work.
- For anything beyond a small bug fix, test, or documentation correction,
  discuss the change in an issue before implementing it.
- Keep the change focused on one problem and make it in the repository that
  owns the behavior.
- New contributors should keep one pull request open at a time unless a
  maintainer agrees to a broader set of work.
- Read the repository's local contribution guide and run its required checks.

## AI and automation

AI-assisted development and automation are welcome. They do not replace the
requirement for a genuine Askr connection or accountable human review.

If AI or automation materially helped create a contribution:

- disclose the tools and what they generated or changed;
- personally review every submitted line and verification claim;
- be able to explain the design, behavior, tests, and tradeoffs without
  delegating maintainer discussion to an unattended agent;
- verify that generated code, text, and assets have acceptable provenance and
  licensing; and
- remain available to address review feedback and regressions.

Automated accounts must identify the person or organization responsible for the
contribution. Do not open unattended or speculative pull requests, submit the
same generic cleanup across unrelated projects, or use Askr issues as inputs to
a mass contribution campaign.

## Pull request requirements

Every pull request must include:

- **Askr context:** what you are building, maintaining, or concretely
  evaluating with Askr;
- **Problem:** the user-visible problem or project need being addressed;
- **Change:** a focused explanation of the implementation;
- **Causal model:** one sentence describing what runs, what changes, and why;
- **Failure behavior:** misuse and failure modes, the runtime checks that catch
  them, and the actionable errors a user receives;
- **Optimization evidence, when benchmark-driven:** optimized path, fallback
  trigger and parity proof, legibility cost, and evidence that the bottleneck
  matters now;
- **Verification:** exact checks run and any checks not run;
- **Automation disclosure:** tools used and the extent of their involvement, or
  `None`; and
- **Follow-through:** timely, substantive responses to maintainer questions and
  review feedback.

Behavior changes need focused tests. User-visible changes need documentation.
Do not mix unrelated refactors, dependency updates, or generated-file churn
into the same pull request.

Before approval, reviewers should be able to answer yes to each question:

1. Can the behavior be narrated in one causal sentence without hidden
   qualifiers?
2. Is misuse caught at runtime where it occurs?
3. Does each error tell a reader with no prior context what to fix?
4. Does the design preserve legibility instead of trading it for raw speed,
   flexibility, or parity?
5. Do shipped docs match verified behavior and state any real limitation?

## The 0.2 compatibility line

The `0.2.x` line is Askr's compatibility-focused boring phase. Public contracts
include package exports and declarations, accepted inputs, runtime behavior and
ordering, lifecycle and cleanup, error categories, codes, and paths, CLI
behavior, generated specifications, accessibility semantics, CSS tokens, peer
requirements, and documented operating models.

Changes on this line are limited to fixes, documentation, diagnostics,
maintenance, compatible simplification, and narrowly demonstrated application
gaps. A new public primitive needs a real application, explicit failure modes,
actionable invariant checks, North Star review, and proof from a packed
consumer. Otherwise, defer it.

A breaking contract requires an approved RFC for a future compatibility line.
The RFC must document the application need, alternatives, legibility cost,
affected consumers, migration path, and a compatibility adapter or deprecation
when feasible. Optimization is not a reason to weaken invariants, change error
behavior, or add a hidden path without the optimization evidence above.

### Internal dependency ranges

Preserve how an existing Askr relationship is modeled and where it is declared:

- exact internal dependencies use the exact coordinated version;
- ranged internal dependencies use `>=0.2.0 <0.3.0` on the `0.2.x` line; and
- dependency fields, optionality, and package presence do not change merely for
  normalization.

Apply the rule consistently to `dependencies`, `devDependencies`,
`peerDependencies`, and `optionalDependencies`, regenerate lockfiles, and verify
that no direct Askr relationship retains a pre-line constraint.

### Release procedure

Published packages release independently after the coordinated `0.2.0`
baseline. Release only affected packages and required dependants, in dependency
order.

For each package:

1. merge the focused issue and draft pull request only after review and hosted
   checks are green;
2. build and exercise unit, integration, type, lint, documentation, package,
   installed-consumer, browser, example, server, and benchmark gates appropriate
   to that repository;
3. inspect the packed artifact and qualify registry dependencies from a clean
   installation;
4. publish the reviewed main commit with provenance;
5. verify npm metadata and installation, then verify that the release tag points
   to that same commit; and
6. update downstream consumers only after the upstream package is available to
   their hosted checks.

Three consecutive patch cycles using this workflow, with no escaped contract
regression, emergency republish, or unexplained benchmark failure, establish the
stable boring phase. Record each completed cycle; do not infer completion from
version numbers alone.

## Review and project trust

Contributions are evaluated on relevance, correctness, maintainability, and the
quality of collaboration—not on contribution count. Merged pull requests do not
by themselves establish eligibility for repository, release, or organization
access.

Maintainers may close contributions that lack genuine Askr context, omit
automation disclosure, misrepresent verification, duplicate ongoing work,
arrive as part of an indiscriminate campaign, or do not receive substantive
follow-up.

Repository-specific guides may add build, testing, documentation, and style
requirements. Those local requirements apply in addition to this policy.
