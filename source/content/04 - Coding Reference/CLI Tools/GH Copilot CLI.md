---
tags:
  - github
  - command-line
---


## Overview

> GitHub CLI is an open source tool for using GitHub from your computer's command line. When you're working from the command line, you can use the GitHub CLI to save time and avoid switching context.
   
   >GitHub Copilot in the CLI is an extension for GitHub CLI which provides a chat-like interface in the terminal that allows you to ask questions about commands you run from the command line. You can ask Copilot in the CLI to suggest a command for your use case, with `gh copilot suggest`, or to explain a command you're curious about, with `gh copilot explain`.
   >
   >>[!info] [Documentation](https://docs.github.com/en/copilot)

## Installation and Upgrade

>[!terminal] Requires authentication through `gh auth login`
>Installation :FasArrowRight: `gh extension install github/gh-copilot`
>Version :FasArrowRight: `gh copilot --version`
>Update :FasArrowRight: `gh extension upgrade gh-copilot`

## Usage

>[!terminal] Commands start with `gh copilot`
>
>Help :FasArrowRight: `gh-copilot --help`
>Explain :FasArrowRight: `gh copilot explain` or `gh copilot explain [$COMMAND]`
>Suggest :FasArrowRight: `gh copilot suggest` or `gh copilot suggest [$COMMAND]`
>Config :FasArrowRight: `gh copilot config`
>

## Tips

>[!tip] Using explain
>When using `explain`, you can write your prompt in natural text between quotations. For example `gh copilot explain 'how to restart shell after updating ~/.zshrc'`

>[!tip] Using suggest
>The `[$COMMAND]` argument to `suggest` is best used when you already know what command you would like to use. For example `gh copilot suggest "Install git"`

