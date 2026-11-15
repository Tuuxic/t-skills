# Skill library

A personal library of agent skills, built on a source's skills plus my own, and shipped as installable plugins.

## Language

### Origin

**Source**:
An outside repo that skills are imported from, such as Matt Pocock's skills.
_Avoid_: Upstream (for the repo)

**Upstream skill**:
A skill whose text is identical to its source's. An adapted skill whose edits are all removed is an upstream skill again.
_Avoid_: Matt skill, vendored skill

**Adapted skill**:
A skill from a source whose text differs from the source's because of my edits.
_Avoid_: Modified skill, fork

**Own skill**:
A skill written for this library, with no source.
_Avoid_: Local skill, my own skill, personal skill

**Left-out skill**:
A skill in a source that this library chooses not to track.
_Avoid_: Excluded skill

**Vendor branch**:
The branch that holds an untouched copy of one source.
_Avoid_: Upstream branch

### Distribution

**Plugin**:
An installable bundle of skills from this library, such as `t-skills` or `t-obsidian`.
_Avoid_: Group
