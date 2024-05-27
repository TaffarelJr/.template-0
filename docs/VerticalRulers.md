# Vertical Rulers

Vertical rulers (or guidelines) are visual markers in your code editor
that help you maintain consistent line lengths.
They serve as reference points to help developers
keep their lines of code short. This is especially important
during activities like side-by-side code comparisons,
as not all developers have ample screen real-estate.

## Recommended Ruler Positions

For this repository, the recommendations are:

- Ideally, we prefer to keep under 80 characters per line.
- It's OK to go to 100 characters, if it's more asthetically pleasing.
- On occasion, 120 characters might even be acceptable.
- Over 120 characters should be split across lines.

We understand not all file types support splitting lines in all cases.
If it's not supported—such as with a long URI in a Markdown file—then
don't worry about it. It's not the end of the world!
But to facilitate the cases where it _is_ supported,
it's highly recommend to use vertical rulers or guidelines
in your IDE of choice.

## How do I apply them?

These recommendations are already included in the `.editorconfig` file.
If your IDE supports it (via a plugin or built-in functionality),
the vertical rulers should be displayed automatically.
Otherwise, you may need to manually set them up. For example:

- In Visual Studio you can simply install the
  [Editor Guidelines][guidelines] extension.
- In Visual Studio Code you'll need to go into
  `Settings` -> `Rulers` and add something like the following JSON:

```json
"editor.rulers": [
  {
    "column": 80,
    "color": "#00ff0050"
  },
  {
    "column": 100,
    "color": "#ffff0075"
  },
  {
    "column": 120,
    "color": "#8b0000ff"
  }
],
```

Happy coding!

<!-- Public Footnotes -->

[guidelines]: https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelinesPreview
