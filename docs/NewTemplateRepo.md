# Creating a New Template Repo <!-- omit in toc -->

Template repositories use the [`.github`][github] repository
as their template. So to create a new one, follow these steps:

### Table of Contents <!-- omit in toc -->

- [1. Create a new repository](#1-create-a-new-repository)
- [2. Configure manual repository settings](#2-configure-manual-repository-settings)
- [3. Clone the repo](#3-clone-the-repo)
- [4. Customize template files](#4-customize-template-files)
- [5. Customize root repo files](#5-customize-root-repo-files)
- [6. Override repository settings](#6-override-repository-settings)
- [7. Push the changes to GitHub](#7-push-the-changes-to-github)
- [8. Run the template sync](#8-run-the-template-sync)

## 1. Create a new repository

First we need to actually create the repo.

- DO NOT actually use a template in GitHub; we'll be using merging later instead.
- The repository name should use the format: `.template-<type>`.
  - For example: `.template-NuGet`
- Leave the description blank for now.
- Don't add any files to the repo, leave it empty for now.

## 2. Configure manual repository settings

Not all repo settings can be managed from the `settings.yml` file.
Some settings will still need to be configured manually for now:

- `Settings`
  - `General`
    - Check `Limit how many branches and tags can be updated in a single push`
      - Up to `2` branches and tags can be updated in a push
  - `Moderation options`
    - `Code review limits`
      - Check `Limit to users explicitly granted read or higher access`
  - `Actions`
    - `General`
      - Check `Allow GitHub Actions to create and approve pull requests`
      - Click `Save`
  - `Code security`
    - Enable `Private vulnerability reporting`
    - Enable `Dependency graph` _(if necessary)_
    - Enable `Grouped security updates`
    - Set up `CodeQL analysis` to use `Default` settings

## 3. Clone the repo

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

## 4. Customize template files

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

## 5. Customize root repo files

Now we can add deeper customization to the root repo files
to meet the needs of the new template:

- Modify `.editorconfig` as needed
- Generate a `.gitattributes` file using https://gitattributes.io/
- Generate a `.gitignore` file using https://www.toptal.com/developers/gitignore
- Replace the contents of the `README.md` file
- Add any additional ecosystems to `dependabot.yml`
- Add any additional root files necessary for the new template
- Commit the changes with the message: `chore: customize root repo files`

## 6. Override repository settings

Most of the settings in the `.github/settings.yml` file
are fine to just live in the [`.github`][github] repo.
In this new template repo, we only need to override a few of the settings.
Replace the contents of the file with the following,
filling in the values as indicated:

```yaml
_extends: .github

repository:
  #─────────────────────────────────────────────────────────────────────────────
  # "About" section (on Home Page)
  #─────────────────────────────────────────────────────────────────────────────

  # A short description of the repository
  # MUST BE A SINGLE LINE
  description: <1-line description>.

  # A URL with more information about the repository
  homepage: <URI, if applicable; otherwise, delete this property>

  # A comma-separated list of topics to set on the repository
  topics: <topic 1>, <topic 2>, ... # see https://github.com/topics

  #─────────────────────────────────────────────────────────────────────────────
  # Settings -> General
  # https://github.com/repository-settings/app/blob/master/docs/plugins/repository.md
  # https://docs.github.com/en/rest/repos/repos#update-a-repository
  #─────────────────────────────────────────────────────────────────────────────

  # The name of the repository
  name: <name>
```

Commit the changes with the message: `chore: customize repo settings`

## 7. Push the changes to GitHub

Push the branch to GitHub:

```bash
git push
```

The settings should take effect almost immediately;
verify that the repo description and tags are showing on the home page.

## 8. Run the template sync

Next, we need to validate the template sync.
To do this, go to `Actions` -> `Template Sync` -> `Run workflow` -> `main`
and click `Run workflow`. It should complete with no changes.

<!-- GitHub Footnotes -->

[github]: https://github.com/TaffarelJr/.github
