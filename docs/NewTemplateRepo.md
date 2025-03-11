# Creating a New Template Repo

Template repositories use the [`.github`][github] repository
as their template. So to create a new one, follow these steps:

### 1. Create a new repository

First we need to actually create the repo.

- Use the [`.github`][github] repository as the template
- Do NOT include all branches
- The repository name should use the format: `.template-<type>`.
  - For example: `.template-NuGet`

### 2. Clone the repo

Clone the repo locally, and open it in Visual Studio Code.
The [`.github`][github] repository needs to be added as an upstream remote
so the template sync can match up the commits in the new repo
with those in the [`.github`][github] repo. Execute the following commands:

```bash
# May need to configure an SSH key as well
git remote add upstream git@github.com:TaffarelJr/.github.git
git config remote.pushdefault origin
git fetch upstream
git reset --hard upstream/main
git push --force
```

### 3. Run the template sync

Next, we need to validate the template sync.
To do this, we need to get the sync workflow running.
Open the repo and go to `Settings` -> `Actions` -> `General`.

- Check `Allow GitHub Actions to create and approve pull requests`

Now go to `Actions` -> `Template Sync` -> `Run workflow` -> `main`
and click `Run workflow`. It should complete with no changes.

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

### 6. Override Repository settings

Most of the settings in the `settings.yml`
are fine to just live in the [`.github`][github] repo.
In this new template repo, we just need to override a few settings.
Replace the contents of the file with the following,
filling in the values as marked:

```yaml
_extends: .github

repository:
  #─────────────────────────────────────────────────────────────────────────────
  # "About" section (on repo home page)
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

Commit the changes to `main` with the message: `chore: customize repo settings`

### 7. Push the changes to GitHub

No need for a PR yet, just push the `main` branch up.
The settings should take effect almost immediately;
verify that the repo description and tags are showing on the home page.

### 8. Final repository configuration

Not all repo settings can be managed from `settings.yml`.
Some will still need to be set manually:

- `Settings`
  - `General`
    - Check `Limit how many branches and tags can be updated in a single push`
      - Up to `2` branches and tags can be updated in a push
  - `Moderation options`
    - `Code review limits`
      - Check `Limit to users explicitly granted read or higher access`
  - `Code security`
    - Enable `Private vulnerability reporting`
    - Enable `Dependency graph` _(if necessary)_
    - Enable `Grouped security updates`
    - Set up `CodeQL analysis`
      - Use `Default`

### 9. Custom labels

| Label           | Description                                 | Color   |
| :-------------- | :------------------------------------------ | :------ |
| `critical`      | Highest priority                            | #D93F0B |
| `dependabot`    |                                             | #0075ca |
| `needs-fix`     | Looking for a solution                      | #FF6300 |
| `needs-repro`   | Missing replication steps                   | #D97B0B |
| `template sync` | Changes replicated from template repository | #006B75 |

<!-- GitHub Footnotes -->

[github]: https://github.com/TaffarelJr/.github
