---
name: git-identity-confirm
license: MIT OR Apache-2.0
description: >-
  Ask the user which Git identity (`user.name` and `user.email`) a repository
  should use before the first commit in a repository that came into existence
  during the task (`git init`, `git clone`, or as a side effect of another
  tool). Never skip the question because the answer seems obvious.
---

# git-identity-confirm

A repository that has just been created or cloned has no identity of its own
and silently inherits the global default. Once a commit under the wrong
identity is pushed, it exposes a name and email address where they do not
belong, to everyone with access to the remote, and history rewriting is the
only way back. So before the first commit in such a repository, stop and ask
the user which identity it belongs to.

## Before asking, gather the facts

Collect the identity currently in effect:

```sh
git -C <repo> config --get user.name
git -C <repo> config --get user.email
git -C <repo> config --local --get user.name
git -C <repo> config --local --get user.email
git -C <repo> remote -v
```

## Ask

Ask one question: which `user.name` and `user.email` this repository should
use. Offer a default the user can confirm with a word or replace with
another, and wait for the answer.

## Apply

Set the identity locally in the repository, even when it equals the global
default, so the choice survives any later change to the global
configuration:

```sh
git -C <repo> config user.name "<name>"
git -C <repo> config user.email "<email>"
```

## Report

State in the completion message which identity the repository is set to use.
