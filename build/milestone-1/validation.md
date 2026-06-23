# Milestone 1 validation

This is where the build-and-validation record gets written, milestone by milestone. It grows into the formal test plan and results later (D5.1, D5.2), but for now it's a living checklist. This is the Milestone 1 part, so only the scenarios that are in scope right now.

Each row is a test scenario from the plan (see Milestone 1 in [`../../PLANNING.md`](../../PLANNING.md)). Record the result and link to whatever proves it: a NervesHub deployment, a console log, a captured result against the [schema](../../data/schema/).

| Scenario | What should happen | Result | Evidence |
|---|---|---|---|
| Valid signed update delivered | Boots the new firmware, reports the version back to NervesHub | not started | |
| Tampered or unsigned firmware delivered | Signature doesn't match, caught before flash, running firmware untouched | not started | |
| Broken firmware deployed | Health-check fails on the new partition, reverts inside 30s | not started | |
| Delta update on a single node | Patch rebuilds the full image, hash matches, transfer is much smaller | not started | |
| Network drops mid-download | Resumes from the checkpoint on reconnect, nothing corrupted | not started | |

Mark results as: not started, in progress, pass, or fail (link the failure if it fails).

For next week, the realistic targets are the first two rows: a signed update applies, and a tampered one gets rejected. The rest follow over the rest of Milestone 1.
