# Skills

A collection of agent skills for Claude Code and other `SKILL.md`-compatible agents.

## Available skills

| Skill | Purpose |
|-------|---------|
| [thesis-crosscheck](skills/thesis-crosscheck/SKILL.md) | Audit a thesis document, defense deck, and software repository for consistency; run an adaptive mock defense interview; produce an evidence-based report, recommendations, and remediation retests. |

## Installation

Install with the [`skills`](https://github.com/vercel-labs/skills) CLI. It needs Node.js, and `npx` fetches the CLI on demand.

```bash
npx skills add theheavenlyhacker/skills
```

Install only this skill:

```bash
npx skills add theheavenlyhacker/skills --skill thesis-crosscheck
```

Install globally (all projects) for Claude Code:

```bash
npx skills add theheavenlyhacker/skills --skill thesis-crosscheck -g -a claude-code
```

Restart your agent session so the skill is picked up. To list or remove it later, use `npx skills list` and `npx skills remove thesis-crosscheck`.

## Usage: thesis-crosscheck

Give the agent three artifacts and ask it to run the skill:

1. The thesis document (PDF, DOCX, or Markdown)
2. The defense presentation (PPTX or PDF)
3. The software repository (local path)

Example prompt:

```text
Use thesis-crosscheck. Thesis: ./thesis.pdf, deck: ./defense.pptx, repo: ./code
```

The skill then works through these phases:

1. Intake and artifact check
2. Build a thesis knowledge base and claims registry
3. Review the presentation deck
4. Audit the repository
5. Cross-check thesis, deck, and code
6. Prepare questions and run a one-question-at-a-time mock defense
7. Score the answers and project consistency
8. Generate a report, recommendations, and a prioritized action plan
9. Optionally run remediation drills and retests, tracking progress

Notes:

- Your source files are never modified unless you ask.
- Reports and the knowledge base are saved only when the agent can write files.
- Scores reflect the mock interview and the evidence reviewed. They don't predict the outcome of an official defense.

## Connecting Google Docs and Canva (MCP)

The thesis and deck can also be Google Docs or Canva links. Connect the matching MCP servers so the agent can read them:

```bash
claude mcp add --transport http canva https://mcp.canva.com/mcp
```

For Google Docs, connect the Google Drive connector in Claude (Settings → Connectors), or add any Google Docs/Drive MCP server to your agent. Authenticate when prompted, then use links in the prompt:

```text
Use thesis-crosscheck. Thesis: https://docs.google.com/document/d/..., deck: https://www.canva.com/design/..., repo: ./code
```

Without a connector, the skill records the limitation and asks you to export the file instead. Access is read-only.

## Adding a skill

Create `skills/<name>/SKILL.md` with `name` and `description` frontmatter, then add a row to the table above.

## License

No license specified.
