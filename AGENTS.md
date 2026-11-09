# dylan/claude

A public marketplace of Claude Code plugins, named `dylan`. Users install a plugin as `<plugin-name>@dylan`, or install its skills alone with `npx skills add dylan/claude`. The plugins are listed in `.claude-plugin/marketplace.json` and documented in `README.md`.

## Layout

- `plugins/<name>/.claude-plugin/plugin.json` is the plugin manifest.
- `plugins/<name>/skills/<skill>/SKILL.md` holds each skill; `plugins/<name>/agents/` holds agents.
- `.claude-plugin/marketplace.json` lists every plugin.
- `README.md` has one section per plugin, and `CHANGELOG.md` has one entry per release.

## Rules

- **Keep each plugin's version the same in `plugin.json` and its `marketplace.json` entry.** When they differ, the plugin manifest wins without any warning, so a release can ship with the wrong version.
- **Start every `source` path in `marketplace.json` with `./`.** Both Claude Code and the `npx skills` CLI skip sources without it.
- **Give every `plugin.json` and marketplace entry `name`, `description`, `version`, `author` (an object with `name`) and `keywords` (an array).** The marketplace entry repeats the manifest's fields, so change both together.
- **List each plugin's skills in its marketplace entry's `skills` array**, as `./skills/<skill>` paths. The `npx skills` CLI uses that list to group skills under their plugin; without it, every skill lands in one flat list.
- **Add a `CHANGELOG.md` entry for every version bump**, newest first, headed `## <plugin> v<version> — <YYYY-MM-DD>`. A new plugin's first bullet is `**New plugin:** <what it is>`.
- **Add a `README.md` section for every new plugin**, with a summary, the install command and a paragraph on each skill or agent.
- **Run `claude plugin validate .` before committing.** It should pass with no warnings.
- **Use LF line endings.** `.gitattributes` enforces them; a CRLF file shows up as a whole-file diff.
- **Never commit secrets or private data.** The repository is public: no API keys, tokens, `.env` files, personal information or internal URLs.

## Gotchas

- **Edit `marketplace.json` by hand or with targeted inserts.** Rewriting it through `json.dumps` reflows every `keywords` array onto separate lines and turns a one-entry change into a 70-line diff.
- **Bump the version, or reinstall, to test a change.** `claude plugin update` compares version numbers, so an edited plugin at the same version stays stale. While testing locally, run `claude plugin marketplace update dylan`, then uninstall and reinstall the plugin.
- **Write skills for any agent.** The `npx skills` CLI installs them into Codex, Cursor and others, without agents, hooks or plugin variables. Refer to a skill's own files as sitting next to its `SKILL.md`; `${CLAUDE_SKILL_DIR}` may appear as the Claude Code form, but never `${CLAUDE_PLUGIN_ROOT}`. Name MCP tools by the server's own tool name, describe tools by what they do ("search files") instead of a Claude Code tool name (`Grep`), and say "the agent", not "Claude". Anything that needs an agent definition or a hook stays Claude Code only, and the README says so.
- **Don't put repo-maintenance skills in `skills/` or `.claude/skills/` at the root.** The `npx skills` CLI searches both folders and would offer those skills to every user who installs from this repo. Repo rules belong in this file.
