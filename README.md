# localize.dev (hosted)

localize.dev finds hardcoded UI text, gives it translation keys, translates it with your app's
context and writes the locale files. This plugin connects Claude Code and Cursor to localize.dev's
hosted MCP server at `https://uselocalize.dev/api/mcp`, so nothing runs on your computer.

## Install

Claude Code:

```
/plugin marketplace add ufortstephen/localize-dev-hosted
/plugin install localize-dev@uselocalize-hosted
```

The first tool call opens localize.dev in your browser to sign in and pick a workspace. There's a free
tier, and `check` never counts toward your plan.

## How it works

The server can't read your disk. The agent sends the files a call needs (the UI files,
`package.json`, `localize.config.json` and the locale files) and writes back the files the server
returns. The files are kept in a temporary folder for that one call and deleted when it answers.

## The local server

To run the MCP server on your own machine instead, so it reads and writes the project directly,
use the main plugin: https://github.com/ufortstephen/localize-dev

Setup for every agent: https://uselocalize.dev/mcp

## License

MIT
