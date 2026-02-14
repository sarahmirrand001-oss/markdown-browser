# Markdown Browser Skill (OpenClaw)

A professional post-processing wrapper for `web_fetch` results. This tool is designed for AI Agents to handle web content efficiently, respecting site policies and protecting user privacy.

## Features

- **Policy Awareness**: Parses `Content-Signal` headers to determine if the content is allowed for AI training or input.
- **Privacy First**: Automatically redacts sensitive parameters (keys, tokens, passwords) and paths from URLs in the output.
- **Markdown Optimization**: Leveraging Cloudflare's "Markdown for Agents", it prioritizes native Markdown responses to save up to 80% of tokens.
- **Graceful Fallback**: Automatically converts HTML to Markdown using `Turndown` if native Markdown is not available.
- **Token Estimation**: Captures `x-markdown-tokens` for accurate context window management.

## Installation

```bash
git clone https://github.com/sarahmirrand001-oss/markdown-browser.git
cd markdown-browser
npm install
```

## Usage

### As a Standalone CLI Tool

You can pipe a JSON result from any web fetcher (like OpenClaw's `web_fetch`) into this script:

```bash
# Using a saved JSON file
node browser.js --input fetch_result.json --content-signal "ai-input=yes"

# Using stdin
cat fetch_result.json | node browser.js
```

### As an OpenClaw Skill

Add this folder to your OpenClaw `skills` directory. The agent will automatically recognize the `SKILL.md` and use the `process_web_fetch_result` tool.

## Technical Details

- **Input Contract**: Expects a JSON object with `url`, `finalUrl`, `contentType`, and `text`.
- **Output Schema**: Returns a clean JSON object with `content`, `format`, `token_estimate`, and `policy_action`.

## License

MIT
