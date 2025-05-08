---
title: Messing with the zsh not-found handler
date: 2025-05-08
permalink: /zsh-not-found-handler
---

# Messing with the zsh not-found handler

Last week, I saw [this post](https://www.reddit.com/r/commandline/comments/1k7ix0h/silly_little_program_for_silly_people/) on reddit, which features a nice chad ASCII art.

![chadsay](https://preview.redd.it/silly-little-program-for-silly-people-v0-8375wim1yywe1.png?width=640&crop=smart&auto=webp&s=1f6fef2bad70e6d4bdaccd8a0613c8e9a2627ac2)

I thought it was pretty cool, so of course I decided to try it out.

![chadsay](https://btj93.github.io/zsh-not-found-handler/chadsay.png)

Then I thought, why not make it a little more useful?

## Zsh not-found handler

An idea came to me, I could make chad say something when the user typed the wrong command.

So after some goggling, it turns out that `zsh` already has support for executing custom code when the user types a wrong command.

By defining the following function in `.zshrc`, we can override the message when the user types a wrong command.

``` bash
command_not_found_handler() {
  echo "Oops! I don't know what you mean by $1."
}
```

![command-not-found](https://btj93.github.io/zsh-not-found-handler/command-not-found.png)

Now we have every piece of the puzzle. It is time to put it all together.

## Chad roasting the user

I *"borrowed"* the `chadsay` line from the reddit post.

``` bash
command_not_found_handler() {
    chadsay "'$1' not working?"$'\n'"Not my problem."
}
```

![chad-roasts](https://btj93.github.io/zsh-not-found-handler/chad-roasts.png)

## More chaos

To improve the experience, we can create an array of sentences to say, and choose one randomly when the user types a wrong command.

``` bash
command_not_found_handler() {
    quotes=(
        "'$1' not working? Not my problem."
        "'$1' is lost? Not my circus."
        "'$1' failed? Not my fault!"
        "'$1' gone? Oh well!"
    )
    random_index=$((RANDOM % ${#quotes[@]} + 1))
    random_quote=${quotes[random_index]}
    chadsay "$random_quote"
}
```
