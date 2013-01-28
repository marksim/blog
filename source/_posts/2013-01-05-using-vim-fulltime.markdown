---
layout: post
title: "Using VIM Fulltime"
date: 2013-01-05 09:27
comments: true
categories: 
---

I've used various IDEs for the last 10 years of development.  Started with [Eclipse](http://eclipse.org) while developing in Java.  Switched to [TextMate](http://macromates.com) when I moved to a Mac and started developing in Ruby.  Eventually, TextMate's development became stale and things other people were able to do with their editors started to look good.  I began searching, and even bought a license for [Sublime Text 2](http://sublimetext.com).  It had a lot of what I was looking for, but what I wanted was an editor that let me never leave my keyboard unless I wanted to and had good integration points.  I'd love a good fullscreen mode since I'm a bit of a FullScreen addict on Mac.  

Turns out, there's no such editor.

There's one that can come close, though; the editor I've used for little tasks for over 15 years... [VIM](http://www.vim.org). 

## Just a Text Editor?

VIM isn't just a text editor.  I've used it since my sophmore year in college to handle little tasks on servers since it's ubiquitous and powerful enough.  I know my way around without the arrow keys, and how to insert, etc, but I'd never really used Visual mode or tried to handle anything more than one file at a time.

There were a handful of commands, .vimrc configurations, and plugins that helped me get past all that.

## Commands I already knew

1. `i`/`I`/`a`/`A` - enter insert 
1. `o`/`O` - enter insert mode on line below/above
2. `p`/`P` - paste deleted/yanked text on line below/above
3. `Y` - Yank the currently selected line(s)
4. `/` - search file
5. `:##` - go to line
6. `:wq` - write and quit
7. `d` - delete, `dd` - delete row. `d3` - delete 3 rows
8. `jklh` - directions without using arrows.  Awesome.

## Favorite New Commands

1. `V` - Visual Mode

    The VISUAL mode is something I'd seen a lot, but hadn't really understood.  Now it's invaluable.

2. `Ctrl-V` - Vertical Splits

    Vertical splits were something I always wanted, but never quite understood.  I ended up with them randomly and then would :q vim to get out.  Now I know and master them.

3. `:bd` - Delete Buffer

    Delete the current buffer.  This lets you close a file quickly.

4. `Ctrl-ww` - Change Windows

    Quickly change from one split to another.

5. `:e <file>` - create a new file

    Lets me create a new file without leaving vim

6. `:!<command>` - execute a shell command and then return.

    Useful for rake tasks, git pushes, etc.

7. `W`, `w`, `B`, and `b` - word navigation

    Forward and backward one word or one "programming" word.  Can also be combined with d to delete words, etc.

## .vimrc

In my [.vimrc](https://gist.github.com/4472002), I did a handful of things that were helpful to me that I'd never done before:

1. Turned on the 80 column highlight
2. Turned on syntax highlighting
3. Turned on autoindent and :ack
4. Mapped my LEADER key to ','
5. Automatically stripped trailing whitespace on save.
6. And provided a crude tab-complete

## Useful Plugins

1. [Pathogen](https://github.com/tpope/vim-pathogen)

    A plugin to manage plugins.  Makes it easy as long as you have a git repo to clone.

2. [Command-T](https://github.com/wincent/Command-T)

    Lets me use `<leader>-T` to do what I'd do in TextMate/Sublime to find a file in the project

3. [NerdTree](https://github.com/scrooloose/nerdtree)

    I needed it at first, but now, not as much.  Good to have for periodic filesystem navigation

4. [Fugitive](https://github.com/tpope/vim-fugitive)

    A good git plugin that provides the `:Gstatus` command, which let me quickly stage/unstage files, see diffs, and blame

5. [Ack](http://www.vim.org/scripts/script.php?script_id=2572)

    Lets me search the whole project quickly and navigate the results.  This was the final "missing piece" to get off of Sublime/TextMate.
    I would always go back becuase I didn't want to use a goofy RegEx to do very basic searching in my project--luckily Ack and ack.vim provide it quickly and with great result navigation

## Taking the plunge

Ultimately, the things that really helped me were getting to know a few basic commands, installing Command-T and Ack, and tweaking with my VIMRC.  I've been using VIM for years and never really got it until the last month.  Over the last 2 weeks, I've actually made it my primary editor and only brought up SublimeText 2 once.  Now, all I have to load up to get started is iTerm + vi.  Guard runs in a separate pane and everything else can be done from inside VI.  

Now I have a long way to go before I become a VIM ninja, but this is what got me started.  Maybe it will help you too.
