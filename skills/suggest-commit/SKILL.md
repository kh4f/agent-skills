---
name: suggest-commit
description: Suggest conventional commit messages from Git changes. Use when asked to suggest a commit message.
---

## Workflow
1. Analyze staged changes (fallback to unstaged if empty)
2. Use any user note as supporting context for intent, motivation, or footer details
3. Follow the commit message guidelines below
4. Produce three commit message options, each in its own fenced `markdown` code block

## Commit Message Guidelines

### Style
- Use American English.
- Use backticks for code entities and paths.
- Preserve official capitalization of tech/brand names (e.g., Node.js, GitHub, Bun, tsdown).

### Format
```markdown
<type>(<scope>): <subject>

<body>

<breaking changes>

<footer>
```

- `<type>`, `<scope>`, and `<subject>` are mandatory
- `<body>`, `<breaking changes>`, and `<footer>` are optional

### Header

#### `type`
Pick the best match for the primary intent of the change:

1. `feat`: add a new user-facing capability
2. `fix`: correct broken or incorrect behavior
3. `refactor`: improve code or structure
4. `perf`: improve performance
5. `style`: change formatting, styling, or purely visual presentation
6. `chore`: perform maintenance, dependency, tooling, or housekeeping work
7. `build`: change build tooling, packaging, or bundling behavior
8. `test`: add or update tests
9. `ci`: change CI workflows or automation
10. `docs`: add or update documentation

#### `scope`
Choose the narrowest stable area that best describes the change.

Prefer a feature or subsystem name.

#### `subject`
The subject should be:
- imperative
- present-tense
- lowercase (except for proper nouns, acronyms, and official tech/brand names)
- concise and specific
- free of a trailing period

Prefer the outcome over implementation trivia. Good subjects usually start with verbs like `add`, `fix`, `update`, `remove`, `refactor`, `rename`, `improve`, and similar verbs.

### Details

#### `body`
Skip the body if the header is self-explanatory.

Add a body when:
- the reason for the change is not obvious from the subject
- the behavior change needs a little extra context
- the user supplied motivation is worth preserving

#### `BREAKING CHANGE`
If the change is breaking:
- add `!` before the colon in the header
- add a `BREAKING CHANGE:` section in the details

Use `BREAKING CHANGE:` only when the diff clearly introduces an incompatible API, config, CLI, output, or behavior change.

For multiple breaking changes, use bullet points after `BREAKING CHANGE:`.

#### `footer`
Add a footer when the user asks to include issue or PR references.

Typical footer verbs:
- `Fixes #123`
- `Closes #123`
- `Refs #123`

### Commit Message Examples
```markdown
feat(playlist-sorting): auto-refresh grid on playlist rename

Monitor `browse/edit_playlist` requests and refresh the grid to reflect updated playlist names.
```

```markdown
fix(changelog-gen): use correct content for `BREAKING CHANGES` section

Previously, when a commit had a `breakingChanges` property, the changelog would incorrectly display the commit's `subject` in the `BREAKING CHANGES` section instead of the actual `breakingChanges` content.

Fixes #123
```

```markdown
test(cli): use `runCli` function instead of executing `dist/cli.js`

Remove the need for building the project before running tests.
```

```markdown
feat(config)!: add support for multiple profiles with CLI `--profile` flag

BREAKING CHANGE: Changed alias for `prerelease` option to `P` to reserve `p` for the new `--profile` option.

Closes #123
```

```markdown
refactor(config)!: simplify config by always reading current version from `package.json`

BREAKING CHANGE: The `packageFiles` option has been removed. The current version is now always read from `package.json`.
```

```markdown
refactor(changelog-gen)!: replace `stdout` and `outputFile` options with unified `output`

BREAKING CHANGE: The `stdout` and `outputFile` options have been removed from changelog configuration. Use the new `output` option with `stdout` for console output or a file path string for file output.
```