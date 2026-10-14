# Provenance and what was changed

The **skill content is copied verbatim**. This plugin changes nothing in Matt
Pocock's text; it only packages it so DeepSeek Harness can find it.

- **Upstream:** [mattpocock/skills](https://github.com/mattpocock/skills)
- **License:** MIT — see [LICENSE](LICENSE). Copyright on the skill content is
  held by Matt Pocock.
- **Scope:** all 38 skills in the upstream tree.

## The only transformation: flattening

Upstream files its skills under a category:

    skills/<category>/<name>/SKILL.md

DSH discovers exactly **one level deep**:

    <root>/<name>/SKILL.md

So they are flattened: `skills/engineering/code-review/` becomes
`skills/code-review/`. No file content is altered.

## Note: not all 38 are still maintained

Upstream splits its skills into four categories and says this about them:

| category | count | status according to upstream |
|---|---|---|
| `engineering` | 20 | maintained |
| `productivity` | 7 | maintained |
| `misc` | 4 | **frozen and unmaintained** |
| `in-progress` | 7 | **experimental beta channel** |

This plugin ships **all of them**, including the frozen and experimental ones, so
that you have a complete copy of what upstream publishes. If you only want the
maintained set, remove the skills from `misc` and `in-progress` after installing.

## Updating to a newer upstream

There is deliberately no sync script: that would create a second source of truth
about what belongs in this repository. Updating is manual and small:

1. Fetch upstream and note the commit you are moving to.
2. Copy the skill directories, flattened (`<category>/<name>/` → `<name>/`).
3. Update the commit hash in this file.

The skill content is the only variable; `cordis.patch.yml` and `package.json`
change only when the package name or the DSH wiring changes.
