---
name: stitch
description: Use Google Stitch (AI UI/UX design and code generation) via its MCP server. Use when the user wants to list Stitch projects or screens, generate a UI screen from a text prompt, download a screen's HTML or image, or enhance a rough design idea into an effective Stitch prompt.
---

# Google Stitch

Stitch turns text (or images) into UI designs and front-end code. This skill drives it through the `stitch` MCP server (`https://stitch.googleapis.com/mcp`, configured in `.mcp.json`).

## Setup
1. Create an API key at https://stitch.withgoogle.com/ → profile → Stitch Settings → API Keys.
2. Export it as `STITCH_API_KEY` before starting Claude Code. Never paste it into chat or commit it.
3. If `stitch` tools are missing, tell the user the MCP server isn't connected or the key is unset.

## Domain model
A user has **projects**; a project has many **screens**. A screen has an **image** and a full HTML document (Tailwind via CDN). "Design" means one screen or a whole project.

## Workflows
- **Explore**: list projects → get project details → list screens. Always identify the project before acting on screens.
- **Generate**: write a strong prompt (below), call the generate-screen-from-text tool on the chosen project (default model is Gemini 3 Flash; Gemini 3 Pro is available for higher quality), then show the result.
- **Retrieve**: fetch a screen's HTML code or image and save it where the user asks (e.g. `designs/<screen_name>.html`).
- **Enhance a prompt**: rewrite the user's rough idea into a structured prompt and save it as `snake_case_topic.md`. Do not call generation unless asked.

## Writing effective Stitch prompts
Include: the product and audience; page/screen purpose; layout and key sections in order; visual style (colors, typography, tone, light/dark); components and states; target device (mobile/desktop). Be specific and concrete; iterate with small follow-up edits rather than rewriting everything.

## Notes
- Generation can be slow (timeouts up to ~5 min); wait rather than retry.
- Confirm before generating many screens or overwriting existing files.
