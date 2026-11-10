# How to connect Udemy to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Udemy account.** Udemy's official ChatGPT app helps you discover public courses, and the official Udemy Business connector for Claude needs an Enterprise subscription with the AI Connectors add-on. Cotlet.dev connects your own signed-in Udemy instructor account to any AI agent, so the AI creates coupons and updates your courses for you.

## What you can ask

> Create a coupon BLACKFRIDAY26 for my Python Bootcamp course at $12.99, starting November 27 and running for 5 days.

> Make a free coupon for 100 students on my Excel for Beginners course and send me the link.

> Change the title of my React course to "React 19 Complete Guide" and rewrite the subtitle to match.

> Add a lecture called "Deploying to Vercel" at the end of section 8 in my Next.js course and upload this video.

> Which of my coupons end this week? Create new ones at the same price for my top 3 courses.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Udemy tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"udemy":{"command":"uvx","args":["udemy-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t udemy-mcp .
docker run -i --rm -e COTLET_API_KEY udemy-mcp
```

Tools: `udemy_guide`, `udemy_status`, `udemy_open`, `udemy_read`, `udemy_click`, `udemy_type`, `udemy_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install udemy-mcp        # or run it once: uvx udemy-mcp connect
udemy-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 udemy_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 udemy_agent.py status    # is Udemy ready in your Cotlet.dev account
python3 udemy_agent.py guide     # Udemy screens and sign-in link
python3 udemy_agent.py read      # open Udemy, read the page, close the browser
python3 udemy_agent.py tools     # list Cotlet.dev tools
python3 udemy_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Udemy users

**Does Udemy have an API?**

Udemy has an Instructor API that lists your courses, reads reviews, and reads and answers Q&A questions and direct messages (checked 12 Oct 2026). It has no coupons, announcements, review responses, course edits or revenue. Cotlet.dev works in your own signed-in Udemy account, so your AI agent can create coupons and update courses with no API key and no code.

**How do I connect Udemy to ChatGPT?**

Udemy's official ChatGPT app helps you discover public courses. To manage your own courses, add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Udemy once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Udemy API key.

**Is there a way to use Claude with Udemy?**

Yes. Claude lists an official Udemy Business connector, which needs an Enterprise subscription plus the AI Connectors add-on. To work in your own Udemy account, run the one-line `claude mcp add` command above in Claude Code, or add `https://cotlet.dev/mcp/v1` as a custom connector in the Claude app.

**Is there a Udemy MCP server?**

Udemy offers an official Udemy Business connector for Claude, focused on learning. Cotlet.dev is a hosted MCP server that works in your own Udemy account for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Udemy on Cotlet.dev](https://cotlet.dev/integrations/udemy-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=udemy&utm_content=find)
- [PyPI package udemy-mcp](https://pypi.org/project/udemy-mcp/)
- [Odel](https://odel.app/modules/cotlet/udemy)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-udemy-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/udemy-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=udemy

Start free: https://cotlet.dev/signup?app=udemy&utm_source=github&utm_medium=readme&utm_campaign=udemy
