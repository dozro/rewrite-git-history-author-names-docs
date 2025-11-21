---
title: warnings
weight: 12
---

# warnings

This tool rewrites every commit in the repository.  You must force-push rewritten
branches.  This will break Fork-Relations and everyone who is currently working on a
copy of this repo has to force pull this repo.  This will break current pull requests.
This will break relationships between branches.

You probably have to redo this for every branch, you want to change your name in.  You
probably want to bring your repo into a linear history for this tool to work best, and
with the least amount of side-effects.

ONLY DO THIS ON GIT REPOSITORIES YOU OWN AND ARE NOT MISSION CRITICAL.

Signed tags may be stripped or rewritten.
