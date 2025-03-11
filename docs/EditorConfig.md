# What is an `.editorconfig` File?

An `.editorconfig` file is a simple, plain-text configuration file
that helps maintain consistent coding styles across various editors and IDEs.
It defines formatting rules such as indentation, line endings,
character encoding, and more, ensuring that all contributors to a project
adhere to the same style guidelines.

## Why is it Important?

- **Consistency Across Editors:** Different editors and IDEs can
  interpret default settings in various ways.
  An `.editorconfig` file standardizes these settings,
  so the same file appears consistent regardless of the tool used.
- **Improved Collaboration:** When every team member uses the same code style,
  it reduces formatting discrepancies.
  This consistency makes code reviews and merging changes smoother.
- **Automated Formatting:** Many popular code editors (like
  [Visual Studio Code][vsCode], [Sublime Text][sublime], [Atom][atom],
  and [others][others]) natively support EditorConfig or have plugins available.
  This means the formatting rules are automatically applied
  when files are opened or saved.

## How do I use it?

Simply install the [appropriate plugin/extension][others] in your IDE of choice,
and the styles should be handled automatically for you.

## Note about Visual Studio Projects

Visual Studio allows many of it's own settings
to be added to the `.editorconfig` file
so they can be shared between developers.
However, these settings will only be applied—obviously—if
the developer is actually using Visual Studio.
So this is the recommended IDE for C# projects.

<!-- Public Footnotes -->

[vsCode]: https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig
[sublime]: https://packagecontrol.io/packages/EditorConfig
[atom]: https://github.com/sindresorhus/atom-editorconfig
[others]: https://editorconfig.org/#download
