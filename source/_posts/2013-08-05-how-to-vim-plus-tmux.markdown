---
layout: post
title: "How To VIM+TMUX"
date: 2013-08-05 13:16
comments: true
categories: vim tmux blog
---

<iframe width="560" height="315" src="//www.youtube.com/embed/gB-JSh1EVME" frameborder="0" allowfullscreen></iframe>

[Chris Hunt](http://twitter.com/chrishunt) gave a great presentation at LA Ruby
Conf about
[VIM+TMUX](http://www.confreaks.com/videos/2291-larubyconf2013-impressive-ruby-productivity-with-vim-and-tmux).
There, he shows you a bunch of cool things you can do with VIM and TMUX.

But he doesn't tell you *how* to do them.

So here, I'm going to list each of the things he does and give you the
keystrokes/information you need to do what he's talking about.


## TMUX

For these shortcuts, the `prefix` is mapped to `C-b` (i.e. `Ctrl-b`) -- though
I believe it is much faster and more comfortable to map it to `C-a`.  Chris
even maps his to `C-j` so you use two different hands.

* 3:51 - List Keyboard Shortcuts - `C-b ?`
* 4:06 - [Chris Hunt's TMUX Config](http://goo.gl/98M56)
* 4:30 - Create New Window - `C-b c`
* 4:35 - Rename Window - `C-b ,`
* 4:39 - Change Windows Absolute - `C-b 0|1|2|3|4|5`
* 4:39 - Change Windows Relative - `C-b n|p`
* 4:46 - Switching to Last Used window `C-b l`
* 4:49 - Split Window vertically into Panes - `C-b %`
* 4:52 - Split Window horizontally into Panes - `C-b "`
* 6:18 - See List of sessions - `C-b w`
* 7:06 - Auto-start iTerm with tmux `tmux attach -t hack || tmux new -s hack`
* 11:10 - Detach from session - `C-b d`
* 17:50 - Make a new, shared tmux session `tmux -S /tmp/pair new -d math &&
  chmod 777 /tmp/pair && tmux -S /tmp/pair attach`
* 19:14 - Attach to a shared tmux session `tmux -S /tmp/pair attach`


## VIM

* 7:30 - Fuzzy search with
  [CtrlP](http://kien.github.io/ctrlp.vim/#installation)
    - `C-p [search]` to find files
* 8:22 - Profject wide search with [Ag](https://github.com/epmatsw/ag.vim) 
    - `:Ag [text]` to find text
* 9:18 - [Surround](https://github.com/tpope/vim-surround)
    - change double quotes to single quotes while within double quotes: `cs"'` 
    - change `[` to `(` while within square brackets: `cs[(`
* 10:39 - Aligning code with [Tabular](https://github.com/godlygeek/tabular) 
    - `:Tabularize /<regex to match>/`
* 12:18 - Run bundle within vim `:!bundle`
* 13:23 - Create new spec file `:e spec/math_spec.rb`
* 14:22 - Running tests within VIM - [Gary Bernhardt's RunTests in
  .vimrc](https://github.com/garybernhardt/dotfiles/blob/master/.vimrc#L310-L362)
* 15:44 - Make a Gist of the current buffer with `:Gist`
  ([Gist-Vim](https://github.com/mattn/gist-vim))
* 19:56 - Using the Arglist for global search and replace
    - Find all files <code>:args `ag -l MyAwesomeApp .`</code>
    - View args `:args`
    - Execute a replace across files (with confirmation) `:argdo
      %s/MyAwesomeApp/ToDoApp/gc | w`
* 21:54 - VIM Macros
    - To start recording `Esc q a`
    - To stop recording, in command mode, `q`
    - To execute recording, in command mode, `@a`
    - To execute multiple times, in command mode `9@a`
    - To execute across arg files: `:argdo norm @a`


