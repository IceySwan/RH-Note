---
name: latex-git-commit
description: Inspect LaTeX repository changes and generate or perform focused Git commits with a one-sentence commit message and a markdown changelog using version/date headings with Add/Fix categories. Use when the agent needs to summarize, document, stage, or commit changes to .tex, .bib, .cls, or related mathematical writing files.
---

# LaTeX Git Commit & Changelog

## Workflow

1. Read repository instructions and inspect `git status --short`.
2. Inspect both unstaged and staged changes with `git diff --unified=0` and `git diff --cached --unified=0`.
3. Read relevant untracked `.tex`, `.bib`, and `.cls` files reported by `git status --short`; ordinary `git diff` omits their contents.
4. Separate source changes into additions, mathematical corrections, and supporting edits. Exclude the pending `CHANGELOG.md` edit from this classification to prevent self-referential entries.
5. Verify each mathematical statement from its local definitions and surrounding derivation. Preserve the author's notation.
6. Resolve line numbers against the final updated source file with a numbered view such as `rg -n` or PowerShell line enumeration. Use the first line of a multiline display as its location.
7. Draft the commit sentence and changelog using the formats below.
8. Stage or commit only the files requested by the user. Preserve unrelated working-tree changes.
9. Before committing, show the proposed commit sentence and changelog unless the user explicitly requests immediate execution.

## Commit sentence

Write **one concise sentence** describing the dominant mathematical change. Use an imperative Conventional Commit form:

```text
docs(latex): clarify the residue conditions and correct the jump-matrix sign
```

- Keep the subject **on a single line**, aim for at most **72 characters**, and **omit terminal punctuation**.
- Combine tightly related additions and corrections in the same sentence.
- Use `fix(latex)` when the principal change repairs a mathematical error; use `docs(latex)` for exposition, derivation, or notation improvements.
- Express the subject as one sentence and one line.

## Changelog

Return the changelog entry in the following **Markdown** format. Do **not** use LaTeX environments.

```markdown
## v0.36-2026.07.15

### 2026.07.14

- **Add**: 在留数条件的推导中补充离散谱贡献，说明该项刻画极点对逆散射重构的影响。
- **Fix**: 修正 `content/chapter.tex:128` 的跳跃矩阵符号：`$J=I-2\pi i\,fg^{\mathsf T}$`。
- **Fix**: 修正 `content/chapter.tex:203` 的 Jordan 块索引：`$\begin{pmatrix}a&1\\0&a\end{pmatrix}$`。
```

### Heading rules

| Level | Format | Example | When to use |
|-------|--------|---------|-------------|
| Secondary | `## v<major>.<minor>-<YYYY.MM.DD>` | `## v0.36-2026.07.15` | On each actual release / merge to release branch |
| Tertiary | `### YYYY.MM.DD` | `### 2026.07.14` | For every working-tree commit (sub-version entries before a release) |

- Create one **secondary heading** per release. Take the version and release date from explicit user input or an existing active release block. Ask for the target version and release date when both sources are absent or ambiguous; never invent or overwrite a release identifier.
- Create one **tertiary heading** for the commit date. The project allows at most one commit per date.
- Keep release blocks and their tertiary date sections in reverse chronological order.

### Item rules

- Prefix each item with `- ` (unordered list).
- Use `**Add**` for new mathematical content or exposition.
- Use `**Fix**` for corrections of mathematical errors.
- Use `**Refactor**` for reorganization or rewording without semantic change.
- Use `**Chore**` for reference updates, label changes, formatting, or class-file edits that do not affect mathematical content.
- For every **Add** item, state what the addition **means mathematically**: the object it characterizes, the role it plays in a proof or reconstruction, or the consequence it establishes.
- For every **Fix** item, include the **file path** and **final updated line number** (`path:line`) and copy the **exact corrected formula source** from that file. Wrap a single-line formula in backticks, including its `$...$`, `\(...\)`, or other original delimiters. Use a fenced `latex` block for a multiline formula and preserve its complete environment delimiters.
- When a single commit contains both additions and corrections, list **Add** items before **Fix** items.

### Changelog file

- The changelog lives at `CHANGELOG.md` in the repository root.
- If the file does not exist, create it with a top-level `# Changelog` heading followed by the first secondary heading.
- Insert a new release block immediately below `# Changelog`.
- Insert the commit's tertiary date section immediately below its target secondary release heading, above older tertiary sections in that release block.
- Preserve every existing release block, heading, and entry verbatim outside the insertion point.

## Accuracy checks

- Derive locations from the updated working tree after all edits.
- Copy formula source directly from the updated file; preserve commands, delimiters, subscripts, superscripts, and signs exactly.
- Confirm that each claimed mathematical significance follows from the changed passage and nearby definitions.
- Confirm that the commit subject is a **single sentence** and contains no terminal punctuation.
- Confirm that the changelog uses valid Markdown headings and list syntax.
- Re-read the resulting `CHANGELOG.md` and confirm the hierarchy `# Changelog` → `## version-date` → `### commit-date`.
- Inspect `git diff --check` and the final staged diff before committing.

## Output

Provide exactly these two blocks when drafting:

```text
Commit:
<one sentence>

Changelog:
<markdown changelog entry>
```
