# Maintenance Notes

This repository is a curated usecase content repository. The public README files are manually edited source-of-truth documents, not generated build artifacts.

## Case catalogs

- [Claude Fable 5.2 catalog](fable-5-2/README.md) and its ten translated editions cover Cases 330–489. The matching structured index is [data/fable-5-2-use-cases.json](../data/fable-5-2-use-cases.json).
- The root README and its ten translated editions link to the current catalog and host Cases 1–329. The matching structured index is [data/use-cases.json](../data/use-cases.json).
- [Full Russian case notes](ru-original-case-notes.md) hold longer translations linked from the historic Russian README.
- [Update log](update-log.md) records content and maintenance changes.

## Case Format

The public README uses a custom usecase variant:

- Each case has a stable `<a id="case-x"></a>` anchor.
- Each case heading uses `### Case X:` and links to the original source.
- The first paragraph under the heading is a bold usage takeaway.
- The body keeps readable source-content notes instead of a generic summary label.
- `Type: ... | Date: YYYY-MM-DD` stays near the end of each case.

This intentionally differs from the stricter usecase template:

- No per-case quality badge is shown in public case headings.
- No `How to use it:` label is used.
- No `Tweet excerpt` label is used.
- Code blocks are used only for actual code, prompts, commands, or structured examples.

## Update Checklist

Before adding or changing a case:

- Update the English source README first.
- Keep the same case number, anchor, source link, creator link, type, and date across every localized README.
- Keep the Menu links pointed at the matching `#case-x` anchors.
- Credit every registered creator explicitly in the Acknowledge section.
- Confirm no placeholder translation text remains.
- Confirm every banner image path referenced by a README exists in `images/`.

## Update Intake

Collect public source candidates and deduplicate them against the README source links and both structured indexes. Review the original creator's post, concrete output, source media, and workflow details before selecting a case. Keep supporting posts attached to the same case rather than counting them as separate projects.

Update English first, then every localized README. Preserve exact prompt text when reproducing a prompt, and keep creator-reported timing and one-shot descriptions attributed to the creator.

Keep raw research collections, review queues, credentials, and temporary verification files outside the public repository. Submit selected content through a pull request.

## Validation Commands

Check both catalogs before opening a pull request:

```bash
git diff --check
node --check api-examples/node/messages.mjs
python3 -c 'import ast, pathlib; ast.parse(pathlib.Path("api-examples/python/messages.py").read_text())'
for catalog in . docs/fable-5-2; do
  for readme in "$catalog"/README*.md; do
    printf '%s ' "$readme"
    rg -c '^### Case [0-9]+:' "$readme"
  done
done
```

Review the 11 editions of each catalog against its JSON index. Verify case numbers, menu targets, source and creator links, type, date, and media. Inspect desktop and narrow GitHub renders after changing navigation or media.
