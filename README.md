# INFERENCE Lab Engineering Fellowship — Screening Repository

**Cohort 01 · Pre-Screening Task**

---

This repository is used exclusively for the pre-screening stage of the INFERENCE Lab Engineering Fellowship, Cohort 01. If you have received a shortlisting email, this is where you submit your screening task.

If you have not received a shortlisting email, this repository is not relevant to your application at this stage.

---

## Before You Begin

Read these instructions completely before doing anything. Candidates who start without reading fully are the ones who submit with the wrong branch name or wrong PR title — and have to resubmit.

You will need:
- Git installed on your machine (`git --version` should return a version number)
- A GitHub account
- Basic familiarity with forking, cloning, branching, and opening a Pull Request

If any of those are unfamiliar, the [Student Handbook](docs/student_handbook_excerpt.md) in this repo has a Git quick-reference section.

---

## Task Instructions

Follow these steps **in order**. Do not skip steps.

### Step 1 — Fork this repository

Click **Fork** at the top right of this page on GitHub. Fork it to your personal GitHub account — not an organisation.

### Step 2 — Clone your fork

```bash
git clone https://github.com/YOUR_USERNAME/fellowship-screening.git
cd fellowship-screening
```

Replace `YOUR_USERNAME` with your actual GitHub username.

### Step 3 — Create your branch

```bash
git checkout -b screening/YOUR_GITHUB_USERNAME
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username. The branch name must follow this exact format. A branch named `my-branch`, `feature/task`, or anything other than `screening/yourusername` will be considered incorrectly submitted.

### Step 4 — Create your submission file

Inside the `/submissions` folder, create a new file named:

```
YOUR_GITHUB_USERNAME.md
```

For example, if your GitHub username is `ali_dev`, create `submissions/ali_dev.md`.

Do not create any other files or folders. Do not modify any existing files.

### Step 5 — Write your submission

Your `.md` file must contain the following four sections, in this order:

```markdown
## Name
[Your full name]

## Project and Role
[The project you applied for and the specific role: Lead Engineer / Research Engineer / Integration Engineer]

## Expected Contribution
[One paragraph — what specifically do you expect to contribute in your assigned role?
Reference the actual project. Generic answers ("I will work hard and learn") will not pass this stage.]

## Question
[One question you have about the project after reading the project brief.
This question must show you actually read the brief — not a general question about the fellowship.]
```

### Step 6 — Commit your work

```bash
git add submissions/YOUR_GITHUB_USERNAME.md
git commit -m "add screening submission for YOUR_GITHUB_USERNAME"
```

The commit message must be clear and descriptive. A commit message of `update`, `done`, or `task` is a signal we note.

### Step 7 — Push your branch

```bash
git push origin screening/YOUR_GITHUB_USERNAME
```

### Step 8 — Open a Pull Request

Go to the **original** `Inference-LAB/fellowship-screening` repository — not your fork. You should see a prompt to open a Pull Request from your recently pushed branch. Click it.

**PR Title — must follow this exact format:**

```
[Screening] Your Full Name — Project Name — Role
```

Examples:
```
[Screening] Muhammad Ali — docling-pk — Research Engineer
[Screening] Sara Ahmed — llm-eval-kit — Lead Engineer
```

**PR Description — must contain:**

- What you added (one sentence)
- Why the content of your `.md` file reflects your genuine interest in the role (one to two sentences)

Do not copy-paste from the instructions. Write it yourself.

### Step 9 — Confirm

After submitting, confirm the following yourself before the deadline:

- [ ] Branch name is exactly `screening/your-github-username`
- [ ] PR title follows the exact format above
- [ ] PR description is written in your own words
- [ ] Your `.md` file is inside the `/submissions` folder
- [ ] Your `.md` file contains all four required sections
- [ ] You submitted before the deadline

---

## Deadline

**48 hours from the time you received the shortlisting email.**

The deadline is firm. If you have a genuine blocker — technical or otherwise — message the lab director before the deadline, not after.

---

## What We Are Evaluating

This task is simple by design. We are not testing your ability to write complex code. We are checking:

1. Can you follow precise instructions under a short deadline?
2. Do you communicate clearly in writing?
3. Did you actually read the project brief you applied for?
4. Do you self-check your work before submitting?

A candidate who submits with an incorrect branch name, notices it themselves, fixes it, and opens a corrected PR without being asked has demonstrated more than someone who got it right the first time. Self-correction matters.

A candidate who submits with an incorrect branch name and does nothing further has told us something important about how they will behave in a 6-week sprint when their PR is sent back for changes.

---

## Questions

If something in these instructions is genuinely unclear, open an Issue in this repository with the title:

```
[Question] Your Name — your question here
```

Do not DM the lab director for task clarifications — ask here so the answer is visible to all shortlisted candidates.

---

## Repository Structure

```
fellowship-screening/
├── README.md                          ← you are here
├── submissions/                       ← put your file here
│   └── .gitkeep
├── docs/
│   ├── project_briefs.md              ← summary of both projects
│   └── git_quickref.md               ← Git commands reference
└── .github/
    ├── PULL_REQUEST_TEMPLATE.md       ← auto-fills your PR description
    └── ISSUE_TEMPLATE/
        └── question.md               ← template for asking questions
```

---

*INFERENCE Lab · inference-lab.org · github.com/Inference-LAB*
*Evidence over hype. Engineering over branding.*
