# System Explanation

An opt-in agent skill that helps people explain the systems they build: what the parts do, how they communicate, where state lives, and what happens when something fails.

The assistant inspects the source. The learner practices explaining it in their own words. You do not need to read or debug code independently to use the skill.

## What you get

When enabled, requested summaries include a focused **System explanation**: components, a concrete request trace, state, failure detection and recovery, trade-offs, a speakable summary and one practice question. Small changes get a small explanation. Deeper walkthroughs are available on request.

Claims are grounded in the inspected material. Implemented, historical, proposed and unknown behavior remain distinct; an architecture diagram or passing static check is not proof of production health.

See [illustrative examples](EXAMPLES.md) and the full [skill instructions](SKILL.md).

## On and off

**Default: OFF in a fresh conversation.** Asking for an ordinary summary does not activate coaching.

- **ON:** explicitly invoke the skill using your tool's syntax, or say “System explanation on” in a host that supports loading skills by name.
- **OFF:** say “System explanation off” or “normal summaries.” An explicit invocation with `off` also turns it off.
- The latest explicit toggle applies only to the current conversation. If both appear in one message, OFF wins. No ON state is written to disk.

These are conversation instructions, not a guaranteed runtime switch. Turning OFF does not erase already loaded context or disable a plugin. A host's native skill-disable control is separate. Direct architecture questions can still be answered while OFF.

## Install locally

Clone the repository:

```sh
git clone https://github.com/404kidwiz/system-explanation.git
cd system-explanation
```

Review the files, then copy **only `SKILL.md` and `agents/`** into your tool's personal skill directory below. Keep the folder name `system-explanation`. The package contains no hooks or install scripts.

Example for Claude Code, run from the downloaded repository:

```sh
mkdir -p "$HOME/.claude/skills/system-explanation/agents"
cp SKILL.md "$HOME/.claude/skills/system-explanation/SKILL.md"
cp agents/openai.yaml "$HOME/.claude/skills/system-explanation/agents/openai.yaml"
```

If that skill folder already exists, compare its contents before overwriting it. For another host, substitute its documented directory. Restart the conversation or use the host's supported skill refresh. Local installation does not make files available to remote/cloud sessions automatically.

## Host support

The directories and invocation mechanisms below were checked against official documentation or installed loaders. This is **configuration compatibility**, not a claim of model-behavior testing across every product/version.

| Host | Personal skill directory | Activation | Automatic invocation control |
| --- | --- | --- | --- |
| Claude Code | `~/.claude/skills/system-explanation/` | `/system-explanation` | `disable-model-invocation: true` |
| Cursor Agent chat | `~/.cursor/skills/system-explanation/` | `/system-explanation` | Same frontmatter field |
| Codex | `~/.agents/skills/system-explanation/` | `$system-explanation` | `agents/openai.yaml` sets `allow_implicit_invocation: false` |
| OpenCode | `~/.config/opencode/skills/system-explanation/` | Ask to load the skill by name | Explicit-request guard in description/body |
| Hermes | `~/.hermes/skills/system-explanation/` for the default profile | Ask to load the skill by name | Explicit-request guard in description/body |
| Gemini CLI | `~/.gemini/skills/system-explanation/` | Ask to activate the skill; approve the normal activation prompt if shown | Explicit-request guard; native skill enable/disable is separate |
| Antigravity IDE | `~/.gemini/config/skills/system-explanation/` | `/system-explanation` where offered, otherwise ask by name | Explicit-request guard |
| Antigravity CLI | `~/.gemini/antigravity-cli/skills/system-explanation/` | `/system-explanation` | Explicit-request guard |
| Crush | `~/.config/crush/skills/system-explanation/` | Command palette → `user:system-explanation` on versions supporting user-invocable skills | `disable-model-invocation: true` on supporting versions |
| Grok CLI | `~/.grok/skills/system-explanation/` | `/system-explanation` | `disable-model-invocation: true` |
| Kilo | `~/.agents/skills/system-explanation/` | `/system-explanation` where listed, otherwise ask by name | Explicit-request guard |
| Kimi CLI | `~/.kimi/skills/system-explanation/` | Ask to load the skill by name | Explicit-request guard |

Other tools that support the Agent Skills format may work, but are not verified here. Unknown metadata fields may be ignored. Where the host has no verified explicit-only switch, OFF/ON behavior depends on following the instructions; it is not mechanically enforced.

If named discovery is unavailable, explicitly ask the assistant to read your installed `system-explanation/SKILL.md` file and turn coaching on for this conversation. This fallback requires ordinary file access. There is no universal slash command.

## Verify your installation

1. Confirm the skill appears in your host's skill list or can be read from the installed path.
2. In a fresh conversation, ask for a normal summary: this skill should not add its coaching supplement.
3. Invoke the skill, then request a summary of a small feature with available source.
4. Say “System explanation off”, then request another summary. The standing supplement should stop.

[Behavior scenarios](CHECKS.md) describe expected results. They are a manual evaluation plan, not reported passing model tests. Local checks cover package structure, metadata, privacy and instruction consistency only.

## References

Host configuration references: [Claude Code](https://code.claude.com/docs/en/skills), [Cursor](https://cursor.com/docs/skills), [Codex](https://learn.chatgpt.com/docs/build-skills), [OpenCode](https://opencode.ai/docs/skills/), [Gemini CLI](https://geminicli.com/docs/cli/skills/), [Antigravity](https://antigravity.google/docs/skills), [Crush](https://github.com/charmbracelet/crush), [Kilo](https://kilo.ai/docs/customize/skills), [Kimi CLI](https://moonshotai.github.io/kimi-cli/en/customization/agents.html). Hermes and Grok paths were also checked in installed source/documentation. Behavior may vary by version and profile.

## License

[MIT](LICENSE). You may use, adapt and share this skill under the license terms.
