# Google Stitch skill

Claude Code skill + MCP config for [Google Stitch](https://stitch.withgoogle.com/).

- `skills/stitch/SKILL.md` – the skill
- `.mcp.json` – Stitch MCP server (OAuth2: reads `STITCH_ACCESS_TOKEN` and `STITCH_PROJECT_ID` from the environment; API keys are rejected)

Install the skill: copy `skills/stitch` to `~/.claude/skills/stitch`.
Based on the MCP endpoint used by https://github.com/gemini-cli-extensions/stitch.
