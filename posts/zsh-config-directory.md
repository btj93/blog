---
title: Changing the zsh config directory
date: 2025-05-07
permalink: /zsh-config-directory
---

# Changing the zsh config directory

I've been using zsh for a while now, and I've been using the default config directory for it.

By default, it is located at `~/.zshrc`.

Recently, I want to add some bash script to my zsh config, and I want to keep them in a separate directory for easier git management.

## The problem

When we add a external bash script to our zsh config, it is easy to forget to track it in git, because,

1. the script in the same directory as the zsh config, which is the root directory, and it is cluttered with all sorts of files,
2. the script is not in the same directory as the zsh config, which makes it hard to track it in git.

## The solution

So I decided to create a new directory for my zsh config, and I'll put the script in there.

To align with other config directories, I decided to use `~/.config/zsh`.

Here is the directory structure:

```
~/
├── .config
│   └── zsh
│       ├── script1.bash
│       └── .zshrc
└── .zshenv
```

The `.zshenv` file is a file that is sourced when zsh starts up.

## Tell zsh to use the new config directory

To tell zsh to use the new config directory, we need to add the following line to the `.zshenv` file:

``` zsh
export ZDOTDIR=~/.config/zsh
```

Now, when we start zsh, it will use the new config directory.

### Troubleshooting

During the process of setting up the new config directory, I encountered a few issues.

#### command not found: `brew`

The `~/.config/zsh/.zshrc` file could not find the `brew` command.

I ended up adding the following line to the `~/.config/zsh/.zshrc` file:

``` zsh
eval "$(/opt/homebrew/bin/brew shellenv)"
```

#### Homebrew packages not found

I also encountered a few issues with homebrew packages not being found, even though they are installed.

Specifically, I use the [`pure`](https://github.com/sindresorhus/pure) prompt for zsh, and it is installed via homebrew.

However, when I run `prompt list` in the terminal, `pure` is not listed.

I ended up adding the following line to the `~/.config/zsh/.zshrc` file:

``` zsh
fpath+=("$(brew --prefix)/share/zsh/site-functions")
```

That solved the issue.

## Conclusion

This is a simple solution to the problem of having a separate config directory for zsh.

With this method, you can isolate the zsh config and scripts to the config directory, and it is easy to track the script in git.
