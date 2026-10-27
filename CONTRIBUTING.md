# NV OSE GitHub Contributing Guidelines (SOP)

**Version:** 1.0 · **Last updated:** [date] · **Maintainers:** [Owner 1], [Owner 2]

These guidelines apply to every repository in the nv-ose organization. Following them keeps our work consistent, findable, and easy to hand off.

---

## 1. Before you start

- Create a free GitHub account and enable **two-factor authentication**.
- Ask an organization owner to add you to the appropriate team.
- New to Git? Start with the materials in the [`training`](https://github.com/nv-ose/training) repo.

## 2. Naming conventions

**Repositories, folders, and files**

- Use lowercase letters, numbers, and hyphens only: `intro-to-r`, `data-cleaning-template`
- No spaces, special characters, or capital letters
- Be descriptive but short
- Start file names with dates (`YYYY-MM-DD`) when order or version matters: `2026-11-05_workshop-slides.pdf`
- Number files that run in sequence: `01_import.R`, `02_clean.R`, `03_analyze.R`

## 3. Standard folder structures

Templates for all structures below are included in the repos. **Copy the `_template` folder, rename it, and fill it in** — don't build from scratch.

### Training materials (`training` repo)

Each workshop or tutorial gets its own folder (copy `training/_template/`):

```
training/
├── README.md                  # Index of all trainings
├── intro-to-git/
│   ├── README.md              # Overview, audience, learning objectives, prerequisites
│   ├── slides/
│   ├── exercises/
│   ├── data/                  # Small example datasets only
│   └── solutions/
└── r-for-beginners/
    └── ...
```

### Code and project resources (`shared-resources` and project repos)

Copy `shared-resources/_template-project/`:

```
project-name/
├── README.md                  # What it is, how to use it, who maintains it
├── data/
│   ├── raw/                   # Original data — never edit
│   └── processed/             # Cleaned / derived data
├── code/                      # Scripts and notebooks
├── docs/                      # Documentation, protocols, notes
└── outputs/                   # Figures, tables, reports
```

### Presentations (`presentations` repo)

Training workshops go in `training`; one-time talks, posters, briefings, and webinars go here. Copy `presentations/_template/` and name the folder `YYYY-MM-DD_event-name`:

```
presentations/
├── README.md                              # Index table: date, title, event, presenter
└── 2026-11-05_cste-annual-conference/
    ├── README.md                          # Presenter, event, abstract, clearance, citation
    ├── slides.pdf
    └── poster.pdf
```

- Upload **PDFs**; `.pptx` is optional. Keep files under 50 MB.
- This repo is **private**. Presentations with preliminary or unreleased data must be cleared before an owner makes them public.

Delete folders you don't need; don't invent new top-level folders without a good reason. (Empty folders contain a `.gitkeep` file so Git tracks them — delete it once the folder has content.)

## 4. Required files

Every repository **must** have:

- **`README.md`** — use the template in Section 9
- **`LICENSE`** — CC BY 4.0 for training and documentation; MIT for code (add via GitHub: *Add file → Create new file → name it `LICENSE` → Choose a license template*)
- **`.gitignore`** — appropriate for the language used

## 5. Workflow

1. **Never commit directly to `main`** in shared repos. Create a branch:
   `yourname/short-description` (e.g., `mwegener/add-git-workshop`)
2. Make your changes and commit in small, logical steps.
3. Open a **pull request** and request a review from at least one other team member.
4. After approval, merge and delete the branch.

**Commit messages:** start with a verb in the present tense and describe what changed.
- ✅ `Add exercises for intro-to-git workshop`
- ✅ `Fix broken link in R tutorial README`
- ❌ `stuff`, `update`, `final version 2`

## 6. Issues

Use **Issues** to report problems, suggest improvements, or plan new content. Apply a label (`bug`, `enhancement`, `new-training`, `question`) and assign someone where possible.

## 7. What NOT to upload

- ❌ Passwords, API keys, tokens, or credentials
- ❌ Protected health information (PHI), personally identifiable information (PII), or any data subject to IRB, HIPAA, or FERPA restrictions
- ❌ Copyrighted materials you don't have rights to share
- ❌ Large files (>50 MB) — link to them from Box, OneDrive, or a data repository instead
- ❌ Temporary or system files (`.DS_Store`, `.Rhistory`, `__pycache__/`)

If something sensitive is committed by mistake, **tell an owner immediately**. Deleting the file is not enough, because it remains in the history.

## 8. Visibility

- **Public:** training materials and resources meant to be shared
- **Private:** internal projects, drafts, or unpublished work
- When in doubt, start private. Ask an owner before making a repository public.

## 9. README template

```markdown
# Title

One-sentence description of what this is.

## Overview
What it does, who it's for, and why it exists.

## Contents
Brief description of the folder structure.

## How to use
Steps, prerequisites, or software required.

## Maintainer
Name — email

## License
CC BY 4.0 / MIT

## Last updated
YYYY-MM-DD
```

## 10. Questions

Contact [name] at [email], or open an issue in the `.github` repository.
