# Weekday Schedule 15:38 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Run the daily GitHub Actions analysis once each weekday at 15:38 Beijing time.

**Architecture:** Keep the existing single GitHub Actions `schedule` trigger and replace only its UTC cron value. Update the workflow comments and the existing bilingual documentation and changelog references so the workflow remains the single source of runtime truth and the docs remain consistent.

**Tech Stack:** GitHub Actions YAML, Markdown, POSIX cron

---

### Task 1: Replace The Weekday Schedule

**Files:**
- Modify: `.github/workflows/00-daily-analysis.yml:4-6`
- Modify: `docs/full-guide.md:699-706`
- Modify: `docs/full-guide_EN.md:632-639`
- Modify: `docs/CHANGELOG.md:15`

- [x] **Step 1: Update the workflow trigger and comments**

Set the workflow block to:

```yaml
# 定时触发 - 每个工作日北京时间 15:38 (UTC 07:38)
schedule:
  - cron: '38 7 * * 1-5'     # 周一到周五，UTC 07:38 = 北京时间 15:38
```

- [x] **Step 2: Update the bilingual examples and schedule tables**

Replace the 09:08 example and table row in both full guides with 15:38 and `38 7 * * 1-5`.

- [x] **Step 3: Update the existing changelog line**

Use this exact entry rather than adding another schedule entry:

```markdown
- [chore] GitHub Actions 工作日定时分析调整为北京时间 15:38（UTC 07:38），并同步中英文定时配置示例。
```

### Task 2: Verify And Publish

**Files:**
- Verify: `.github/workflows/00-daily-analysis.yml`
- Verify: `docs/full-guide.md`
- Verify: `docs/full-guide_EN.md`
- Verify: `docs/CHANGELOG.md`

- [x] **Step 1: Verify exact schedule references**

Run:

```bash
rg -n "15:38|38 7 \* \* 1-5" .github/workflows/00-daily-analysis.yml docs/full-guide.md docs/full-guide_EN.md docs/CHANGELOG.md
```

Expected: the workflow has two matching comment/cron lines, each guide has an example and table row, and the changelog has one matching entry.

- [x] **Step 2: Verify stale schedule references are gone**

Run:

```bash
rg -n "09:08|UTC 01:08|8 1 \* \* 1-5" .github/workflows/00-daily-analysis.yml docs/full-guide.md docs/full-guide_EN.md docs/CHANGELOG.md
```

Expected: no output.

- [x] **Step 3: Validate and inspect the patch**

Run:

```bash
git diff --check
git diff --stat
git diff
```

Expected: no whitespace errors and only the approved workflow, documentation, design, and plan files are included.

- [x] **Step 4: Commit and push**

```bash
git add .github/workflows/00-daily-analysis.yml docs/CHANGELOG.md docs/full-guide.md docs/full-guide_EN.md docs/superpowers
git commit -m "chore: schedule weekday analysis at 15:38"
git push origin main
```

- [ ] **Step 5: Verify GitHub and remove the temporary clone**

Confirm the remote workflow contains `38 7 * * 1-5` and reports `active`, then remove `/tmp/RRedamancy-daily-stock-analysis-1538` and confirm the path no longer exists.
