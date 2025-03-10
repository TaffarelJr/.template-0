# Conventional Commits

[Conventional Commits][cc] is a lightweight specification for creating
consistent, readable, and meaningful commit messages.
It establishes a common language that not only improves collaboration
but also supports automation tools, such as changelog generators
and versioning systems.

## How does it work?

It encourages/requires the use a structured commit message format
that clearly communicates the intent of the change
in a both human- and machine-readable format.
A good commit message follows this structure:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- **Type:** Indicates the nature of the commit (e.g., `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`).
- **Scope _(optional)_:** Provides context about the section of the code affected.
- **Description:** A brief (one-line) summary of the change.
- **Body _(optional)_:** More detailed explanation. (Can be multiple lines.)
- **Footer _(optional)_:** Metadata such as breaking changes or issue references.

If you're new to this style of commit message,
there are several good cheat sheets out there
that can help you get familiar with it:

- [Dash][kapeli]
- [Bengt Brodersen][qoomon]
- [Yaroslav Vorobev][zekfad]

All commit messages in this repository should follow this template
for consistency, as well as for automatic changelog generation and version bumping.
To help make this easier, a custom Git commit message template
is included in the repo - and can be added to your Git tooling of choice
by running the following command from the root of the repo:

```bash
git config commit.template .gitmessage
```

Happy committing!

<!-- Public Footnotes -->

[cc]: https://www.conventionalcommits.org
[kapeli]: https://kapeli.com/cheat_sheets/Conventional_Commits.docset/Contents/Resources/Documents/index
[qoomon]: https://gist.github.com/qoomon/5dfcdf8eec66a051ecd85625518cfd13
[zekfad]: https://gist.github.com/Zekfad/f51cb06ac76e2457f11c80ed705c95a3
