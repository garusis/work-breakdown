---
name: self-contained-work-packages
description: Split planned work into work packages (tickets, subtasks) that an agent or engineer with no prior context can pick up and finish, stating what and why but never how. Use when the user asks to "create the subtasks", "break this phase into tasks", "write the tickets for the agents", "make the tasks self-contained", or when a plan agreed in conversation has to become something another agent will implement.
---

# Self-contained work packages

The reader of a work package was not in the planning conversation and never will be. Everything they need to understand the work must be in the package or reachable from it. Everything about *how* to build it must be left to them.

## The line between what and how

**Belongs in a package**
- The outcome and why it matters; why it comes in this position.
- What must be produced, described by its purpose and properties.
- Behaviour that is required, stated so it can be tested.
- Decisions already made by the owner, stated as decisions with their reason.
- Boundaries: what this package must not do, and what belongs to a neighbour.
- What is true today that the work relies on.
- Working rules of the project (budgets, safety limits, process conventions).
- How to find things, by concept: "the policy that governs the deterministic checks, reachable from that phase's summary".
- Done-when criteria that can come out false.

**Never in a package**
- File paths, function, variable, script or command names.
- Schemas, field names, data layouts, library choices, algorithms.
- The approach inside a component.

If the implementer complains that they do not know which file to change, the package is working. If they could not find the thing at all, improve the directions, not the answer.

## Anatomy of one package

1. **Context (read first)** — one block, identical in every package of the set: what the whole effort is in two sentences; the rules that apply everywhere; where the shared definitions live (the parent); how to find your way in the repository; how to keep the repository healthy while working. Repeating it is deliberate: each package must stand alone.
2. **Depends on** — which packages, and *what exactly* it takes from each.
3. **Outcome** — what exists when this is done, and who consumes it.
4. **Why** — including why now and why here.
5. **What to produce / behaviour required** — properties, not mechanisms.
6. **Things to expect** — known traps and costs, told as facts with where to read more.
7. **Boundaries** — what is out of this package; what needs the coordinator's go-ahead.
8. **Done when** — verifiable, including the project's standing quality gates.

## The parent carries what is shared

Put in the parent, once: the definitions every package uses; the facts about the repository that several packages rely on; how the work is split and in what order; budgets and who approves spend; what is explicitly out of scope and why. Packages point to it instead of redefining it. A term used in two packages and defined in neither is the most common defect.

## Rules learned the hard way

- **One owner per shared decision.** If two packages both need a decision, give it to the earliest one as a named deliverable and make the others consume it. "Agree it together" is not an owner. Check the dependency graph for cycles after doing this.
- **Decide what is yours; surface what is not.** Every choice the implementer cannot legitimately make (budgets, scope, policy, which starting point) is either decided in the text or listed as a question for the owner. Never left implicit.
- **Volatile facts are phrased as instructions to check.** Anything about work still moving elsewhere is written as "confirm the current state; this text may be stale", never as "X has / has not happened".
- **Verify before asserting.** Every statement about the repository is checked against the repository before it is written. Inherited claims ("the existing harness already does X") are the ones most often wrong.
- **Out of scope is written down with its reason**, so nobody rebuilds it by habit, and with the one thing still owed to it if any (for example "record results readably so a person can decide later").
- **Proportion.** Do not ask for guards against situations that do not exist in this project's context, and do not turn a design constraint into a later audit. If something must be true for the work to run at all, it belongs in the package that builds it.
- **Criteria must be able to fail.** "Shows improvement" with no way to come out negative is not a criterion. Say what a negative result looks like and that it is an acceptable outcome.
- **Best-effort is a valid requirement** when the owner says so: state the low bar explicitly ("catching a few is fine; not a blocker") so the implementer does not gold-plate.
- **Names describe function**, not the project phase that built them; people will operate this after the phase is forgotten.
- **No owners, people or secrets** in the text unless the project's rules say otherwise.

## Procedure

1. Restate the agreed plan to the user in a few lines and get any open decision settled first.
2. Draft the split: packages, order, what can run in parallel, shared decisions and their single owner.
3. Write the parent's shared sections, then each package using the anatomy above.
4. Self-check every package: could it be started with only this text and the repository? Any name of a file, function or command? Any undefined term? Any criterion that cannot fail? Any fact not verified?
5. When one decision changes later, update every package and the parent in the same pass, and any neighbouring document that states the old decision; list the ones you may not touch.
6. Offer the blind spec review as the next step; that is how the set is proven.
