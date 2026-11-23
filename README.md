# Scopecheck

A Claude Code skill that keeps coding tasks in scope. It guides Claude to
look at the existing code first, reuse what already works, and make the
smallest change that fully solves the problem. Inspired by Ponytail.

## What it does

When you run `/scopecheck <task>`, Claude:

1. Checks your uncommitted changes, the code the task touches, nearby code
   and the related tests.
2. Looks for an existing helper, component or pattern before writing new code.
3. Makes the smallest complete change, including edge cases, without touching
   your unrelated edits.
4. Adds new files, helpers or dependencies only when they solve a concrete
   problem.
5. Runs the relevant checks, reviews the diff, and reports what it verified.

## Installation

Copy the skill folder into your project (shared with your team):

```sh
mkdir -p .claude/skills
cp -r path/to/scopecheck/.claude/skills/scopecheck .claude/skills/
```

Or install it for all your projects:

```sh
mkdir -p ~/.claude/skills
cp -r path/to/scopecheck/.claude/skills/scopecheck ~/.claude/skills/
```

Start a new Claude Code session; `/scopecheck` appears in the `/` menu. The
skill only runs when you invoke it.

## Usage

```
/scopecheck Fix the empty search message using the existing empty-state component
```

## Example (illustrative)

Task: show a message when a search returns no results.

- Without Scopecheck, Claude might write a new `NoResults` component with its
  own styles and a new icon package.
- With Scopecheck, Claude first searches the codebase, finds the existing
  `EmptyState` component already used on other pages, and renders
  `<EmptyState title="No results" />` in the search view. It also handles the
  empty query case, runs the search tests, and leaves your unrelated edits
  alone. One file changed, no new dependencies.

## License

MIT. See [LICENSE](LICENSE).
