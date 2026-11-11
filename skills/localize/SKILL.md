---
name: localize
description: Translate an app's UI with localize.dev's hosted MCP server. Use when adding or changing text people see in a React, Next.js, React Native, Vue, Svelte, Astro, Angular, Flutter, iOS, Android, Rails, Django or Laravel app; when asked to internationalize an app, add a language, or fix missing translations; or before finishing work that touched UI copy in an app that has a localize.config.json.
---

# Translating UI text with localize.dev

The `localize` MCP server runs at https://uselocalize.dev/api/mcp. It finds text that's hardcoded
in UI code, gives it translation keys, rewrites the code to the app's i18n library, translates the
new messages with the app's context and writes the locale files.

The server can't see the project. Every tool takes the files it needs in `files` (each a `path`
relative to the project root and the file's whole `content`) and answers with the files to create
or overwrite. Write those back exactly as returned.

## What to send

- The UI files to work on.
- `package.json`, and `localize.config.json` when there is one.
- The existing locale files, for example `locales/en.json` and `locales/es.json`.

Leave out `node_modules`, build output and binary files.

In a monorepo, either send paths relative to the repository root (`apps/web/src/App.tsx`) and pass
`app: "apps/web"`, or send paths relative to the app's folder (`src/App.tsx`) and leave `app` out.

Large locale files can be left out of `check`; it then reports hardcoded text only, not missing or
outdated translations. Always send the locale files to `localize`,
`translate` and `add_language`: a locale file they return is written whole, so one that wasn't sent
comes back with only the new messages.

## Tools

- `check`: lists hardcoded copy, missing and outdated translations, each with its file and line.
  It costs nothing.
- `config`: the languages, locale files and i18n library the app uses. Read it before writing new
  copy so it follows the app's conventions.
- `localize`: extracts and translates. Pass `paths` with the files you changed so a run stays quick.
- `translate`: fills in missing translations in existing locale files, for any stack.
- `add_language`: adds a language (BCP 47 code such as `ja` or `pt-BR`) and translates every
  message into it.

## Workflow

1. After adding or changing UI text, call `localize` with those files and the files listed above,
   then write back every file it returns.
2. Leave new messages out of the other languages' locale files; `localize` fills them in. Fixing a
   translation that's wrong is fine.
3. Before finishing, call `check` with the same files. It should pass.

## Signing in

The first call asks the user to sign in to localize.dev in the browser and choose a workspace
(free tier included). Don't ask the user to paste an API key into the chat.
