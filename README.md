# Argument.ai — Argument Mapping Studio

A WebMCP-powered app where you and an AI agent debate together on a shared visual canvas.

**Hackathon:** OpenAI WebMCP Challenge — deadline September 3, 2026

## What it is

A single-page web app where a human and an AI agent collaboratively map arguments on a
visual canvas. The agent reads and manipulates the argument graph via WebMCP tools. The
human sees the same live canvas. Neither can "win" without the other — that's the point.

Most WebMCP apps let the agent *do tasks for* the human. Argument.ai is different: the
agent is an **intellectual sparring partner**, not an assistant.

## How to use

1. Open this page (`index.html`) in an agent-enabled browser — e.g. ChatGPT's built-in
   browser (desktop app, GPT-5.6 Sol/Terra), or Chrome with
   `chrome://flags/#enable-webmcp-testing` turned on.
2. Tell the agent: "Set the topic to [your topic] and argue the [pro/con] side."
3. Watch the agent place its opening argument on the canvas.
4. Add your own claims using the toolbar (`+ Claim`, `+ Support`, `+ Objection`).
5. The agent will object, rate, and flag logical fallacies in real time.

No backend, no build step, no npm. The whole app is `index.html`; state persists in
`localStorage` between visits.

## WebMCP tools exposed

| Tool | Type | What it does |
|---|---|---|
| `get_map_state` | read | Returns the full argument graph |
| `get_node` | read | Returns one node plus its connections |
| `get_weak_points` | read | Finds low-strength or fallacious nodes |
| `add_claim` | write | Adds a new claim to the map |
| `add_support` | write | Adds supporting evidence for a node |
| `add_objection` | write | Challenges a node with a counter-argument |
| `add_rebuttal` | write | Responds to an objection |
| `rate_node` | write | Updates a node's strength rating |
| `highlight_node` | write | Draws attention to a node |
| `flag_fallacy` | write | Marks a logical fallacy |
| `set_topic` | write | Sets the debate topic and sides |
| `clear_map` | write | Resets the canvas |

## Why WebMCP makes this better

Without WebMCP: the agent describes arguments in text, you manually draw them.
With WebMCP: the agent calls `add_objection(...)` and the node appears instantly — both
of you looking at the same living argument map. The canvas *is* the conversation.

## Testing without ChatGPT

- Enable in Chrome: `chrome://flags/#enable-webmcp-testing`
- Or use `webmcp-test.html` in this folder, a standalone tool tester that lets you call
  each WebMCP tool directly without the full UI or an agent host.

## Deployment

Any static host works:

```bash
# Vercel
npx vercel --yes

# Netlify
npx netlify deploy --dir . --prod

# GitHub Pages
git init && git add . && git commit -m "Argument.ai"
gh repo create argument-ai --public --push --source=.
# then enable Pages in repo settings → Deploy from main → /(root)
```

A public HTTPS URL is required for WebMCP tool testing in ChatGPT.

## Built for the OpenAI WebMCP Challenge, August 2026
