# PVC Practitioner — Claude Code Context

## What This Project Is
A client-side AI-powered data workflow tool deployed to pvc.wsdalearning.ai.
Static site, no build step. All HTML, CSS, and JS in one file.

## Deployment
- Host: Cloudflare Pages (auto-deploys from this repo on push to main)
- No build step — push to main and it's live
- _redirects handles SPA routing: all URLs resolve to index.html
- AI calls proxy through: pvc-proxy.walterashields.workers.dev (keeps Anthropic API key off the client)

## Tech Stack
- sql.js (SQLite-as-WASM) — runs database queries entirely in the browser
- Claude claude-sonnet-4-20250514 via Cloudflare Worker proxy
- Vanilla HTML/CSS/JS — no framework, no bundler
- Stripe checkout via buy.stripe.com link — $49/month paywall
- Klaviyo email gate in pvc-app.html (SESSION_KEY + expiry in localStorage)

## Core PVC Workflow
Three sequential steps inside the tool screen:
- Prompt (P): User types business question → Claude generates SQL
- Validate (V): SQL runs in-browser via db.exec(), Claude reviews data quality
- Communicate (C): Claude produces stakeholder output in 4 formats:
  Executive summary, Slack message, Email, Slide bullets

## Paywall
- Triggered after 3 free sessions (localStorage key: pvc_sessions_used)
- Counter increments after completing the Communicate step
- Paywall price: $49/month via Stripe checkout link
- No automated subscription verification in current version

## File Status
- index.html — the LIVE app (142KB) — this is what's deployed
- pvc-app.html — next version in development (516KB) — has email gate + updated styling
- Do not overwrite index.html with pvc-app.html without explicit instruction

## Brand
- Colors: navy #0f1923, green #06c015
- Fonts: DM Sans, DM Mono
- Domain: wsdalearning.ai

## What NOT to Do
- Do not hardcode the Anthropic API key — it lives in the Cloudflare Worker proxy
- Do not introduce a build system or framework
- Do not promote pvc-app.html to index.html without explicit instruction
- Do not change the Stripe checkout link without confirming the correct URL