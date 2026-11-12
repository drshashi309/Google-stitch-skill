---
name: stitch
description: Use Google Stitch (AI UI/UX design and code generation) via its MCP server. Use when the user wants to list Stitch projects or screens, generate a UI screen from a text prompt, download a screen's HTML or image, or enhance a rough design idea into an effective Stitch prompt.
---

# Google Stitch

Stitch turns text (or images) into UI designs and front-end code. This skill drives it through the `stitch` MCP server (`https://stitch.googleapis.com/mcp`, configured in `.mcp.json`).

## Setup
1. The Stitch MCP endpoint rejects API keys; it needs an OAuth2 access token. Use a Google Cloud project with the Stitch API enabled (`gcloud services enable stitch.googleapis.com`).
2. Export `STITCH_PROJECT_ID=<gcp-project-id>` and `STITCH_ACCESS_TOKEN=$(gcloud auth print-access-token)` before starting Claude Code. Tokens expire after about an hour; refresh and restart. Never paste them into chat or commit them.
3. If `stitch` tools are missing, tell the user the MCP server isn't connected or the token/project env vars are unset or expired.

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
