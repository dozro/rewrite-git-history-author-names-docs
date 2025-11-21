---
title: Background
weight: 15
---

# Background

Rewriting Git history allows you to modify commits that already exist in a repository. You might do this to correct author or committer information, adjust Signed-off-by lines, remove sensitive data, or re-sign all commits. Because commits are immutable, any rewrite creates entirely new commit hashes. This means that rewriting is a destructive process and often requires a force push.
This guide explains how rewriting works and how to perform it safely.

## Inside Git

Git stores its data using four main object types: blobs, trees, commits, and tags. Blobs represent file contents, while trees store directory structures. Commits reference a tree, parent commits, metadata, and a message. Tags provide optional annotated labels.
Since commit objects include hashes of their contents and parents, any change produces a new commit with a new hash.

## Why tho?

There are many reasons to rewrite Git history. Common motivations include fixing incorrect names or email addresses, correcting DCO lines, re-signing commits (e.g., switching from GPG to SSH), and removing sensitive text. Rewrites are also useful when importing unrelated history or standardizing metadata in shared or corporate repositories.