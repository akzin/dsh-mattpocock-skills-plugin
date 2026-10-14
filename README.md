# dsh-mattpocock-skills-plugin

All **38 skills** from [Matt Pocock](https://github.com/mattpocock/skills) packaged
as a **DeepSeek Harness (DSH) bundle**. The skill bodies are unchanged; only the
directory layout is adapted so DSH can find them. See [NOTICE.md](NOTICE.md).

- **License:** MIT, copyright on the content held by Matt Pocock — [LICENSE](LICENSE).
- **Scope:** 38 skills, registered in the global skill layer, available on every surface.
- **One command to install.** No build step, no manual registration.
- **Not published to npm.** Installing goes through a local folder or directly
  from GitHub.

## Install

This plugin is a **DSH bundle**: a package that ships a `cordis.patch.yml`. You
install it with one command — `dsh plugin add` installs the package *and* records
it in the profile's bundle list, which is what makes DSH load it. There is
nothing to do by hand, and nothing to repeat: the registration stays across
restarts and updates.

### Requirements

- A working **DeepSeek Harness** install (`dsh` on your `PATH`).
- **pnpm** on your `PATH`. `dsh plugin` uses it under the hood, and tells you when
  it is missing. Node ships Corepack, which is the quickest way to get it:

  ```bash
  corepack enable pnpm
  ```

  Or install it directly: `npm install -g pnpm`.

### From the command line

Two routes work; there is no npm package.

```bash
# directly from GitHub
dsh plugin --profile web add github:akzin/dsh-mattpocock-skills-plugin
```

Or clone it first and install from the folder. Use an **absolute** path:

```bash
git clone https://github.com/akzin/dsh-mattpocock-skills-plugin.git ~/dsh-mattpocock-skills-plugin
dsh plugin --profile web add ~/dsh-mattpocock-skills-plugin
```

### Verify

After the restart the bundle is loaded and the skills are in the catalog:

```bash
dsh --profile web --dump-config | grep -A5 'skill-filesystem-mattpocock'
```

On **web** this route is required, not optional: the web profile ships the host
`skill-filesystem` row as `disabled` ("presets own local discovery"), so a bundle
that inserts its own row into the global skill layer is the only way to make the
skills visible on every surface.

### From the UI

DSH has plugin management (settings → plugins, plus the plugin manager). Paste
one of these into its add field:

    github:akzin/dsh-mattpocock-skills-plugin
    /absolute/path/to/dsh-mattpocock-skills-plugin

It installs the package and records the bundle, so the only thing left is a
restart. There is no registry name to type, because the package is not on npm.

> Install by absolute folder path if the UI cannot resolve the GitHub shorthand.
> The command line above does the same thing but shows its output, which is the
> faster route when something does not resolve.

## What you get

38 skills, alphabetically. Each description is taken from the skill's own
frontmatter.

| skill | what it does |
|---|---|
| `ask-matt` | Ask which skill or flow fits your situation. A router over the skills in this repo. |
| `chief-of-staff` | Pursue a long-running goal in a single session by co-ordinating subagents. |
| `claude-handoff` | Hand the current conversation off to a fresh background agent that picks up the work immediately. |
| `code-review` | Review the changes since a fixed point (commit, branch, tag, or merge-base) along two axes: Standards (does th |
| `codebase-design` | Shared vocabulary for designing deep modules. Use when the user wants to design or improve a module's interfac |
| `diagnosing-bugs` | Diagnosis loop for hard bugs and performance regressions. Use when the user says "diagnose"/"debug this", or r |
| `domain-modeling` | Build and sharpen a project's domain model. Use when discussing codebase terminology, writing or editing a GLO |
| `git-guardrails-claude-code` | Set up Claude Code hooks to block dangerous git commands (push, reset --hard, clean, branch -D, etc.) before t |
| `grill-me` | A relentless interview to sharpen a plan or design. |
| `grill-with-docs` | A relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go. |
| `grilling` | Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thin |
| `handoff` | Compact the current conversation into a handoff document for another agent to pick up. |
| `implement` | Implement a piece of work based on a spec or set of tickets. |
| `implement-spec` | Implement the result of /to-spec and /to-tickets in code. |
| `improve-codebase-architecture` | Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whicheve |
| `loop-me` | Grill me about specs for the workflows I want to build, within this workspace. |
| `migrate-to-shoehorn` | Migrate test files from `as` type assertions to @total-typescript/shoehorn. Use when user mentions shoehorn, w |
| `pr` | Use when writing a PR body. |
| `prototype` | Build a throwaway prototype to answer a design question. Use when the user wants to sanity-check whether a sta |
| `research` | Investigate a question against high-trust primary sources and capture the findings as a Markdown file in the r |
| `retro` | Conduct a retrospective on a coding session. |
| `scaffold-exercises` | Create exercise directory structures with sections, problems, solutions, and explainers that pass linting. Use |
| `setup-matt-pocock-skills` | Configure this repo for the engineering skills: set up its issue tracker, triage label vocabulary, and domain  |
| `setup-pre-commit` | Set up Husky pre-commit hooks with lint-staged (Prettier), type checking, and tests in the current repo. Use w |
| `setup-ts-deep-modules` | Wire dependency-cruiser into a TypeScript repo so each package is a deep module, with implementation hidden in |
| `tdd` | Test-driven development. Use when the user wants to build features or fix bugs test-first, mentions "red-green |
| `teach` | Teach the user a new skill or concept, within this workspace. |
| `to-questionnaire` | Turn a decision you can't fully answer into a questionnaire for someone else to fill in. |
| `to-spec` | Turn the current conversation into a spec and publish it to the project issue tracker: no interview, just synt |
| `to-tickets` | Break a plan, spec, or the current conversation into a set of tracer-bullet tickets, each declaring its blocki |
| `triage` | Move issues and external PRs through a state machine of triage roles, categorise, verify, grill if needed, and |
| `wait-what` | Stop. That last message did not land: re-pitch it. |
| `wayfinder` | Plan a huge chunk of work (more than one agent session can hold) as a shared map of decision tickets on your i |
| `wizard` | Generate an interactive bash wizard that walks a human through steps only they can perform. Use when provision |
| `writing-beats` | Writing, exploit; assemble raw material into a journey of beats, grounding each term before a beat leans on it |
| `writing-for-agents` | Writing documents for agents. Use when creating or editing skills, or modifying AGENTS.md or CLAUDE.md. |
| `writing-fragments` | Writing, explore: mine raw fragments, no structure yet. |
| `writing-shape` | Writing, exploit: shape raw material into an article, paragraph by paragraph. |

## Why no dependencies

`@deepseek-ai/dsh-skill-filesystem` — the plugin that actually reads the skills —
is **not** listed in `package.json`. It ships with DSH itself.

That is a deliberate choice with a history: an earlier port of this same skill
set declared it with the range `"*"`. That resolved to the package's `latest`
tag, which sits on an **older release line** whose peer dependencies did not
match the runtime. The compatibility check then disabled the plugin row **and all
38 skills** with it.

So do not add a loose range here. If you must pin it, use the exact version your
DSH installation ships.

## Updating to a newer upstream

See [NOTICE.md](NOTICE.md). There is deliberately no sync script: it would create
a second source of truth about what belongs in this repository.

## For maintainers

There is nothing to build: `skills/` is Markdown and `cordis.patch.yml` is YAML.
So this repository has no `prepare` script and no workflow, and installing means
copying files. If a build is ever needed, that is the moment to add one — not
before.

## License

MIT — see [LICENSE](LICENSE). The skill content is Matt Pocock's
([mattpocock/skills](https://github.com/mattpocock/skills)); this repository
packages that content for DSH and changes none of it.
