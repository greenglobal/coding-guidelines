
Python coding style guide
===================

#### Contents
- [Intro](#intro)
- [Setup linters on the popular editors](#setup-linters-on-the-popular-editors)
  - [VIM](#vim)
  - [Atom](#atom)
  - [Sublime Text 3](#sublime-text-3)
  - [Visual Studio Code](#visual-studio-code)
- [Verify standard compliance with bash script](#verify-standard-compliance-with-bash-script)
- [Auto verify standard compliance on GitLab](#auto-verify-standard-compliance-on-gitlab)

## Intro

In this project, we apply PEP8 standards. This is the full list of rules:

[PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)

In summary, here are  the most important rules we need to remember:

- **Shebang**: always begin with `#!/usr/bin/env python3`
- **File encoding**: UTF-8
- **Indentation**: 4 spaces
- **Maximum line length**: 79
- **Comments**: start with `#`, line by line
-  **Naming conventions**: `CamelCase` for Class name, `UPPERCASE` for constants, otherwise, `lowercase` and `under_score`

There is something called "The Zen of Python", you can get it by running `python` command, then type `import this`:

````
...
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
...
````

However, don't try to remember all the rules. Let's the tools help you.


## Setup linters on the popular editors

It's recommended to use linters to verify coding standard as you typing. Here we intro how to setup linters on the popular source code editors.

But at first, we need to install [flake8](https://pypi.org/project/flake8/):

```bash
sudo apt install flake8

# or using pip
sudo pip3 install flake8
```

Then, depending on the editor, we are going to install some plugins.


####  Visual Studio Code

Press Ctrl + Shift + X (or  File --> Preferences --> Extensions) to go to Extensions tab. Enter "python" into search field then install Python if not yet.

![enter image description here](https://i.imgur.com/1KBcYiG.png)

Press Ctrl + Shift + P (Or View --> Command Palette) to show Command Palette, enter `Python: Enable Linting`, select `On` to enable linting.

Go to Command Palette again, enter `Python: Select Linter`, choose `flake8`.

![enter image description here](https://i.imgur.com/5qCocsc.png)

If you see something like below, just click `install`:

![](https://i.imgur.com/mA7Vrfl.png)

Back to 

![](https://i.imgur.com/i7aO0e0.png)

You can go to File --> Preferences --> Settings --> Extensions, find Python group to personalize the display.

There maybe more settings relating to linter, please refer:

- [Linting Python in Visual Studio Code](https://code.visualstudio.com/docs/python/linting)
- [Configure flake8](https://code.visualstudio.com/docs/python/settings-reference#_flake8)



#### VIM

You can install the following plugins using your favorite plugin manager:

- [ALE](https://github.com/w0rp/ale)
- [lightline](https://github.com/itchyny/lightline.vim)
- [lightline-ale](https://github.com/maximbaz/lightline-ale)

In `.vimrc` or alternative VIM config file, just add something like below:

```bash

let g:lightline = {
      \ 'colorscheme': 'Dracula',
      \ 'active': {
      \   'left': [
      \               ...
      \           ],
      \   'right': [
      \               [ 'linting', 'fileencoding', 'filetype'],
      \   ],
      \ },
      \   'linting': 'LinterStatus',
      \ },
      \ }

function! LinterStatus() abort
    let l:counts = ale#statusline#Count(bufnr(''))

    let l:all_errors = l:counts.error + l:counts.style_error
    let l:all_non_errors = l:counts.total - l:all_errors

    return l:counts.total == 0 ? 'OK' : printf(
    \   '%dW %dE',
    \   all_non_errors,
    \   all_errors
    \)
endfunction

let g:ale_sign_column_always = 1

let g:ale_linters = {
\   'python': ['flake8'],
\}

```

Now VIM is already able to check if your code follows PEP8 standard:

![](https://i.imgur.com/lTUAKyF.png)

####  Atom

With Atom, these plugins are required:

- [linter](https://github.com/steelbrain/linter)
- [linter-ui-default](https://github.com/steelbrain/linter-ui-default)
- [intentions](https://github.com/steelbrain/intentions)
- [busy-signal](https://github.com/steelbrain/busy-signal)
- [linter-flake8](https://github.com/AtomLinter/linter-flake8)

You can install them using `apm`:

```
apm install linter linter-ui-default intentions busy-signal
apm install linter-flake8
```

After installing finished, please go to packages settings to modify the options as you want.

*Recommended settings*

- **linter**:
   - Link Preview Tabs: ON
   - Link on Open: ON
   - Link on Change: ON
 - **linter-ui-default**:
   - Always Take Minimum Space: ON
   - Hide Panel When Empty: ON
   - Show Decorations: ON
   - Show Status Bar: ON
   - Show Tooltip: ON
   - Statusbar Represents: Entire Project

![enter image description here](https://i.imgur.com/irUfWlW.png)

####  Sublime Text 3

In Sublime, after getting [Package Control](https://packagecontrol.io/installation) already, please install these 2 packages:

- [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter)
- [SublimeLinter-flake8](https://github.com/SublimeLinter/SublimeLinter-flake8)

There is no special settings, however the following values are recommended:

```json
{
        "default_line_ending": "unix",
        "draw_white_space": "all",
        "ensure_newline_at_eof_on_save": true,
        "show_encoding": true,
        "show_line_endings": true,
        "tab_size": 4,
        "translate_tabs_to_spaces": true,
        "trim_trailing_white_space_on_save": true,
        "word_wrap": "false"
}
```

![enter image description here](https://i.imgur.com/ZWyY75g.png)



___________________
