# skills

![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)

Agent skills written by [hainet50b](https://github.com/hainet50b). A skill is a
directory of instructions an AI coding agent loads on demand, following the
[Agent Skills specification](https://agentskills.io/specification).

## Skills

| Skill | Description |
|-------|-------------|
| [git-identity-confirm](git-identity-confirm/) | Ask the user which Git identity a newly created or cloned repository should use before its first commit. |
| [gh-markdown-preview-run](gh-markdown-preview-run/) | Run [gh-markdown-preview](https://github.com/yusukebe/gh-markdown-preview), the GitHub CLI extension that renders Markdown as GitHub does, from start to shutdown. |
| [plain-language](plain-language/) | Apply plain-language principles when writing, editing, reviewing, or translating natural-language documents and AI responses. |

## Installation

Install a skill with [GitHub CLI](https://cli.github.com/)'s `gh skill`:

```sh
gh skill install hainet50b/skills gh-markdown-preview-run --agent universal --scope user
```

Pass `--agent claude-code` (or another agent) for agents that load skills only
from a directory of their own. See `gh skill install --help` for the full list.

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
