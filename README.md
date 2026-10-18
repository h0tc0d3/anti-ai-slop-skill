# anti-ai-slop-skill

An [Agent Skill](https://agentskills.io/specification) for writing and editing
prose without stock AI phrasing or repetitive rhythm. It covers posts, emails,
documentation, and other writing while preserving the author's meaning and
voice. Code, config, logs, commands, payloads, and quoted text stay intact.

## Install

Clone the repository into your tool's skills directory. For Codex and other
tools that read `~/.agents/skills/`:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/h0tc0d3/anti-ai-slop-skill.git ~/.agents/skills/anti-ai-slop-skill
```

Keep the final directory named `anti-ai-slop-skill` to match the skill's `name`.
Include `references/` alongside `SKILL.md`; copying the main file alone leaves
its rules incomplete. For a project installation, use a project directory from
the table and commit the whole skill folder.

### Tool directories

Each entry is a parent directory: the skill belongs at
`<directory>/anti-ai-slop-skill/SKILL.md`. Tool names link to their installation
docs.

| Tool | Project directory | Personal directory |
| --- | --- | --- |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/` | `~/.claude/skills/` |
| [Codex](https://developers.openai.com/codex/skills/) | `.agents/skills/` | `~/.agents/skills/` |
| [Qwen Code](https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/) | `.qwen/skills/` | `~/.qwen/skills/` |
| [Cline](https://docs.cline.bot/customization/skills) | `.cline/skills/` | `~/.cline/skills/` |
| [Zoo Code](https://docs.zoocode.dev/features/skills) / [Roo Code](https://docs.roocode.com/features/skills) | `.roo/skills/` | `~/.roo/skills/` |
| [OpenCode](https://opencode.ai/docs/skills/) | `.opencode/skills/` | `~/.config/opencode/skills/` |
| [Cursor](https://cursor.com/docs/skills) | `.cursor/skills/` | `~/.cursor/skills/` |
| [Gemini CLI](https://geminicli.com/docs/cli/skills/) | `.gemini/skills/` | `~/.gemini/skills/` |
| [Kilo Code](https://kilo.ai/docs/customize/skills) | `.kilo/skills/` | `~/.kilo/skills/` |

OpenCode, Cursor, Gemini CLI, Zoo/Roo Code, and Kilo Code also support
`.agents/skills/` and `~/.agents/skills/`. The linked docs cover alternate paths
and discovery settings. Project paths are relative to your repository; `~`
means your home directory. The commands here use Bash.

### Share one copy

For a tool with a separate directory, link the clone into its personal skills
directory. For Claude Code:

```bash
mkdir -p ~/.claude/skills
ln -s "$HOME/.agents/skills/anti-ai-slop-skill" ~/.claude/skills/
```

Use an unused destination. If links are unavailable, copy the complete folder
and refresh the copy when updating. To update the shared clone:

```bash
git -C ~/.agents/skills/anti-ai-slop-skill pull --ff-only
```

## Use

Ask for a writing task or name the skill:

```text
Use anti-ai-slop-skill to rewrite this draft. Keep the facts and match my tone:
[paste draft]
```

Provide a voice sample when tone matters. The skill follows requested formats,
keeps necessary technical terms, and uses headings or lists when useful. It
avoids invented specifics and labels hypothetical examples. Rule explanations
and scores stay out of the result unless requested.

To check discovery, ask the agent to list its available skills, then ask it to
use `anti-ai-slop-skill` on a draft. If it is missing, check the directory name
and frontmatter, then reload skills or restart the tool. See the linked tool
docs for discovery commands.

## How it works

[SKILL.md](SKILL.md) contains the workflow and final review. Hosts that support
progressive loading read metadata for discovery and load instructions when the
skill activates; context cost depends on the host and tokenizer.

| Reference | Loaded when |
| --- | --- |
| [Banned lists](references/banned-lists.md) | Before drafting or reviewing prose |
| [Structures](references/structures.md) | The draft exceeds two sentences |
| [Examples](references/examples.md) | A rule is unclear or a revision still sounds synthetic |

The final check rates directness, rhythm, trust, authenticity, and density from
1–10 each, with revision below 35/50. Factual errors and missed requirements
must be fixed regardless of score. This is an editing heuristic, not a test of
human authorship.

## Without skill support

Include the body of `SKILL.md` and the needed reference contents in your prompt
or the tool's rules file. Relative links alone do not give a chat access to local
files. Always-on rules use context even for unrelated tasks; native skills allow
the host to load instructions on demand.

## Credits

Adapted from [jalaalrd/anti-ai-slop](https://github.com/jalaalrd/anti-ai-slop)
and [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop).
Upstream projects retain their own licenses. See [LICENSE.md](LICENSE.md) for
this repository's license.
