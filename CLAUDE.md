## Writing and changing code

When refactoring, every element you carry forward must be explicitly justified by the new design. Do not inherit anything by default. If something existed before but has no clear role in the new architecture, flag it and ask before proceeding. Do not carry it forward or drop it unilaterally.

When making a change, only modify what the change directly requires. Do not remove, add, or clean up anything else. If you notice something that looks wrong, unused, or improvable: verify it first (read the code, grep for usages, reason through it), then flag it to the user as a separate item. Never fold it into the current change.

Avoid Python shorthands that compress logic at the cost of readability. Specifically: do not use list comprehensions, dict comprehensions, generator expressions, or conditional expressions (ternary `x if cond else y`) when an explicit loop or if/else block would be clearer. Write the expanded form instead.

## Fail loud — never degrade silently

This is the most important rule here. Do not have a bias toward "keep things moving" — when something fails, do not continue as if it did not.

- Testing/verification: diagnose the error and fix the root cause. Never reason past it ("probably not important") and move on.
- Writing code: every line of code and every spec requirement exists for a reason. If a part fails, fail the whole operation loudly and surface it to the user with recovery options — do not continue with "degraded output." Retry or auto-recover only with a specific, stated justification.

Flag blockers immediately: if a required check fails or cannot run, stop and say what failed and what the user must do — as the first thing in the response, not deferred. When retrying a failed command with a fix, say so in text before retrying.

## Finish what you start

"Build X" means build all of X. The only valid stopping points: the user says stop, context limits force a break, or a blocker needs user input. Never hand off a scaffold or partial layer as if finished; after completing a task, verify you did not stop partway.

Plan rigorously before writing code — code generation is the last step, not the default next step. Probe specs for gaps, ambiguities, and unhandled edge cases rather than accepting them as written. For dependent work, go sequentially (write, verify, commit, next) rather than parallelizing pieces that must agree on shared interfaces.

## Keep the record straight

Persist decisions, conclusions, open questions, and design critiques to the appropriate durable file — do not leave them only in conversation. When an implementation resolves a spec ambiguity, update that document to match.

## Thoroughness and scope

Do not cut corners on refactors or scope-splits — verify dependencies remain intact and flag anything risky first. For "find everything" audits, reason about logically-connected code, not just keyword matches; grep misses what does not contain the search term.

Features are cheap to write in the AI era. Defer a feature only when it has no clear reason to exist — never on implementation-complexity grounds alone; a feature with a genuine reason to exist stays in. The concern is over-engineering (needless abstraction, premature generalization), not completeness.

## Dependencies and verifiable claims

Never guess package versions from training data. Look them up: pick the most recent stable release published at least 2 weeks ago, pin the exact version, and check for known vulnerabilities before committing. Applies to npm, PyPI, and Docker images.

Do not assert claims you cannot verify — "actively maintained", "industry standard", "best", "top of the leaderboard". Flag uncertainty, especially in fast-moving domains where training data goes stale.
