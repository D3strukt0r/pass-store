# AGENTS.md

This file provides guidance to AI coding agents when working with this repository.

## What this repo is

This is a **personal [pass](https://www.passwordstore.org/) password store**, not a software project. There is no code to build, lint, or test. The tracked content is:

- `*.gpg` — GPG-encrypted password entries. Directory layout = category hierarchy.
- `.gpg-id` — the GPG key ID (`D3strukt0r`) authorized to decrypt entries.
- `docker-credential-helpers/` — credential data written by [`docker-credential-pass`](https://github.com/docker/docker-credential-helpers) (Docker's pass-backed credential helper). Treat it as data owned by that tool — do not hand-edit.
- `.gitattributes` enables `diff=gpg` for `*.gpg`, so diffs decrypt on the fly if a GPG key is available.

The repo is expected to live at pass's default path: `~/.password-store` on Linux/macOS, `C:\Users\<user>\.password-store` on Windows (required by browserpass-native — see README).

## Working in this repo

- Never write plaintext secrets to disk. Mutations to password entries must go through `pass insert`, `pass edit`, `pass generate`, `pass mv`, `pass rm`, etc., so entries stay encrypted and re-encrypted against `.gpg-id`.
- Do not commit decrypted files or exported keys. `.gitignore` excludes agent-local config (`.claude/settings.local.json`, `CLAUDE.md`).
- `.gpg` files are binary/encrypted — file-read and content-search tools cannot introspect contents. Don't attempt to read them to "understand the data"; ask the user instead.
- The `docker-credential-helpers/` directory contains opaque base64-named files managed by the Docker helper. Leave it alone unless the user is explicitly debugging Docker credentials.

## Conventions

- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) (per README).
- **Editor**: `.editorconfig` enforces LF, UTF-8, 2-space indent, trimmed trailing whitespace, final newline.
- **CODEOWNERS**: `@D3strukt0r` owns everything.

## GitHub automation (`.github/`)

- `dependabot.yml` + `dependabot-automerge.yml` / `dependabot-validate.yml` workflows auto-manage GitHub Actions version bumps.
- `greetings.yml`, `label.yml`, `stale.yml` — community automation. None of these affect local work.
