# Editing Requirements

Apply the following rules to every Markdown note in this directory and all of its subdirectories.

## Links

- Every internal link must work in both Obsidian and Markdown Preview Enhanced.
- Use standard Markdown links with relative paths.
- Do not use Obsidian-only wikilinks.
- When a relative path contains spaces or punctuation, wrap the destination in angle brackets.
- After adding, renaming, or moving a note, update and verify every affected link.

## Mathematics

- Use only inline dollar delimiters or display dollar delimiters for mathematical expressions.
- Inline mathematics must have no whitespace immediately inside its delimiters. Write `$expression$`, never `$ expression $`.
- Display mathematics must place each delimiter on its own line:

  ```markdown
  $$
  expression
  $$
  ```

- Do not place display delimiters and an expression on the same line.
- Do not use `\(...\)`, `\[...\]`, equation environments, align environments, or any other mathematics delimiters.
- Do not alter dollar signs or mathematical-looking content inside fenced code blocks or inline code spans.

## Tables

- Put a blank line before every Markdown table, especially when the preceding line is a heading, bold text, list item, or paragraph.
- Put a blank line after every Markdown table before starting the next block.
- In table cells, wrap literal Markdown metacharacters or command syntax in inline code spans, such as `*`, `?`, `[characters]`, `|`, `-a`, or `Ctrl-a`.

## Verification

- Verify that all internal Markdown links resolve to existing files.
- Verify that all local image links resolve to existing assets.
- Verify the link, table, and mathematics rules before completing an edit.
