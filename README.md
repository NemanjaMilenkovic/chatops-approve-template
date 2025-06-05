// Note: This is applicable for specific projects only and not reccommended unless you know you need it

# ChatOps `/approve` Example

This demonstrates a GitHub‑native ChatOps flow:

1. A reviewer types **`/approve`** in a pull‑request comment.
2. A GitHub Actions workflow detects the command.
3. The workflow uses the GitHub CLI to **approve** (and optionally merge) the PR.
4. The bot posts the result back in the same thread.

## Setup

1. Enable **GitHub Actions** in your repository.
2. Copy `.github/workflows/command-approve.yml` into your repo.
3. Verify the repository (or org) settings allow the default `GITHUB_TOKEN` to **push and merge**.  
   *Settings → Actions → General → Workflow permissions*.
4. Protect main/master if desired and grant `contents: write` cautiously.

## Notes

* The workflow ignores bot comments to avoid loops.
* The default `GITHUB_TOKEN` is short‑lived and scoped to this repo.
* To further lock down who can run `/approve`, inspect  
  `${{ github.event.comment.author_association }}` (`MEMBER`, `OWNER`, etc.) in the `if` condition.
