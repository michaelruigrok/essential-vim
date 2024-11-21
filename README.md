# Michael's Essential Vim 

This guide intends to help you use vim effectively with minimal learning involved.

The focus here is on *what to learn first*, based on what features give you the
most bang for your buck. Each section teaches you just a few keybinds, which you
can use until they become second nature, then you can move to the next section at
your own pace.

As such, this guide isn't focused on giving the best explanations. To gain a
deeper understanding, look at the documentation (`:help`, 
[the Vim wiki](https://antifandom.com/vim/wiki/Vim_Tips_Wiki),
[SO](https://stackoverflow.com/questions/tagged/vim?tab=Votes), etc) 

Still, stay curious! If you want to know how to do something *now* (for instance,
how to replace all instances of a given word), the answer is just a google away.

## vimrc

The vimrc file (`$HOME/.vimrc` on linux/mac or `$HOME/_vimrc` on Windows) stores
personal configuration for vim.

These options are maximally recommended to all skill levels. You're welcome to
smack them in your vimrc file without thinking, but descriptions are given if you
want them.

```vim
""" Essential
set mouse=a " allow use of mouse
set backspace=indent,eol,start " always allow backspace in insert mode
set nocompatible " ensure vim features are available

""" Critical
syntax on " syntax highlighting
filetype plugin indent on " detect file type
set smartcase " case insensitive search, unless you use a capital letter.

set incsearch " Starts searching while you type in your search
set hlsearch " Highlights all search instances

set autoindent  " copy previous line's indent
set smartindent " increase indent after start of new block (e.g. '{')

" In command mode, first tab fills in the longest common match
"  Second tab displays list. Two more tabs will iterate over that list.
set wildmode=longest,list,list,list:full
set wildmenu

""" Personal Preference
colorscheme desert " best stock colourscheme
set background=dark
set noeb vb t_vb= " disable beeping
```

## Keybinding Legend
The thing that makes vim actually good is how shortcut keys are typed in
combination to form custom and powerful actions (almost like combining words
into a sentence). Each keybind performs a particular role in these commands.
You'll see what I mean later, but to help I've marked each keybinding with the
category it falls under using the following legend:

- 👟 - Movement key. Changes the position of the text cursor or text selection.
- 💥 - Action key. Actually edits text, or modifies a file, etc
- 🌧 - Mode change key. Going from normal mode/insert mode/command mode etc
- 📣 - Command-line command. Not technically a keybinding, and doesn't actually
interact with the special keybind grammar. But still lets you do powerful
things.
- 🦚 - Other

## Absolute Beginner 
- 👟 [Mouse click/scroll] - Move cursor (make sure you have the vimrc above)
- 🌧 i - insert mode
- 🌧 Escape - leave insert mode 
- 📣 :wq - save and quit (mnemonic: write, quit)
- 📣 :q! - quit without saving (mnemonic: "quit!")
- 👟 / - search file (mnemonic: ? key) (full regex support)
- 👟 [arrow keys] - Move cursor

## Novice

### Mechanic: Visual Mode
A 'Selection' or 'Highlight' mode, where you select/highlight the text you want
to perform an action on. To activate it, just click and drag over text as you
would in a GUI text editor (or press 'v'). Pressing 👟 Movement keys in this
mode will change the text selection.

When in visual mode, any 💥 Action key you press will instantly operate on the text
you have currently selected. For instanmce, if you press `d`, your highlighted
text will be deleted.

### Keybinds
- 💥 d - delete text
- 💥 y - copy text (mnemonic: 'yank')
- 💥 p - paste text
- 💥 u - undo last action
- 💥 ctrl-r - redo last action
- 📣 :s/{old}/{new} - substitute occurrences of {old} with {new}

## Great bang-for-buck keyboard movements

### Mechanic: Shift modifier type 1 - 
Holding Shift and pressing a 👟 movement key _reverses_ the direction of the
movement. 

Like /, ? searches text, but _backwards_ from the cursor position, instead of
forwards. Some more useful examples are in the following keybinds.

Some 💥 Action keys (like 'p/P' for paste) also operate this way.

### Keybinds

- 👟 f/F{character} - move back/forward to the next instance of the character.
	(mnemonic: 'find')
- 👟 n N - move to next/previous search occurence
- 👟 {number}G - move to line number (or last line if no number given)
- 💥 < > - indent left/right

## Situational Movement 1

### Keybinds
- 👟 % - Jump to the bracket (`()<>[]{}`) matching the one under the cursor
- 🌧 o O - create an empty newline below/above the current line, and enter insert
mode on it.
- 👟 ^ - move to start of current line
- 👟 $ - move to end of current line
- 👟 { } - move to the previous/next blank line after a block of text (i.e, move a
paragraph up/down).

### Mechanic: linewise actions with keybind double-press

From normal mode (without pressing any keybind beforehand), pressing an action
keybind twice will perform that action on the line the cursor is currently on.
For instance, `dd` will delete the entire line, and `yy` will copy the entire
line.

## In/Around movements
- 👟 i{key}
- 👟 a{key}

{key} can be one of the following:

- any bracket or quote (`` '"`{}[]()<> ``) - inside the closest surrounding pair of
	chars
- p - paragraph
- s - sentence
- t - tag (`<html></html>`)
- w - word (up to alphanumeric only)
- W - word (including symbols, up to spaces)

## Once you're comfortable with the idea of moving the cursor with shortcut keys
- 👟 h j k l - Home row < v ^ >
- 👟 w W b B e E - Word-wise movement (follows word/Word convention instead of
reverse convention)

### Mechanic: {action} {movement} grammar
An 💥 Action key followed by a 👟 Movement key will perform that action from the
current cursor postion to the postion the cursor would be after that movement.

## Advanced // Extensions on Old Concepts
- 💥 . - repeat last 💥 Action (best used from normal mode)
- 💥 c - change text, i.e. delete and enter insert mode. Very powerful in
	combination with '.', since it includes the replaced text!

- 👟 ctrl-o ctrl-i - go back and forward between your recent movement 'jumps'
- 🌧 V ctrl-v - line-wise and column-wise visual selection modes

## Optimisations
- 👟 t/T{character} - move forward/back to just before the next instance of the
	character (equivalent to f{char}◀ or F{char}▶)
- 💥 r{character} - replace character under the cursor, without going into insert
	mode
- 🌧 a - enter insert mode after the current cursor (equivalent to `li`)
- 🌧 I - enter insert mode at the start of the line (after indentation)
	(equivalent to `^i`). Works great with '.'
- 🌧 A - enter insert mode at the start of the line (after indentation)
	(equivalent to `$a`). Works great with '.')
- 👟 `* #` - search for word under cursor


## Advanced
- 💥 gu - make lowercase
- 💥 gU - make uppercase
- 💥 J - join next line
- 🦚 zt zb zz - move _viewport_ so the current line is the top/bottom/middle line

## Advanced // Record/retrieve
- 🦚 q{letter} - record macro
- 💥 @{letter} - record macro
- 🦚 m{letter} - set location bookmark in file
- 👟 '{letter} - move to location bookmark

## Advanced // Obscure
- 💥 !{shell-command} - run lines as input to given shell command, and replace
	them with the command output.
- 💥 gq -- split long lines
- 📣 :g/{match}/{command} - on every line with {match}, perform {action}
- 📣 :v/{match}/{command} - on every line _without_ {match}, perform {action}

## Less Useful
- 👟 H L M - move cursor to the top/bottom/middle line (mnemonic: high/low/middle)

# Appendices

## Appendix A: additional vimrc recommendations
```vim
set scrolloff=7 # leave 7 lines of extra space above/below the maximum cursor height

# Decent font options
if has ('gui_running')
	if s:MSWindows
		set guifont=Consolas\ 14
	elseif has("gui_photon")
		set guifont=Courier\ New:s12
	elseif has("gui_kde")
		set guifont=Courier\ New/12/-1/5/50/0/0/0/1/0
	elseif has("x11")
		set guifont=-*-courier-medium-r-normal-*-*-180-*-*-m-*-*
	else
		set guifont=Courier_New:h12:cDEFAULT
	endif
endif
```

## Appendix B: Other resources
