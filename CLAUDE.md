# For anyone (human or agent) working in this repo

## This repo is a GitHub fork — `gh` targets the wrong repo by default

This repository (`Catchswim/flutter_workout_bridge-watchos11`) is a fork of
`xhayankhan/flutter_workout_bridge`. Because of the fork link, the GitHub CLI
(`gh`) resolves the **upstream author's repo** as its default target — so
`gh pr create` run here opens the PR on a stranger's repository.

This has happened twice; on 2026-09-01 an internal PR (Crashlytics IDs, user
counts) briefly went up on the upstream repo. Closed PRs stay publicly visible
there forever.

Rules:

- In a fresh clone, run
  `gh repo set-default Catchswim/flutter_workout_bridge-watchos11`
  before any other `gh` command. The setting is local and does not travel
  with clones.
- Pass `--repo Catchswim/flutter_workout_bridge-watchos11` explicitly on any
  `gh` command that creates, merges, comments, or closes anything.
- Check the URL `gh` prints back. If it does not contain `Catchswim/`, stop
  and undo before doing anything else.

## What this plugin is to CatchSwim

The iOS HealthKit/WorkoutKit bridge used by the CatchSwim app
(`Catchswim/catch_swim`). The app pins an exact commit of this repo via
`ref:` in its `pubspec.yaml` — pushing to `main` here ships nothing until the
app repo updates that pin and its `pubspec.lock`.

Concurrency rule for `ios/Classes/FlutterWorkoutBridgePlugin.swift`: HealthKit
callbacks arrive on arbitrary queues, and every write to a collection shared
across callbacks must go through a serial `DispatchQueue` (see the
`workoutQueue` / `workoutDataMerge` / `workoutMetricsMerge` /
`routePointsMerge` queues). Every value returned over the platform channel
must be codec-safe — route new payload fields through `channelSafeValue`.
Both rules exist because breaking them killed the app in production
(v1.0.4 changelog, CatchSwim PRD-041).
