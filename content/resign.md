---
weight: 14
title: Git re-sign
---

# Git re-sign

`git re-sign` reconstructs every commit in a Git repository and re-signs them using your configured Git signing method (GPG, SSH, etc.).
It’s most useful after rewriting author/committer identities or when converting a repository to fully signed commits.

All rewritten commits are placed onto a new branch, or a optionally specified branch, leaving the original history untouched.

## Features

- Rebuilds every commit using `git commit-tree -S`
- Preserves tree contents, parents, author/committer metadata, and messages
- Re-signs each commit with your Git signing configuration
- Writes the rewritten history to a new branch (default: `resigned`)
- Leaves original branches unchanged
- Ideal for repositories that have:
  - Metadata corrections (author/committer changes)
  - Unsigned historical commits that need signing
  - Migration between signing methods (GPG → SSH, etc.)

## Usage

```bash
man git-re-sign
```

For convenience sake you can also access the man pages of this command

### General Usage

```bash
git re-sign [ -signCommits ] [ -signOnBranch <branch> ]
```

| option | description |
| ------ | ----------- |
| `-signCommits` | Enable commit signing. Enabled by default |
| `-signOnBranch <branch>` | Name of the branch that will receive the rewritten, signed history. Default: `resigned` |

## Examples

### Re-sign all commits using the configured signing key

```bash
git re-sign
```

Result:

- Original history on main stays the same
- New rewritten history stored at `resigned`

### Re-sign commits into your own custom branch name

```bash
git re-sign -signOnBranch fully-signed
```

Result:

- Original history on main stays the same
- New rewritten history stored at `fully-signed`

### Re-sign commits into your main branch

```bash
git re-sign -signOnBranch main
```

Warning: This will have serious side effects.

