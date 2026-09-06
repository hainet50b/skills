---
name: gh-markdown-preview-run
license: MIT OR Apache-2.0
description: >-
  Run gh-markdown-preview, the GitHub CLI extension that renders a local
  Markdown file the way GitHub does, from start to shutdown. Use only when
  the user asks to preview a Markdown file or asks how a Markdown file will
  look on GitHub.
---

# gh-markdown-preview-run

[gh-markdown-preview](https://github.com/yusukebe/gh-markdown-preview) is a
[GitHub CLI extension](https://cli.github.com/manual/gh_extension).
`gh markdown-preview <file or directory>` starts a local web server that
renders Markdown as GitHub would and reloads the browser whenever a file under
the served directory changes. Start it in the background, hand the user the
URL, and stop it when the work is done.

## Before starting

- If the extension is not installed, its source is
  `yusukebe/gh-markdown-preview`. Whether to install it, whether to do so
  with `gh extension install yusukebe/gh-markdown-preview` or through whatever
  the user uses to manage tools on the machine, and who runs the install are
  the user's decisions.
- The default port is 3333 on `localhost`. Reuse a running server only if
  you started it in this session for this project. Any other listener on the
  port — another session, another project, a leftover — is not yours: do not
  hand out its URL and do not kill it; pick a free port and pass `-p <port>`.

## Start

Run it as a background process so the conversation continues. Serve the
root of the project that contains the file, not the file alone, so one
server covers every Markdown file the user may ask for next. Resolve that
root from the file's location, not from your current directory — a session
may be working across several repositories. For a git repository, for
example:

```sh
root=$(git -C "$(dirname path/to/file.md)" rev-parse --show-toplevel)
cd "$root" && gh markdown-preview .
```

- Every file under the served directory is reachable by its relative path,
  e.g. `http://localhost:3333/path/to/file.md`. The bare `/` shows the
  README, and the browser the server opens by itself lands there, so always
  give the user the URL with the file's path in it.
- Add `--disable-auto-open` when you start the server only to check that it
  serves, so a browser tab does not appear unasked.
- GitHub-specific output such as Mermaid diagrams is drawn by JavaScript in
  the browser, so you cannot see the rendering from the shell: let the user
  judge, and do not report that the page renders correctly. Probe the server
  only when you have reason to doubt it is serving the file; if you do, the
  page returns 200 for any path, so query `/__/md?path=path/to/file.md`
  instead.

## Stop

Stop the server when the user is done looking, and always before the session
ends unless they asked to keep it running.

- Terminate the server process itself, found by the port it listens on; the
  background task that started it ends with it. Stopping the task alone can
  leave the process alive and holding the port.
- Report that the server is stopped.
