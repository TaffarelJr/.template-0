# Creating a New Template Repo <!-- omit in toc -->

Template repositories use the [`.github`][github] repository
as their template. So to create a new one, follow these steps:

### Table of Contents <!-- omit in toc -->

- [1. Create a new repository](#1-create-a-new-repository)
- [2. Clone the repo](#2-clone-the-repo)
- [3. Customize template files](#3-customize-template-files)
- [4. Customize root repo files](#4-customize-root-repo-files)
- [5. Push the changes to GitHub](#5-push-the-changes-to-github)
- [6. Run the template sync](#6-run-the-template-sync)

## 1. Create a new repository

First we need to actually create the repo.

- DO NOT actually use a template in GitHub; we'll be using merging later instead.
- The repository name should use the format: `.template-<type>`.
  - For example: `.template-NuGet`
- Leave the description blank for now.
- Don't add any files to the repo, leave it empty for now.

## 2. Clone the repo

Clone the repo locally, and open it in Visual Studio Code.
The [`.github`][github] repository needs to be added as an upstream remote
so the template sync can match up the commits in the new repo
with those in the [`.github`][github] repo. Execute the following commands:

```bash
# May need to configre SSH key
git remote add template git@github.com:TaffarelJr/.github.git
git config remote.pushdefault origin
git config commit.template .gitmessage
git fetch template
git checkout -B main template/main
```

## 3. Customize template files

The files that were synced from the [`.github`][github] template
need to be customized for this new template repo.

- Delete the following files that will
  reside only in the [`.github`][github] repo:
  - `.github/ISSUE_TEMPLATE/config.yml`
  - `.github/FUNDING.yml`
  - `docs/`
  - `CODE_OF_CONDUCT.md`
- Find all instances of `TaffarelJr/.github` in the repo
  - Replace it with `TaffarelJr/<new repo name>` in **ONLY** these files:
    - `CONTRIBUTING.md`
    - `SECURITY.md`
    - `SUPPORT.md`
    - `.github/ISSUE_TEMPLATE/01_bug_report.yml`
    - `.github/ISSUE_TEMPLATE/02_performance_issue.yml`
    - `.github/ISSUE_TEMPLATE/03_feature_request.yml`
- Commit the changes with the message: `chore: customize template files`

## 4. Customize root repo files

Now we can add deeper customization to the root repo files
to meet the needs of the new template:

- Modify `.editorconfig` as needed
- Generate a `.gitattributes` file using https://gitattributes.io/
- Generate a `.gitignore` file using https://www.toptal.com/developers/gitignore
- Replace the contents of the `README.md` file
- Add any additional ecosystems to `dependabot.yml`
- Add any additional root files necessary for the new template
- Commit the changes with the message: `chore: customize root repo files`

## 5. Push the changes to GitHub

Push the branch to GitHub:

```bash
git push
```

The settings should take effect almost immediately;
verify that the repo description and tags are showing on the home page.

## 6. Run the template sync

Next, we need to validate the template sync.
To do this, go to `Actions` -> `Template Sync` -> `Run workflow` -> `main`
and click `Run workflow`. It should complete with no changes.

<!-- GitHub Footnotes -->

[github]: https://github.com/TaffarelJr/.github
