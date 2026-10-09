# Contributing

Thanks for considering a contribution. This is a small static site, so the bar is
low — but there is one non-obvious trap described below that will bite anyone
who edits the HTML naively.

## Reporting a bug

Open an issue with the page name, what you expected, and what happened. A
screenshot helps for anything visual.

## Before you start

For anything beyond a typo fix, open an issue first. The site has no build step
and no test suite, so there is no automated safety net — a quick conversation
prevents duplicated effort and wasted patches on the same problem.

## The RSC payload trap

> [!WARNING]
> Every page stores its content in **two** places: the visible markup, and a
> Next.js RSC payload embedded in `<script>` blocks. React re-renders from the
> payload on load. Edit only the markup and your change silently reverts.

Search for `__next_f.push` to find the payload.

What is safe to change by hand:

- Text, labels, and headings
- External URLs
- Adding or removing whole elements, if you follow the existing shape exactly

What is not:

- Reordering or restructuring elements. The payload is positional — a change in
  nesting order breaks decoding for that entire row.
- Editing the keys, IDs, or reference markers (`$L2a`, `"01"`, and similar).
  These are an internal addressing scheme, and dangling references throw during
  hydration.

If you break the payload, the page renders but React throws on load. Verify
after any structural change:

```bash
grep -c '__next_f.push' index.html   # row count should be unchanged
```

## Previewing your change

```bash
python3 -m http.server 8000
```

Serve from the repository root over `http://`. Opening the file directly will
render unstyled.

Then check all three pages, not just the one you edited — the payload is shared
between them in places, and a search-and-replace will hit all of them at once:

```bash
grep -rn 'your-change' --include=*.html --include=*.js .
```

A change that should appear on one page but appears on three means a global
replace went too far.

## Style

- Match the surrounding code. There is no linter or formatter configured.
- Keep the existing Tailwind class strings intact; reordering them breaks the
  generated stylesheet's ordering assumptions.
- Comments explain *why*, not *what*. Most files here are generated-looking
  markup, so a short note beats a restatement.
- No emoji in code or file contents.

## Adding a project card

Project cards are data, but they live in both the markup and the payload. Adding
one means editing both. The tags on each card come from the GitHub language API
for that repository.

## Commit messages

Follow the existing style — a short imperative summary line, and a body
explaining what changed and why when the reason is not obvious from the diff.

```
fix theme toggle icon state on first load
```

## Pull requests

Keep them focused on one change. Describe what you changed, how you verified it,
and note anything you deliberately left out.

## Licensing

Contributions are accepted under the [MIT License](LICENSE). By opening a pull
request you agree to your work being distributed under those terms.

By participating you are expected to uphold the [Code of Conduct](CODE_OF_CONDUCT.md).
