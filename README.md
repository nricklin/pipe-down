# pipe-down

A verbosity sledgehammer for coding agents. Three skills, three lengths:

| Command | You get |
| --- | --- |
| `/0` | Nothing. It does the work and says nothing. |
| `/1` | Exactly one sentence. |
| `/3` | At most three sentences. |

Put the command at the start of your message:

```
/1 why is this test flaky
/3 what's the diff between these two configs
/0 rename every usage of `fooBar` to `foo_bar`
```

Each applies only to that one response.


## Install

### Claude Code

```bash
claude plugin marketplace add nricklin/pipe-down
claude plugin install pipe-down@pipe-down
```

Verify with `claude plugin list`. Update with `claude plugin marketplace update pipe-down`.


### Cursor, Codex, OpenCode, Copilot, Amp, and any other agent-skills harness

```bash
npx skills add nricklin/pipe-down                  # this workspace
npx skills add nricklin/pipe-down -g               # all projects
npx skills add nricklin/pipe-down -a cursor -y     # one agent only
```

Start a new chat, then type `/0`, `/1`, or `/3`. `npx skills list` to verify,
`npx skills update pipe-down` to update, `npx skills remove pipe-down` to drop it.

### By hand

Copy the skill folders into whatever path your agent scans:

```bash
git clone https://github.com/nricklin/pipe-down
mkdir -p ~/.cursor/skills          # Cursor. Use your agent's own path.
cp -R pipe-down/skills/0 pipe-down/skills/1 pipe-down/skills/3 ~/.cursor/skills/
```

They're plain `SKILL.md` files with YAML frontmatter — no dependencies, nothing
to build. Start a new session afterward; skills are indexed at session start.


## License

MIT
