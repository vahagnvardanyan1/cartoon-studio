---
name: film-status
description: Report where an in-progress cartoon production stands — which stage, what is approved, what is pending, what is blocked. Use when the user says "/film-status", "where are we", "what's the status", "what's left", "show me progress", or returns to a production after a break.
---

# Report production status

Read the production folder and give an honest account of where the film stands.

## Gather

Read `canon.md`, `assets.md`, `shots.md` and `audio.md`. Do not rely on
conversation memory — the files are the record, and a session may have been
resumed from elsewhere.

## Report

**Stage.** Which of the eight stages is current, and what gate it is waiting on.

**Assets.** How many approved, how many pending, and name anything superseded
so nothing downstream is built on a stale reference.

**Shots.** A compact table: number, title, state (not started / drafted /
approved / needs rework), duration. Total approved runtime against target.

**Blocked.** Anything waiting on the user — an unanswered cultural question, an
asset pending review, a decision not yet made. List these first; they are the
only things stopping progress.

**Known problems.** Every defect you are aware of and have not yet fixed,
including ones the user has not spotted. If a character sheet was corrected
after shots were rendered against the old one, say which shots are now stale.

**Spend.** Credits used so far and estimated to finish.

## Then

Say what the single next action is, and ask whether to take it. One action, not
a list.
