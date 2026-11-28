# Caelo on Scoop (Windows)

[Caelo](https://caelo.sh) is a free, local security scanner for apps built with AI coding
tools (Lovable, Bolt, Cursor, v0, Replit). It finds exposed keys, browser-leaked secrets,
open Firebase or Supabase rules, and committed `.env` files. It runs entirely on your
machine: it reads files, uploads nothing, and redacts every secret value it reports. By
Irth Labs.

This is a [Scoop](https://scoop.sh) bucket that installs the `caelo` command on Windows.

## Install

```powershell
# 1. Add this bucket
scoop bucket add caelo https://github.com/arthi-arumugam-git/scoop-caelo

# 2. Install Caelo (Node.js is pulled in automatically as a dependency)
scoop install caelo
```

Then:

```powershell
caelo .           # scan the current folder
caelo --mcp       # run Caelo as an MCP server over stdio
```

## Update

```powershell
scoop update caelo
```

## Uninstall

```powershell
scoop uninstall caelo
```

## How this manifest works

Caelo is an npm-based CLI (not a standalone compiled binary), so this manifest installs it
through npm:

- It declares `"depends": "nodejs"`, so `scoop install caelo` installs Node.js first if you
  do not already have it via Scoop.
- Scoop downloads the versioned npm tarball and verifies its SHA-256 hash before extracting it.
- Its install script uses `npm install --global --install-links --ignore-scripts "$dir"` to install that verified local package and its dependencies.
- The `caelo` command is provided by npm's global bin directory, which Scoop's `nodejs`
  package adds to your PATH. (This is the one caveat of installing an npm CLI via Scoop:
  the executable lives in npm's global prefix rather than Scoop's own `shims` directory.)

If you only ever want a one-off scan and already have Node, you do not even need Scoop:
`npx caelo .` works directly.

## Maintainer notes

- `checkver` reads the latest version from the npm registry
  (`https://registry.npmjs.org/caelo/latest`), so `scoop status` reports new releases.
- `autoupdate` selects the matching versioned npm tarball. Review its download hash and verify the installed CLI and MCP entrypoints before publishing a bucket update.
- Validate the manifest against Scoop's schema before publishing:
  `https://raw.githubusercontent.com/ScoopInstaller/Scoop/master/schema.json`.
