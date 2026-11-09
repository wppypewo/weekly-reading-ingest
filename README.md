# Weekly Reading Ingest

English | [繁體中文](README.zh-TW.md)

A weekly close-reading curator: a pair of Claude Code skills that find one article or paper worth reading closely each week and, only after you confirm, turn it into notes in an Obsidian knowledge base.

- **Two stages with a human in between.** `weekly-reading-curate` searches and scores candidates and writes a report with one main pick and two backups; it never writes to the knowledge base. `weekly-reading-ingest` acts only on one of three exact confirmations ("確認主選" confirm main pick, "改選備選 A" / "改選備選 B" switch to backup A / B). Replies like "let me look" or "maybe later" do not count.
- **Hard limits on writing.** It never edits the knowledge base's index, log or lint files, never touches existing special folders, never adds files inside project folders, and never puts candidate reports into the vault. The full list is in [`SAFETY.md`](SAFETY.md).
- **One confirmation, a full set of notes.** A confirmed pick becomes a source note, concept note, project link, review card and weekly log entry. Each is written as a preview first, passes a safety check, then goes into the vault, followed by the vault's index and lint scripts.

A personal tool for one user: no app, no multi-user support, no local OS scheduler. The skills, documents and reports are in Traditional Chinese.

## Status

- The manual loop works end to end and has completed one real ingest: candidates → confirmation → previews → write → index → lint → commit.
- Weekly automatic triggering (a Claude cloud routine) **has not been tested**; `routine.enabled` stays `false` in the config. The readiness assessment and the first-run checklist are in [`docs/`](docs/).

## A complete example

[`runs/real-curate-001/`](runs/real-curate-001/) holds everything from the first real run:

| File | What it is |
|---|---|
| `candidates.md` | Candidate report: this week's theme, the main pick and two backups, each scored on source quality, idea density, long-term value, relevance and fit for Obsidian |
| `ingest-preview/` | The six previews produced after confirmation and before writing: source note, concept note, project link, review card, weekly log, safety check |
| `closeout.md` | Results of the write, index, lint and commit |

## How it works

| File | Contents |
|---|---|
| [`.claude/skills/weekly-reading-curate/`](.claude/skills/weekly-reading-curate/SKILL.md) | Stage one: read the config and vault context, search, score, write the candidate report |
| [`.claude/skills/weekly-reading-ingest/`](.claude/skills/weekly-reading-ingest/SKILL.md) | Stage two: after a confirmation, produce previews, check them, write them |
| [`weekly-reading.config.json`](weekly-reading.config.json) | Vault path, allowed concept domains and source folders, main-pick thresholds, modes |
| [`SAFETY.md`](SAFETY.md) | Write scope, hard limits, safety checklist |
| [`FAILURE-HANDLING.md`](FAILURE-HANDLING.md) | How each failure stops and is reported |
| [`MODES.md`](MODES.md) | strict (six previews, lint right away) and quick (merged preview, lint may be deferred); both require the same human confirmation |
| [`routine-design.md`](routine-design.md) | Design of the weekly automatic trigger (cloud routine, untested) |
| [`docs/SPEC.md`](docs/SPEC.md) | Full specification: positioning, non-goals, confirmation phrases, hard limits, domain rules, processed policy, title format |

Open this repository in Claude Code and say "本週精讀" (this week's reading) to start stage one. To actually write notes, point `vaultRoot` in `weekly-reading.config.json` at your own Obsidian vault. The skills assume the vault already has index and lint scripts and a particular folder structure; adapting them to another vault means changing the config and `SAFETY.md` first.

## License

[MIT](LICENSE). Articles summarised or cited in the `runs/` example belong to their authors; the reports contain only links and summaries.
