# Git Quick Reference

**For shortlisted candidates who need a command refresher**

This is not a tutorial. It is a reference for the specific Git operations you need to complete the screening task. If you have never used Git before, the screening task will be difficult — but the commands below cover everything required.

---

## The Commands You Need

### Fork and Clone

Forking is done on GitHub (click the Fork button). Cloning is done in your terminal:

```bash
# Clone YOUR fork — not the original repo
git clone https://github.com/YOUR_USERNAME/fellowship-screening.git
cd fellowship-screening
```

### Create a Branch

```bash
# Always create your branch from main
git checkout main
git pull origin main   # make sure you have the latest version

# Create and switch to your branch in one command
git checkout -b screening/YOUR_GITHUB_USERNAME
```

Verify you are on the right branch:

```bash
git branch
# The branch with * next to it is your current branch
# You should see: * screening/your-username
```

### Add and Commit Your File

```bash
# Add only your submission file — not everything
git add submissions/YOUR_GITHUB_USERNAME.md

# Commit with a clear message
git commit -m "add screening submission for YOUR_GITHUB_USERNAME"

# Check your commit was made
git log --oneline -3
```

### Push Your Branch

```bash
git push origin screening/YOUR_GITHUB_USERNAME
```

After this, go to GitHub. You should see a yellow banner on the original repo page saying your branch has recent pushes, with a button to open a Pull Request. Click it.

---

## Common Problems and Fixes

**Pushed to the wrong branch (e.g. pushed to main):**

```bash
# First, create the correct branch from where you are
git checkout -b screening/YOUR_GITHUB_USERNAME

# Then push the correct branch
git push origin screening/YOUR_GITHUB_USERNAME

# Do NOT push to main again
```

**Made a mistake in your submission file after committing:**

```bash
# Edit the file, then:
git add submissions/YOUR_GITHUB_USERNAME.md
git commit -m "fix: correct section content in screening submission"
git push origin screening/YOUR_GITHUB_USERNAME
# The PR updates automatically — you do not need to close and reopen it
```

**Forgot to fork and cloned the original repo directly:**

```bash
# Fork on GitHub first, then:
git remote set-url origin https://github.com/YOUR_USERNAME/fellowship-screening.git
git push origin screening/YOUR_GITHUB_USERNAME
```

**PR went to your fork instead of the original repo:**

On the PR page, look at the base repository dropdown at the top. It should say `Inference-LAB/fellowship-screening`, not `YOUR_USERNAME/fellowship-screening`. If it shows your fork, close the PR and open a new one from the correct page.

---

## What a Correct Submission Looks Like

```
Branch:    screening/ali-dev
PR title:  [Screening] Muhammad Ali — docling-pk — Research Engineer
PR desc:   Added my screening submission file to the /submissions folder.
           The file explains my prior OpenCV experience and the specific
           contribution I plan to make as Research Engineer on docling-pk.

File:      submissions/ali-dev.md
Contents:  Name, Project and Role, Expected Contribution, Question
           (all four sections present)
```

---

## If You Are Completely Stuck

Open an Issue in this repository using the Question template. Do not DM the director for technical Git help — post the question publicly so others who face the same problem can see the answer.

Include in your issue:
- The exact command you ran
- The exact error message you received
- Your operating system (Windows / Mac / Linux)

---

*INFERENCE Lab · inference-lab.org*
