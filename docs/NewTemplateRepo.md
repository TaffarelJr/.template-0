# Creating a New Template Repo

Template repositories use the [`.github`][github] repository
as their template. So to create a new one, follow these steps:

### 1. Create a new repository

First we need to actually create the repo.

- Use the [`.github`][github] repository as the template
- Do NOT include all branches
- The repository name should use the format: `.template-<type>`.
  - For example: `.template-NuGet`

### 2. Configure template sync

Next, we need to make sure the template sync matches up
the commits in the new repo with those in the [`.github`][github] repo.
To do this, we need to get the sync workflow running.
Open the repo and go to `Settings` -> `Actions` -> `General`.

- Check `Allow GitHub Actions to create and approve pull requests`

Now go to `Actions` -> `Template Sync` -> `Run workflow` -> `main`
and click `Run workflow`. It should complete with no changes.

### 3. Clone the repo

Clone the repo on your local machine so you can work with the files.
Open it in Visual Studio Code.

### 4. Customize template files

The files that were synced from the [`.github`][github] template
need to be customized for this new template repo.

- Delete the following files that are not part of the template sync:
  - `.github/ISSUE_TEMPLATE/config.yml`
  - `.github/FUNDING.yml`
  - `docs/`
  - `CODE_OF_CONDUCT.md`
- Find all instances of `.github` in the repo
  - Replace `.github` with the new repo name in the URIs
    in **ONLY** the following files:
    - `CONTRIBUTING.md`
    - `SECURITY.md`
    - `SUPPORT.md`
    - `.github/ISSUE_TEMPLATE/01_bug_report.yml`
    - `.github/ISSUE_TEMPLATE/02_performance_issue.yml`
    - `.github/ISSUE_TEMPLATE/03_feature_request.yml`
- Commit the changes to `main` with the message: `chore: customize template files`

### 5. Customize initial repo files

Now all that's left is to customize the root repo files
to meet the needs of the new template:

- Modify `.editorconfig` as needed
- Generate a `.gitattributes` file using https://gitattributes.io/
- Generate a `.gitignore` file using https://www.toptal.com/developers/gitignore
- Replace the contents of the `README.md` file
- Add any additional ecosystems to `dependabot.yml`
- Commit the changes to `main` with the message:
  `chore: customize initial repo files`

### 6. Push the changes to GitHub

No need for a PR yet, just push the `main` branch up.
The settings should take effect almost immediately;
verify that the repo description and tags are showing on the home page.

<!-- GitHub Footnotes -->

[github]: https://github.com/TaffarelJr/.github
