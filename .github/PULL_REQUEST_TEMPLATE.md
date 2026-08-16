## Askr context

<!--
What are you building, maintaining, or concretely evaluating with Askr?
Which package or behavior does this affect? Do not include confidential details.
-->

## Problem

<!-- Describe the user-visible problem or project need. -->

## Change

<!-- Explain the focused implementation and any important tradeoffs. -->

## Causal model

<!-- In one sentence: what runs, what changes, and why? -->

## Failure behavior

<!--
What misuse and failure modes exist? Which runtime checks catch them, and what
actionable correction does each error provide?
-->

## Optimization evidence

<!--
Complete this section for benchmark-driven changes; otherwise write "Not
benchmark-driven."

- Optimized path: one causal sentence.
- Fallback: exact trigger and behavioral/error-surface parity proof.
- Legibility cost: new path/state/concept, or "none."
- Need now: the real application or production-representative bottleneck.
-->

## Verification

<!-- List the exact checks run and explicitly identify anything not run. -->

## Automation disclosure

<!--
List any AI or automation tools that materially helped create this change and
what they generated or modified. Write "None" if no such tools were used.
-->

## Contributor checklist

- [ ] I am using Askr, maintaining an Askr integration or community resource,
      or evaluating Askr for a concrete project described above.
- [ ] I searched for existing issues and pull requests and kept this change
      focused on one problem.
- [ ] I personally reviewed every submitted line and verification claim.
- [ ] I disclosed material AI or automation assistance above, or wrote `None`.
- [ ] I can explain and maintain this change and will respond to review feedback.
- [ ] I added or updated tests and documentation when the change requires them.
- [ ] I can narrate the behavior in one causal sentence without hidden
      qualifiers.
- [ ] Important invariants are enforced at runtime with actionable errors, and
      failure paths are covered.
- [ ] The change keeps subsystem seams and configuration explicit and adds no
      speculative surface area.
- [ ] Documentation matches verified behavior and states any real limitation.
- [ ] If this is benchmark-driven, I documented the optimized path, fallback
      parity, legibility cost, and evidence that the bottleneck matters now.
