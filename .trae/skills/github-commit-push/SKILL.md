---
name: github-commit-push
description: Use when the user asks to commit and push this 高级网页设计 project to GitHub, or to sync/upload to GitHub ("提交到 github", "push 到 github", "同步 GitHub", "推送到 github"). Covers the github remote (SSH), coexisting with the gitee origin remote, ignored bundled apps, prompt logging, and the exact commit/push commands.
---

# Commit and push the project to GitHub

This course archive is also pushed to **<https://github.com/zhanglongen/zle>**.
Branch: `master`. Remote name: `github` — the existing `origin` points to
gitee, so never overwrite or remove it. SSH public key is already set up,
so use the SSH URL.

## Rules

1. **Never** stage, commit, or push `CodeBuddy/` or `Steam++/`. They are
   bundled third-party Windows apps, not part of the website. They are
   excluded by `.gitignore`.
2. Log the user's prompt to `zhang prompt.md` (append only) **before** doing
   the git work, per the repo-wide workflow rule in `AGENTS.md`.
3. Commit messages should be concise and describe the page work, e.g.
   `添加 11-2 3D 动画页面` or `更新课程作业页面`.
4. Only commit/push when the user explicitly asks.
5. Pages created or modified in the session must follow the `AGENTS.md`
   conventions (`zle_` naming, header comment) before being committed.

## Preflight

```powershell
git remote -v
git status
git branch --show-current
```

If the `github` remote is missing, add it (SSH, since the public key is set):

```powershell
git remote add github git@github.com:zhanglongen/zle.git
```

## Network notes (already configured, do not redo)

- **Port 22 is blocked** on this network — SSH only works over port 443
  (`ssh.github.com:443`). `~/.ssh/config` already contains a
  `Host github.com` block that redirects to `ssh.github.com:443`, reuses
  `~/.ssh/id_ed25519_gitee` (the same public key is registered on the
  GitHub account), and disables the post-quantum KEX
  (`sntrup761x25519-sha512@openssh.com`) which the local LibreSSL build
  cannot negotiate.
- GitHub's SSH host keys (including `ssh.github.com:443`) are already in
  `~/.ssh/known_hosts`.
- So the plain `git@github.com:zhanglongen/zle.git` URL works as-is. If SSH
  auth ever fails again, fall back to HTTPS and let the user handle
  credentials:

```powershell
git remote set-url github https://github.com/zhanglongen/zle.git
```

## Commit

```powershell
git add -A
git commit -m "<concise message>"
```

## Push

```powershell
git push -u github master
```

On the first push GitHub may ask to verify the host key — answer yes.
If the push is rejected because the remote already has commits (e.g. a
README created on GitHub), fetch first and rebase or merge
(`git fetch github` then `git rebase github/master`). **Never** force-push
without asking the user.
