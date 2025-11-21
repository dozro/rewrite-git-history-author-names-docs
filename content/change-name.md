---
weight: 13
title: Rewrite Git History
---

# Git change-name

`git change-name` rewrites commit metadata across an entire Git repository.
It replaces outdated or incorrect author names, email addresses, and Signed-off-by lines while preserving commit timestamps and commit messages.
Because the tool rewrites every commit object, it produces an entirely new commit history.

## Description

`git change-name` works by streaming your entire history through git fast-export, modifying the author/committer metadata and Signed-off-by lines, and then reconstructing the history with git fast-import. This method ensures that all changes are applied consistently and that the commit structure is retained.
Optionally, the tool can also re-sign each commit after rewriting, creating a new branch containing both rewritten and re-signed commits.
Since commit hashes are immutable, this process changes every commit in the repository and requires a force push.

## Synopsis

```bash
git change-name
    [-oldName <name>]
    [-oldEmail <email>]
    [-newName <name>]
    [-newEmail <email>]
    [-signCommits]
    [-signOnBranch <branch>]
```

| option | description |
| ------ | ----------- |
| `-oldName <name>` | Specifies an author or committer name in existing commits that should be replaced |
| `-oldEmail <email>`| Specifies an email address to match and replace in author or committer fields |
| `-newName <name>` | Provides the new name that should replace any matched old names |
| `-newEmail <email>` | Provides the new email address to apply to rewritten metadata | 
| `-signCommits` | If enabled, the tool uses Git’s signing configuration to re-sign all rewritten commits. Disabled by default |
| `-signOnBranch <branch>` | Defines the branch where re-signed commits should be written The default branch name is `resigned` |

## Warning

Rewriting commit history is a destructive operation. Since every commit hash changes:

- You must force push rewritten branches.
- Forks and clones will no longer be compatible without a forced pull or re-clone.
- Open pull requests referencing the old history will break.
- Relationships between branches may be disrupted.
- In most cases, you must repeat the process for every branch where the metadata should be corrected.
- For best results, use a linearized repository (e.g., after rebasing) to reduce complexity and side effects.

Only use this tool on repositories you fully control and that are not mission-critical.
Signed tags may also be removed or altered during rewriting.

## Examples

### Rewrite author metadata

```bash
git change-name \
    -oldName "Old Dev" \
    -oldEmail old@example.com \
    -newName "New Dev" \
    -newEmail new@example.com
```

This updates all commits that were created using the old name or email, preserving the existing timestamps and messages.

### Rewrite and re-sign commits

```bash
git change-name \
    -oldName Old \
    -oldEmail old@example.com \
    -newName New \
    -newEmail new@example.com \
    -signCommits \
    -signOnBranch re-signed-history
```

This performs the metadata rewrite and then rebuilds the entire history with fresh commit signatures on a dedicated branch.