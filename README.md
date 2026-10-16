# Simple Lists

A tiny, **read-only** utility that answers two questions in one click: *what is actually
installed?* and *what is in my config folder?*

No blocks, no items, no gameplay changes — just six commands with a colorful, clickable chat
output and clean file exports. Handy for bug reports, server audits and modpack debugging.

## Commands

| Command | Generic form | Lists |
|---|---|---|
| `/modlist` | `/list mod` | every loaded mod |
| `/configlist` | `/list config` | all files in the `config` folder, recursively |
| `/pluginlist` | `/list plugin` | server-side mods (side `SERVER` or `BOTH`) |
| `/clientlist` | `/list client` | client-side mods (side `CLIENT` or `BOTH`) |
| `/serverlist` | `/list server` | server-side mods (side `SERVER` or `BOTH`) |
| `/list` | `/list help` | an in-game cheat sheet |

All commands require **permission level 2** (op / gamemaster).

## Arguments

Every command takes the same optional arguments, in this order:

```
/<command> [details] [format] [filename]
```

| Argument | Values | Default | Effect |
|---|---|---|---|
| `details` | `basic` · `version` · `full` | `basic` | how much is shown per entry |
| `format` | `chat` · `txt` · `json` | `chat` | print to chat, or write a file |
| `filename` | any name | `<command>_<details>` | output file for `txt` / `json` |

For **mods**, `version` adds the mod version; `full` adds the side, jar file name, license and
description.

For **configs**, `version` adds the file size; `full` adds the last-modified timestamp.

Every part is optional, so all of these are valid:

```
/modlist
/modlist version
/modlist full json
/modlist version txt my-mods
/list config full json
/list client full
```

## The chat view

The default `chat` output is built to be read at a glance:

* the mod id, display name, version and side badge are each colored
* **hover** any entry to get the full metadata card — id, version, side, jar file, license and
  description — even in `basic` mode
* **click** an entry to copy the mod id (or the absolute path for a config file)
* the footer offers a ready-to-click export command, e.g. `/modlist version json`
* after an export, a `[Copy path]` button appears

`/list` opens a visual cheat sheet where every command and example is clickable and inserts
itself into the chat bar.

## File exports

`txt` and `json` are written to the game's `logs/` folder. Nothing else on disk is touched.

```json
{
  "type": "mod",
  "details": "version",
  "generatedAt": "2026-10-16T19:39:14.529231Z",
  "count": 3,
  "columns": ["id", "name", "version"],
  "entries": [
    {"id": "minecraft", "name": "Minecraft", "version": "1.21.1"},
    {"id": "neoforge", "name": "NeoForge", "version": "21.1.209"},
    {"id": "simplelists", "name": "Simple Lists", "version": "1.0.0"}
  ]
}
```

## Notes

* **Read-only.** The mod never modifies anything. It only reads mod metadata and the `config`
  folder.
* **No plugins.** NeoForge has no separate plugin concept, so `/pluginlist` is an alias for the
  server-side mod list.
* **How sides are detected.** A mod counts as client- or server-only if it declares a `neoforge`
  dependency with `side="CLIENT"` or `side="SERVER"` — the standard NeoForge convention. Mods
  without such a marker count as `BOTH`.
* Exports land in `logs/`, so they are easy to attach to a bug report.

## Compatibility

* Minecraft **1.21.1**
* NeoForge **21.1.209 or newer**
* Works on both the client and a dedicated server
* No dependencies
* In future will be more versions

## Gallery 

* All the mods in the photos are just examples
* Only explicit examples of chat commands are displayed
* You can get familiar with json and txt file types in practice.

## License

MIT
