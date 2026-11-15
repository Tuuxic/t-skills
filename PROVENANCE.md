# Provenance

Where every skill comes from, what I changed, and how to pull in updates from the source.

Source: [mattpocock/skills](https://github.com/mattpocock/skills), imported at `4ae2317` (2026-11-05).

`upstream.json` maps each skill to its path in the source. The vendor branch `vendor/matt` holds an untouched copy of the source.

## Labels

- **upstream**: byte-identical to the source.
- **adapted**: from the source, with my edits. The edits are listed below.
- **own**: written for this library, no source.

The table states intent. For the exact lines, run `git diff vendor/matt -- skills/<skill>`. `python scripts/sync_upstream.py report` checks which skills currently differ from the source.

## Skills

| Skill | Label | What I changed |
|---|---|---|
| Every skill from the source not listed below (17) | upstream | |
| `implement`, `implement-spec` | adapted | Call `t-skills:code-review` by its namespaced name, because the bare name runs Claude Code's built-in `code-review`. The bare name stays as the fallback for other harnesses. |
| `flow`, `setup-project` | adapted | Renamed from `ask-matt` and `setup-matt-pocock-skills`, with the heading and the `agents/openai.yaml` display name to match. `setup-project`'s templates name no author repo: the triage table's first column is "Canonical role", and the GitHub guardrail keeps only the `gh repo view` check. |
| `code-review`, `implement-spec`, `to-spec`, `to-tickets`, `triage`, `wayfinder` | adapted | Call `/setup-project` by its new name. |
| `grilling` | adapted | A round is a question-tool popup of up to four questions, the most unblocking first, replacing the numbered list template, with a one-question plain message as the fallback. |
| `t-mode` | own | My full working style, written from my vault's conversation rules. The proof and writing rules are in my own words. Its `agents/openai.yaml` is hand-written. |
| `inbox-capture` | own | Written from my vault's `CLAUDE.md`, its templates, and one existing capture. Finds the vault per device (working directory, `SECOND_BRAIN_VAULT`, memory, or asks). |

Other files that are my own: `README.md`, `CLAUDE.md`, `PROVENANCE.md`, `personal/`, `upstream.json`, `scripts/`, and `.claude-plugin/`.

## Decisions

| Decision | Why |
|---|---|
| Build on Matt's skills, with pstack out for now | A fresh start from one paradigm instead of merging two. |
| Take all 27 stable skills | `flow` stays accurate without edits, and skills he calls by name are always installed. User-invoked skills cost no context until typed. `in-progress` and `misc` stay out. |
| Start from his text, and bring edits back when a real session shows the need | I can adapt freely, but only `grilling`'s popups earned a place in the reset. His setup skill already covers a local or "Other" (Notion) tracker. |
| Keep the question-tool popups in `grilling` | Matt rejects these for his skills. I prefer them, and "Other" still takes a free-text answer. |
| Namespace the two `code-review` calls instead of renaming the skill | Tested: a bare-name call resolves to Claude Code's built-in. Two one-line edits are the smallest fix that works in every session. Matt won't rename his skill, and a `CLAUDE.md` line only works where it's linked. |
| One `t-skills` plugin, with `inbox-capture` apart in `t-obsidian` | His skills call each other across folders, so a partial install would break real steps. |
| Style in both `personal/CLAUDE.md` and `t-mode` | I work from several devices. `CLAUDE.md` is the main home, symlinked per device. `t-mode` is the fuller version that travels with the plugin. |
| Rename skills that carry an author's name (`ask-matt` → `flow`, `setup-matt-pocock-skills` → `setup-project`) | The library is about the skills, not who wrote them. The README still credits Matt. The key in `upstream.json` sets the folder name, so his updates still merge, and `sync_upstream.py report` flags any old name a merge brings back. |
| Import his `agents/openai.yaml` | Keeps Codex working and the folders identical to the source, so the build needs no generator. |

The state before this reset is the tag `pre-matt-reset`, including pstack, its clash decisions, and my merged skills.

## Updating from the source

1. Import the source's latest version onto its vendor branch. This doesn't touch the current branch:

   ```
   python scripts/sync_upstream.py import matt
   ```

   The output shows which files changed in the source. It also lists skills that are new in the source (neither tracked nor in `left_out`).
2. Read what the source changed: `git show vendor/matt`.
3. Merge it: `git merge vendor/matt`. Skills labelled upstream update cleanly. For adapted skills, git applies the source's change on top of my edits, and it stops with a conflict only where both sides changed the same lines. Resolve conflicts against the decisions above.
4. Push the branch so other devices get it: `git push origin vendor/matt`.
5. For each skill new in the source, either add it to `skills` in `upstream.json` and import again, or add it to `left_out`.
6. If an update changes what a skill does, update its row here and in `README.md`.

## Bringing pstack back

`vendor/pstack` stays on `origin`, imported at `4dd1d05`. To bring it back, restore its entry under `sources` in `upstream.json` (see the tag `pre-matt-reset`) and add an entry under `skills` for each skill you want. Then run `python scripts/sync_upstream.py import pstack` and `git merge vendor/pstack`. Add its license back to `THIRD_PARTY_NOTICES.md`.
