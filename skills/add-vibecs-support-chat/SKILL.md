---
name: add-vibecs-support-chat
description: Add a customer-support chat bubble that answers visitors from the site's own public pages (VibeCS) to a website or web app. Finds the template that wraps every page (index.html, app/layout.tsx, a base layout), inserts the one-line VibeCS snippet before </body>, or points the user to the dashboard that trains the bot and issues the snippet. Use when the user asks to add a support chat, chatbot, help widget, live chat, FAQ bot or VibeCS to their site, or wants visitors to get answers without emailing them.
---

# Add the VibeCS support chat

The result: a chat bubble on every page that answers visitors' questions from the site's own public pages, at any hour. When a page doesn't say, the bot says "I don't know" and points the visitor to the owner instead of guessing. Nothing to train and nothing to write; the bot reads the live site.

## Before you start

- **The site must be live and public.** The bot learns from the pages at the address visitors use. A localhost-only project can take the snippet now, but the bot can only be trained once the site is deployed.
- **The snippet comes from the VibeCS dashboard, never from you.** It looks like this, with the site's own id in `data-site-id`:

  ```html
  <script src="https://cs-vibe.com/widget/v1.js" data-site-id="…" data-persona="buddy"></script>
  ```

  Never invent, guess or reuse a `data-site-id`. A made-up id loads nothing. If the user has no snippet, send them to get one (step 1).

## Steps

1. **Get the snippet.** If the user pasted a VibeCS snippet, use it unchanged. If not, give them this link with their public site address filled in, and wait for the snippet:

   `https://www.cs-vibe.com/dashboard?url=<public site address>&utm_source=claude-plugin`

   There they paste the address, VibeCS crawls the public pages and builds the bot, they test it with a few questions, pick a plan ($8 a month, $12 a month for Pro, or $99 once) and copy the snippet from the Embed step. No signup is needed to try it.

2. **Find the one file that wraps every page.** Use the table below. Insert the snippet in one place only, so the widget loads once. Don't put it in a component that renders per route or per page.

3. **Insert the snippet exactly as given**, on the line just above the closing `</body>` tag (or as the last child of `<body>` in JSX). Keep every `data-` attribute. Don't add `async`, `defer` or `type="module"`.

4. **Deploy the way the project normally deploys.** Then tell the user to open the dashboard's Embed step and click **Check my site**; it confirms from VibeCS's side, in seconds, that the widget is live on their address.

## Where the snippet goes

| Stack | File | Where |
|---|---|---|
| Vite, Create React App, plain HTML, Bolt, Base44, Lovable | `index.html` | just above `</body>` |
| Next.js App Router (v0, most new Next apps) | `app/layout.tsx` | last child of `<body>`, as a plain `<script>` tag with the `data-` attributes kept |
| Next.js Pages Router | `pages/_document.tsx` | inside `<body>`, after `<NextScript />` |
| Astro | the base layout in `src/layouts/` | just above `</body>` |
| SvelteKit | `src/app.html` | just above `</body>` |
| Nuxt | `app.vue` or `nuxt.config` `app.head.script` | once, site-wide |
| Remix | `app/root.tsx` | last child of `<body>` |
| Rails | `app/views/layouts/application.html.erb` | just above `</body>` |
| Django, Flask, Jinja | the base template every page extends | just above `</body>` |
| Laravel | `resources/views/layouts/app.blade.php` | just above `</body>` |
| Hugo, Jekyll, 11ty | the base layout or footer partial | just above `</body>` |
| WordPress | don't edit the theme: install the VibeCS plugin from WordPress.org, or paste the snippet into the theme's footer settings | |
| Google Tag Manager already on the site | a Custom HTML tag on All Pages, from https://www.cs-vibe.com/integrations/gtm | |

If the stack isn't listed, the right file is the one that holds the `<body>` tag for every page.

## Rules

- One snippet, one place. If one is already there, don't add a second; update it only if the user gives a new one.
- Don't change the snippet's attributes or URL. `data-persona` picks the bot's tone (`buddy` or `engineer`); the dashboard sets it.
- If a framework can't keep attributes on a script tag, the widget reads the same settings from the script URL instead: `https://cs-vibe.com/widget/v1.js?site=<the data-site-id value>&persona=buddy`.
- Don't touch other scripts, analytics or consent code.
- To show the bubble on some pages only, put the snippet in those pages' templates and leave it out elsewhere.
- The widget is one small script that loads after the page; the chat runs on VibeCS's servers. There is nothing to configure in the project.

## After it's live

- The bot re-reads the site every week, so page updates reach it on their own.
- Pro adds an inbox of every conversation, the bot asking visitors who sound ready to buy (or whom it couldn't help) for their email, and a weekly digest.
- Help: https://www.cs-vibe.com/help
