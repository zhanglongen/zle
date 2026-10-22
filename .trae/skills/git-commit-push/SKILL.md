---
name: git-commit-push
description: Use when the user asks to commit and push this 高级网页设计 project with git, or to submit/publish/upload ("提交项目", "git commit", "git push", "推送到 gitee"). Covers the gitee remote, ignored bundled apps, prompt logging, and the exact commit/push commands.
---

# Commit and push the project to Gitee

This course archive is pushed to **<https://gitee.com/zhang-longen/advanced-web-design>**.
Branch: `master`. Remote name: `origin`.

## Rules

1. **Never** stage, commit, or push `CodeBuddy/` or `Steam++/`. They are
   bundled third-party Windows apps, not part of the website. They are
   excluded by `.gitignore`.
2. Log the user's prompt to `zhang prompt.md` (append only) **before** doing
   the git work, per the repo-wide workflow rule in `AGENTS.md`.
3. Commit messages should be concise and describe the page work, e.g.
   `添加 11-2 3D 动画页面` or `更新课程作业页面`.
4. Only commit/push when the user explicitly asks.

## Preflight

```powershell
git remote -v
git status
git branch --show-current
```

If `origin` is missing, add it:

```powershell
git remote add origin https://gitee.com/zhang-longen/advanced-web-design.git
```

## Commit

```powershell
git add -A
git commit -m "<concise message>"
```

## Push

```powershell
git push -u origin master
```

On the first push the gitee repo may require credentials. If the remote
default branch differs, or the user wants a different branch, confirm with
them before pushing.
