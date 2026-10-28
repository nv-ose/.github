# NV OSE GitHub Contributing Guidelines (SOP)

**Version:** 1.1 · **Last updated:** 2026-10-28 · **Maintainers:** Max Wegener, Jordan Lancaster

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

## 3. Where does my work go?

| If it's… | Put it in… |
|---|---|
| A **project**: several scripts, a pipeline, a recurring report or dashboard, its own collaborators | **Its own new repository** (Section 4) |
| A **reusable piece**: a function, a template, a SQL query, a snippet others can copy | `shared-resources`, in the matching topic folder |
| A **training** or tutorial | The [Training submission form](https://github.com/nv-ose/team-hub/issues/new?template=training-submission.yml) in `team-hub` (or `training` directly if you know Quarto) |
| A **presentation**, poster, or briefing | `presentations` |
| A **question, idea, or announcement** | [Discussions](https://github.com/orgs/nv-ose/discussions) |

If a project contains a piece others could reuse (e.g., a REDCap upload function), keep it in the project **and** add a generalized copy to `shared-resources` with a link back to the project.

## 4. Adding a new repository

Members can create **private** repositories in nv-ose. Only owners can make a repository public.

**Before the first commit**

1. **Name it** following Section 2 (e.g., `respiratory-dashboard`, `measles-case-report`).
2. **Add a `.gitignore` first.** It must exclude data folders, credentials (`.Renviron`, `.env`), old notes, and rendered output. Commit nothing until it's in place.
3. **Check for secrets.** Search your code for passwords, tokens, and usernames. Credentials must be read from `~/.Renviron` or `.env` (for example `Sys.getenv("REDCAP_TOKEN")`), never typed into scripts. **Old notes and scratch files often contain credentials. Leave them out.**
4. **Write a `README.md`** using the template in Section 12.

**Creating it**

5. In GitHub Desktop: **File → Add local repository → create a repository**. Review the **Changes** list: only code and documentation should be there, no data.
6. Click **Publish repository**, set **Organization** to **nv-ose**, and keep **Keep this code private** checked.

**After publishing**

7. **Add a description and topics:** on the repo page, click ⚙️ next to **About**. Use topics from Section 5: at least one each for program area, data source, language, type, and status.
8. **Set access:** **Settings → Collaborators and teams**. Add the team or people who need it. Give at least one other person **Admin** or **Maintain**, so the repo isn't stranded if you leave.
9. **List it in the member directory:** add a row to the **Projects** table in [`.github-private/profile/README.md`](https://github.com/nv-ose/.github-private/blob/main/profile/README.md) with a pull request.
10. **Optional:** add a `CODEOWNERS` file (`.github/CODEOWNERS` containing, e.g., `* @your-username`) so you're automatically asked to review changes.

**Retiring a repository**

When a project ends, change its `active` topic to `archived`, then go to **Settings → Danger Zone → Archive this repository**. Archived repos become read-only but stay searchable. Update its status in the member directory.

## 5. Topics (tags)

Topics let everyone filter repositories (search `topic:redcap` on the [org repositories page](https://github.com/orgs/nv-ose/repositories)). Use these standard topics: lowercase, with hyphens. Ask an owner before inventing new ones.

| Category | Topics |
|---|---|
| Program area | `influenza`, `rsv`, `covid-19`, `respiratory-surveillance`, `syndromic-surveillance`, `vaccine-preventable`, `foodborne`, `std-hiv` |
| Data source | `essence`, `redcap`, `ilinet`, `fluview`, `nedss` |
| Language | `r`, `python`, `sql`, `quarto` |
| Type | `pipeline`, `dashboard`, `report`, `training`, `template`, `functions` |
| Status | `active`, `archived` |

Example: `respiratory-dashboard` → `influenza`, `rsv`, `respiratory-surveillance`, `essence`, `redcap`, `ilinet`, `fluview`, `r`, `python`, `pipeline`, `dashboard`, `active`.

## 6. Standard folder structures

Templates for all structures below are included in the repos. **Copy the `_template` folder, rename it, and fill it in** — don't build from scratch.

### Training materials (`training` repo)

The `training` repo is a [Quarto](https://quarto.org) website published at <https://nv-ose.github.io/training/>. Each training gets its own folder in `pages/` (copy `training/_template/`):

```
training/
├── _quarto.yml                # Site navigation and sidebars: add each new training here
├── index.qmd                  # Site home page (list of trainings)
├── pages/
│   ├── intro-to-github/
│   │   ├── index.qmd          # Overview, audience, learning objectives, prerequisites
│   │   ├── 01-lesson-name.qmd # Numbered lessons
│   │   └── exercises.qmd
│   └── intro-to-r/
│       └── ...
└── docs/                      # Generated website. Never edit by hand
```

After editing, run `quarto render` and commit the updated `docs/` folder too. See the `training` README for details.

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

## 7. Required files

Every repository **must** have:

- **`README.md`** — use the template in Section 12
- **`LICENSE`** — CC BY 4.0 for training and documentation; MIT for code (add via GitHub: *Add file → Create new file → name it `LICENSE` → Choose a license template*)
- **`.gitignore`** — appropriate for the language used

## 8. Workflow

1. **Never commit directly to `main`** in shared repos. Create a branch:
   `yourname/short-description` (e.g., `mwegener/add-git-workshop`)
2. Make your changes and commit in small, logical steps.
3. Open a **pull request** and request a review from at least one other team member.
4. After approval, merge and delete the branch.

**Who reviews:** the repo's maintainer, or an organization owner (Max Wegener or Jordan Lancaster) if you're not sure. Reviewers check that the change follows this SOP and **contains no data or credentials**, then merge it.

### How to add or change files

Pick whichever way you're comfortable with. Both end in a pull request.

#### Option A: On the GitHub website (no software needed)

Best for adding a few files or small edits.

1. Open the repo on github.com and go to the folder you want to add to.
2. **To add files:** click **Add file → Upload files**, then drag your files in.
   **To edit a file:** open it and click the **pencil ✏️** icon.
   **To create a file:** click **Add file → Create new file**. Type `folder-name/` in the name box to create a folder.
3. Click **Commit changes…**, write a short message (Section 8), and choose **Create a new branch for this commit and start a pull request**.
4. Click **Propose changes**, then **Create pull request**. Add a reviewer on the right.
5. After it's approved and merged, delete the branch (GitHub offers a button).

#### Option B: With GitHub Desktop

Best for larger changes, code you run locally, or many files.

1. **Clone** the repo once: **File → Clone repository**. Save it in `Documents/GitHub/NV-OSE/`.
2. **Fetch origin / Pull origin** to get the latest version.
3. **Current branch → New branch**, named `yourname/short-description`.
4. Add or edit files in the repo folder on your computer, following the repo's folder structure (Section 6).
5. In the **Changes** tab, **review every file**. No data, no credentials. Write a summary, then **Commit to `your-branch`**.
6. Click **Publish branch**, then **Create Pull Request**. Add a reviewer on github.com and click **Create pull request**.
7. After it's merged: switch back to `main` and click **Pull origin**.

New to this? The [Introduction to Git and GitHub](https://nv-ose.github.io/training/pages/intro-to-github/) training walks through both, step by step.

### Where to add things in each repository

| Repository | What to add | Steps |
|---|---|---|
| `training` | A new training or lesson | **Most people:** [submit it through the Training submission form](https://github.com/nv-ose/team-hub/issues/new?template=training-submission.yml) in `team-hub`. Max or Jordan converts it into web pages. **If you know Quarto:** build it yourself. See the [training README](https://github.com/nv-ose/training#adding-a-training) |
| `shared-resources` | A reusable function, template, or snippet | Add it to the matching topic folder with a short README. See the [shared-resources README](https://github.com/nv-ose/shared-resources#adding-a-resource) |
| `presentations` | Slides, a poster, or a briefing | Copy `_template/` to a `YYYY-MM-DD_event-name` folder, add PDFs. See the [presentations README](https://github.com/nv-ose/presentations#adding-a-presentation) |
| `team-hub` | Questions, ideas, announcements | Don't add files. Start a [Discussion](https://github.com/orgs/nv-ose/discussions) |
| `.github-private` | Your project in the member directory | Add a row to the Projects table. See the [.github-private README](https://github.com/nv-ose/.github-private#adding-your-project-to-the-member-directory) |
| `.github` | Changes to this SOP or the public profile | Edit with a PR. Owners approve SOP changes |
| A project repo | Changes to that project | Branch and PR. Follow the project's own README |
| **A new project** | A whole new repository | Section 4 |

**Commit messages:** start with a verb in the present tense and describe what changed.
- ✅ `Add exercises for intro-to-git workshop`
- ✅ `Fix broken link in R tutorial README`
- ❌ `stuff`, `update`, `final version 2`

## 9. Issues

Use **Issues** to report problems, suggest improvements, or plan new content. Apply a label (`bug`, `enhancement`, `new-training`, `question`) and assign someone where possible.

## 10. What NOT to upload

- ❌ Passwords, API keys, tokens, or credentials
- ❌ Protected health information (PHI), personally identifiable information (PII), or any data subject to IRB, HIPAA, or FERPA restrictions
- ❌ Copyrighted materials you don't have rights to share
- ❌ Large files (>50 MB) — link to them from Box, OneDrive, or a data repository instead
- ❌ Temporary or system files (`.DS_Store`, `.Rhistory`, `__pycache__/`)

If something sensitive is committed by mistake, **tell an owner immediately**. Deleting the file is not enough, because it remains in the history.

## 11. Visibility

- **Public:** training materials and resources meant to be shared
- **Private:** internal projects, drafts, or unpublished work
- When in doubt, start private. Ask an owner before making a repository public.

## 12. README template

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

## 13. Questions

Contact Max Wegener at [mwegener@health.nv.gov](mailto:mwegener@health.nv.gov), or open an issue in the `.github` repository.
