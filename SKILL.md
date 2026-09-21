---
name: work-breakdown
description: Split work one level down into packages that someone with no prior context can pick up, stating what and why but never how. Works at two sizes, one per run - big packages (epics, phases - the big picture plus enough to split them later) or small packages (tasks, tickets - everything needed to start and finish). Use when the user asks to "split this project into epics", "break this epic/phase into tasks", "create the subtasks", "write the tickets for the agents", "make the tasks self-contained", or when a plan agreed in conversation has to become something another agent will implement.
---

# Work breakdown

The reader of a package was not in the planning conversation and never will be. Everything they need to understand the work must be in the package or reachable from it. Everything about *how* to do it must be left to them.

## One level per run, and two sizes

Each run splits exactly one thing one level down. Before writing anything, settle with the user which size is being produced:

- **Big packages**: a project split into epics or phases.
- **Small packages**: one epic or phase split into tasks.

Never go a level deeper in the same run, even when a big package obviously needs splitting. The user decides when to come back to each big package and run this again on it. Do not offer to continue into the next level unprompted.

## The line between what and how

This holds at both sizes.

**Belongs in a package**
- The outcome and why it matters; why it comes in this position.
- Decisions already made by the owner, stated as decisions with their reason.
- Boundaries: what this package must not do, and what belongs to a neighbour.
- What is out of scope, with the reason.
- Working rules of the project (budgets, safety limits, process conventions).

**Never in a package**
- File paths, function, variable, script or command names.
- Schemas, field names, data layouts, library choices, algorithms.
- The approach inside a component.
- For a big package: its future tasks. How an epic gets split is part of its "how".

If the implementer complains that they do not know which file to change, the package is working. If they could not find the thing at all, improve the directions, not the answer.

## Big packages

A big package gives the big picture and enough to split it well later. It is deliberately light.

**It contains**
1. **Outcome and why** — what is true when this is done, and what it is for.
2. **Scope** — what is in, what is out and why.
3. **How success will be judged** — coarse: the few measures or conditions that matter, not a checklist.
4. **Relation to the other big packages** — what it needs from them, what it gives them, and the order.
5. **Decisions** — the ones already made, and the ones still open and whose they are.
6. **Main areas of the work** — the natural parts of the problem and what makes each one hard, risky or uncertain. This is what lets someone find the cuts later.

**It does not contain** detailed required behaviour, done-when criteria per deliverable, directions for finding things in the repository, known traps, or anything written at task resolution.

**The hidden task list is forbidden.** "Main areas of the work" describes the terrain, not the route. Each area is a noun phrase with its difficulty ("the labeled cases: hard because the right answer must be certain by construction"), never a verb phrase that could be assigned ("build the labeled cases", "then write the scorer"). No ordering between areas, no sizing, no owners, no "first… then…". If an area reads like something you could hand to a person tomorrow, it is a task: rewrite it as the part of the problem it belongs to, or remove it. When in doubt, leave it out; an epic with too little terrain gets a question later, an epic with a task list gets built as written without anyone thinking.

## Small packages

A small package carries everything needed to start and to finish.

1. **Context (read first)** — one block, identical in every package of the set: what the whole effort is in two sentences; the rules that apply everywhere; where the shared definitions live (the parent); how to find your way in the repository; how to keep the repository healthy while working. Repeating it is deliberate: each package must stand alone.
2. **Depends on** — which packages, and *what exactly* it takes from each.
3. **Outcome** — what exists when this is done, and who consumes it.
4. **Why** — including why now and why here.
5. **What to produce / behaviour required** — properties, not mechanisms; stated so they can be tested.
6. **Things to expect** — known traps and costs, told as facts with where to read more.
7. **Boundaries** — what is out of this package; what needs the coordinator's go-ahead.
8. **Done when** — verifiable, including the project's standing quality gates.

Directions for finding things are by concept: "the policy that governs the deterministic checks, reachable from that phase's summary".

## The parent carries what is shared

The parent of a set of small packages is their big package; the parent of a set of big packages is the project. Put in the parent, once: the definitions every package uses; the facts several packages rely on; how the work is split and in what order; budgets and who approves spend; what is explicitly out of scope and why. Packages point to it instead of redefining it. Each level adds only what is new at that level and points upward for the rest. A term used in two packages and defined in neither is the most common defect.

## Splitting a big package into small ones

Start from the big package's own text, plus whatever the user adds in this session. Do not reconstruct intent from an old conversation or from memory of how it was planned. If the text does not give enough to find the cuts, say so and ask; do not invent them. A big package that cannot be split from what it says is a defect in the big package: fix it there first, then split.

Splitting may show that the big package needs more in its shared sections (definitions, facts, decisions). Add them to it as part of this run.

## Rules learned the hard way

- **One owner per shared decision.** If two packages both need a decision, give it to the earliest one as a named deliverable and make the others consume it. "Agree it together" is not an owner. Check the dependency graph for cycles after doing this.
- **Decide what is yours; surface what is not.** Every choice the implementer cannot legitimately make (budgets, scope, policy, which starting point) is either decided in the text or listed as a question for the owner. Never left implicit.
- **Volatile facts are phrased as instructions to check.** Anything about work still moving elsewhere is written as "confirm the current state; this text may be stale", never as "X has / has not happened".
- **Verify before asserting.** Every statement about the repository is checked against the repository before it is written. Inherited claims ("the existing tool already does X") are the ones most often wrong.
- **Out of scope is written down with its reason**, so nobody rebuilds it by habit, and with the one thing still owed to it if any (for example "record results readably so a person can decide later").
- **Proportion.** Do not ask for guards against situations that do not exist in this project's context, and do not turn a design constraint into a later audit. If something must be true for the work to run at all, it belongs in the package that builds it.
- **Criteria must be able to fail.** "Shows improvement" with no way to come out negative is not a criterion. Say what a negative result looks like and that it is an acceptable outcome.
- **Best-effort is a valid requirement** when the owner says so: state the low bar explicitly ("catching a few is fine; not a blocker") so the implementer does not gold-plate.
- **Names describe function**, not the project phase that built them; people will operate this after the phase is forgotten.
- **No owners, people or secrets** in the text unless the project's rules say otherwise.

## Procedure

1. Settle the size for this run (big or small) and what is being split. Restate the agreed plan in a few lines and get any open decision settled first.
2. Draft the split: the packages, their order, what can run in parallel, shared decisions and their single owner.
3. Write the parent's shared sections, then each package using the anatomy for its size.
4. Self-check every package. Both sizes: any file, function or command name? any undefined term? any fact not verified? any criterion that cannot fail? Big: does any "area" read like a task; is anything at task resolution? Small: could it be started with only this text and the repository?
5. When one decision changes later, update every package and the parent in the same pass, and any neighbouring document that states the old decision; list the ones you may not touch.
6. Offer the blind spec review as the next step. Reviewing big packages before they are split is much cheaper than reviewing after: a defect in a parent is copied into every package under it.
