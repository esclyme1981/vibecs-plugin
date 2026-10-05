# VibeCS for Claude Code

Your site answers its own customers' questions, at any hour, from your own pages.

Install the plugin and ask Claude Code for a support chat. It puts the one-line VibeCS snippet in the file that wraps every page, and VibeCS answers visitors from your live pages: pricing, hours, how it works, what happens next. Nothing to train, nothing to write. When a page doesn't say, VibeCS says "I don't know" and points the visitor to you instead of guessing.

## Install

In Claude Code:

```
/plugin marketplace add esclyme1981/vibecs-plugin
/plugin install vibecs@vibecs
```

For Claude Code, Cursor, Codex and other agents, from your project folder:

```bash
cd /path/to/your-project && npx skills add esclyme1981/vibecs-plugin
```

## Use

1. Deploy your site. Open [the dashboard](https://www.cs-vibe.com/dashboard?utm_source=claude-plugin), paste the site's address and ask VibeCS a few questions. No signup to try it.
2. Pick a plan and copy the snippet from the Embed step. $8 a month, $12 a month for Pro, or $99 once.
3. In your project, say "Add the VibeCS support chat" and paste the snippet. The skill puts it in the right file: `index.html` on Vite, `app/layout.tsx` on Next.js, the base layout elsewhere.
4. Deploy. Click **Check my site** in the dashboard to confirm it's live.

VibeCS re-reads your site every week. Pro adds an inbox of every conversation, VibeCS asking visitors who sound ready to buy for their email, and a weekly digest.

Site: https://www.cs-vibe.com · Help: https://www.cs-vibe.com/help
