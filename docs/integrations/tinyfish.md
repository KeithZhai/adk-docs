---
catalog_title: TinyFish
catalog_description: Search the web, fetch page content, and automate websites
catalog_icon: /integrations/assets/tinyfish.svg
catalog_tags: ["search"]
---

# TinyFish plugin for ADK

<div class="language-support-tag">
  <span class="lst-supported">Supported in ADK</span><span class="lst-python">Python</span>
</div>

The [TinyFish ADK package](https://github.com/tinyfish-io/tinyfish-web-agent-integrations/tree/main/google-adk)
connects your ADK agent to [TinyFish](https://tinyfish.ai), which provides web
Search, Fetch, Browser, and Agent APIs for AI agents. This integration gives
your agent the ability to search the web, fetch clean content from URLs, run
browser automations using natural language, and create remote browser sessions.

## Use cases

- **Web Search**: Search the web and get structured results back for your
  agent to reason over.

- **Content Fetching**: Fetch clean content from one or more URLs as markdown,
  HTML, or JSON.

- **Web Automation**: Navigate websites, fill in forms, and extract data by
  describing the goal in natural language. Run automations synchronously, or
  queue long-running ones and poll for results.

- **Remote Browser Sessions**: Create a remote browser session and get
  connection URLs for direct browser control.

## Prerequisites

- A [TinyFish](https://tinyfish.ai) account
- A TinyFish API key, available at
  [agent.tinyfish.ai/api-keys](https://agent.tinyfish.ai/api-keys). Search and
  Fetch are free.

## Installation

```bash
pip install tinyfish-adk
```

Set your TinyFish API key as an environment variable:

```bash
export TINYFISH_API_KEY="your-api-key"
```

## Use with agent

```python
from google.adk.agents import Agent
from tinyfish_adk import (
    tinyfish_fetch,
    tinyfish_search,
    tinyfish_web_agent,
)

root_agent = Agent(
    model="gemini-flash-latest",
    name="web_researcher",
    instruction="Use the TinyFish tools to search the web, fetch page content, and extract data from websites.",
    tools=[tinyfish_search, tinyfish_fetch, tinyfish_web_agent],
)
```

## Available tools

Tool | Description
---- | -----------
`tinyfish_search` | Search the web and return structured results
`tinyfish_fetch` | Fetch clean content from one or more URLs
`tinyfish_web_agent` | Run a browser automation synchronously
`tinyfish_queue_run` | Start an automation asynchronously and return a `run_id`
`tinyfish_get_run` | Check the status and get the results of a run by `run_id`
`tinyfish_list_runs` | List recent automation runs, optionally filtered by status
`tinyfish_create_browser_session` | Create a remote browser session and return connection URLs

## Configuration

All tools read `TINYFISH_API_KEY` from the environment. The web automation
tools (`tinyfish_web_agent` and `tinyfish_queue_run`) also accept the following
optional parameters:

Parameter | Description
--------- | -----------
`browser_profile` | `"lite"` (default, fast) or `"stealth"` (anti-detection)
`proxy_country` | Route through a proxy: `US`, `GB`, `CA`, `DE`, `FR`, `JP`, `AU`

## Additional resources

- [TinyFish Documentation](https://docs.tinyfish.ai)
- [TinyFish ADK on PyPI](https://pypi.org/project/tinyfish-adk/)
- [TinyFish ADK on GitHub](https://github.com/tinyfish-io/tinyfish-web-agent-integrations/tree/main/google-adk)
