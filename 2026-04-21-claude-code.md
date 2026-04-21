# Claude Code Deep Dive

- Repo: <https://github.com/lydiahallie/demo-issue-tracker>

> **Author's note:** I didn't attend in person &mdash; I had the live stream on in the background.

CLI, desktop app, website &mdash; it's really just an agent.

Sonnet general purpose rec.

Model is still stateless, that hasn't changed.

Q: impact of changing models mid convo?  
A: it will break cache.

- Tools (read, write, edit, bash, fetch, mcp)
- Sys Prompt
- Messages

The harness (above, essentially; "Claude Code") provides the state.

Being an "agent" means having a loop with tools, ends w/ text or no output.

`/init` generates `CLAUDE.md`.

`/permissions` for ... wait for it ... permissions. 🙂

`/fewer-permission-prompts` is new, useful if you've already ran a few sessions.

In order:

- Managed settings e.g. enterprise/org/corporate
- CLI
- User
- Project (local, then shared)
- User

Model vs effort. Worth changing effort vs model (can reduce cost as well).

`.claude/skills/SKILL.md` has YAML frontmatter and then just Markdown. Can use `$ARGUMENTS` syntax.

Q: Skill vs script: what's the line?  
A: Skill easier because don't need to write code. If already have script, can use it. Skill could use a script e.g. deploy.sh.

Plugins are wrapping skills, agents, hooks, MCP servers into something to be shared. They go in `.claude-plugin` and have a `plugin.json`. `plugin-exercise` branch in the repo has the `EXERCISE.md`.

MCP == Model Context Protocol. Recommended package: <https://www.npmjs.com/package/@modelcontextprotocol/sdk>

- Create server
- It specifically uses [JSON-RPC 2.0](https://www.jsonrpc.org/specification)
- Transport layer is either stdio (for local dev) or HTTP/SEE for remote servers

So the basic steps, for source code:

1. Init a server
2. Register a tool definition
3. Handle tool logic (this is the actual business logic)
4. Connect the transport layer

Pro tips, cool things, TILs, re: Claude features and such:

- Claude Design -> send to Claude Code
- Desktop app can preview local web stuff
- Routines are like LLM-ified crons 🙂
- `/btw` to interject while it's doin' things

Q&A:

Q: How to save tokens? Compaction vs clearing?  
A: Compaction is a summary, either automated or w/ manual hint message. Clearing just truncates.
A: Clear when switching to new task in same window. Compact retains summarized versions.

Q: Memory files? What is "auto memory"?  
A: When said something multiple times, gets added to `MEMORY.md`.

Q: Better workflow than asking for screenshots for feedback?  
A: Depends on what you need for feedback, (browser) extension could work OK.

Q: `MEMORY.md` grows over time, how to manage that?  
A: Manual review. Lydia personally runs with auto-memory turned off.

Q: Mixing models in same prompt can cause caching issue. Skills can mix models, how does that work together?  
A: Would break cache if no `context: fork` in frontmatter.
