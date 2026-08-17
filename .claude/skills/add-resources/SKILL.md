---
name: add-resources
description: Add learning resources (local files, PDFs, notes, URLs) to a topic's resource database, or web-search to fill coverage gaps. Use when the user provides study material, pastes links, or a roadmap unit has no covering resource.
---

Tone here matches the rest of the harness: terse and flat — no praise, no filler, no personality. Report what was ingested and what's missing, nothing more.

You are building the resource database for a topic. Everything ends up as a local file under `topics/<slug>/resources/` plus an index entry in `topics/<slug>/resources.md` — the teaching loop only trusts what's indexed.

Determine the topic from the arguments or conversation; if ambiguous, ask. If the topic directory doesn't exist yet, this is running inside `/learn` intake — use the paths it created.

## Ingesting

- **Local files** (PDFs, slides, notes): ask the user to drop them in `topics/<slug>/resources/` (or copy them there from a path they give you). Read each one (PDFs page-by-page as needed).
- **URLs**: fetch with WebFetch. Save a readable markdown extract to `resources/<descriptive-name>.md` with the source URL at the top. If a URL can't be fetched (paywall, video), index it anyway with a note on what it covers, marked `unreadable — user-side resource`.
- **Web search** (gap-filling): only with the user's permission. Search, pick 1–2 solid sources per gap, save extracts to `resources/` like URLs. Prefer explanatory sources (tutorials, lecture notes) over reference dumps.

## Indexing — `resources.md`

One entry per resource:

```markdown
## <name> (`resources/<file>` or URL)
- **Covers**: concepts/units this addresses
- **Level**: intro / course-level / advanced — and register fit (good for eli5? intern?)
- **Quality**: one line — is it explanatory or just reference? any known gaps or errors?
- **Best for**: which roadmap units should cite it
```

## Gap check (called during roadmap generation)

Compare `roadmap.md` units against the **Covers** lines. For any unit with no covering resource, tell the user which units are uncovered and ask: web-search to fill them, or proceed teaching from general knowledge? Record the answer per unit in `resources.md` under a `## Gaps` section so it isn't re-asked.

Resources are raw material, never the lesson: the teach loop translates them through analogy and example per the Teaching Contract — it never recites them.