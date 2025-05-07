---
title: Mastering the global Command in Vim
date: 2025-05-10
permalink: /vim-g-command
---

<https://www.reddit.com/r/neovim/comments/1jy5gyf/how_would_you_go_about_editing_this/>

# Mastering the global Command in Vim

The `global` command in Vim is a powerful tool for executing commands on all lines that match a specific pattern.

The `global` command has the following syntax:

```
:g/pattern/command
```

This command allows you to perform various actions, including substitutions, deletions, and more, making it an essential feature for any Vim user. In this article, we will explore the syntax of the `global` command, its various options, and how to chain it with the `substitute` command for efficient text editing.

## Basic Syntax

The basic syntax of the `global` command is as follows:

```
:g/pattern/command
```

- `:g` indicates that you are using the `global` command.
- `pattern` is the text you want to search for.
- `command` is the action you want to perform on the matching lines.

### Example

To delete all lines containing the word "error", you would use:

```
:g/error/d
```

This command will remove all lines that match the pattern "error" from the current buffer.

## Viewing Grep Results

After running a `global` command, you can see the results directly in the buffer. If you want to perform actions on the matching lines, you can use the command in conjunction with other Vim commands.

## Chaining Commands with Global and Substitute

It is not a coincidence that the [last post](https://btj93.github.io/nvim-substitute-command) is about another command in vim.

One of the powerful features of Vim is the ability to chain commands together. You can use the `global` command in combination with the `substitute` command to quickly find and replace text across all matching lines.

### Grep and substitute synergy

Suppose you want to find all lines that has the word "foo" in your file and replace the whole line with "bar". You can do this in one command:

```
:g/foo/s/.*/bar/g
```

This is particularly useful when you want to have the condition and the replacement string be different.

- `:g` is the command to execute on all lines that match the pattern.
- `foo` searches for the lines that contains the word "foo".
- `s/.*/bar/g` is the command to execute on the lines that match the pattern.
  - `.*` matches any character
  - `bar` is the replacement string

### Real world example

This example is based on a [reddit post](https://www.reddit.com/r/neovim/comments/1jy5gyf/how_would_you_go_about_editing_this/).

initial text:

```
line of code 1
# comment 1
line of code 2
# comment 2
line of code 3
# comment 3
```

result:

```
line of code 1
line of code 2
line of code 3
# comment 1
# comment 2
# comment 3
```

#### Solution 1

With the `global` command, we can use the following command:

```
:g/#/m$
```

- `g` is the command to execute on all lines that match the pattern.
- `#` searches for the lines that contains the `#` character.
- `m$` is the command to execute on the lines that match the pattern. In this case, it moves the line to the end of the file, denoted by `$`.

#### Solution 2

Another solution is to use this command:

```
:g/^#/norm ddGp
```

- `g` is the command to execute on all lines that match the pattern.
- `^#` searches for the lines that starts with `#`.
- `norm ddGp` is the command to execute on the lines that match the pattern.
  - `norm` executes a normal mode command
  - `dd` deletes the line
  - `G` moves the cursor to the end of the file.
  - `p` pastes the deleted line below the current line.

In this solution, we can observe that the `norm` allows us to execute a normal mode keymap, which allows us to use normal mode keymaps to process the line.

## Advanced global Options

The `global` command also supports several options to refine your actions:

- `!`: Negate the pattern, applying the command to lines that do not match the pattern.
- `c`: Confirm each action before it is executed.

You can use these options to customize how the `global` command behaves. For example, to confirm each substitution, you can use:

```
:g/foo/s//bar/gc
```

## Conclusion

Mastering the `global` command in Vim is essential for efficient text manipulation. By understanding its syntax and options, you can quickly perform actions on all lines that match a specific pattern. Additionally, chaining the `global` command with the `substitute` command allows for powerful text editing capabilities. Practice using these commands to enhance your productivity in Vim.

Happy editing!
