# Vim Cheatsheet

> Disclaimer: This cheatsheet is summarized from personal experience and online tutorials. It is not official Vim documentation.

## Contents

- [Notation](#notation)
- [Beginner essentials](#beginner-essentials)
- [Global commands](#global-commands)
- [Cursor movement](#cursor-movement)
- [Insert mode](#insert-mode)
- [Vim grammar](#vim-grammar)
- [Editing](#editing)
- [Visual mode](#visual-mode)
- [Text objects](#text-objects)
- [Yank, delete, and paste](#yank-delete-and-paste)
- [Search and replace](#search-and-replace)
- [Search in multiple files](#search-in-multiple-files)
- [Marks, jumps, and macros](#marks-jumps-and-macros)
- [Exiting](#exiting)
- [Buffers and windows](#buffers-and-windows)
- [Tabs](#tabs)

## Notation

```text
<C-r>    # hold Ctrl and press r
<Esc>    # press Escape
{motion} # a movement command, such as w, $, or }
```

## Beginner essentials

```text
i        # enter insert mode before the cursor
<Esc>    # return to normal mode
:w       # save
:q       # quit
:wq      # save and quit
h j k l  # move left, down, up, right
w        # jump to the start of the next word
b        # jump to the start of the previous word
0        # jump to the start of the line
$        # jump to the end of the line
gg       # go to the first line
G        # go to the last line
/pattern # search forward
n        # repeat the last search
u        # undo
<C-r>    # redo
dd       # delete the current line
yy       # yank (copy) the current line
p        # paste after the cursor
.        # repeat the last change
```

## Global commands

```text
:help keyword  # open help for keyword
:edit file     # open file in the current buffer
:saveas file   # save file as
:close         # close current window
```

## Cursor movement

```text
h        # move cursor left
j        # move cursor down
k        # move cursor up
l        # move cursor right
H        # move to top of screen
M        # move to middle of screen
L        # move to bottom of screen
w        # jump forward to the start of a word
W        # jump forward to the start of a WORD (space-separated)
e        # jump forward to the end of a word
E        # jump forward to the end of a WORD (space-separated)
b        # jump backward to the start of a word
B        # jump backward to the start of a WORD (space-separated)
0        # jump to the start of the line
^        # jump to the first non-blank character of the line
$        # jump to the end of the line
g_       # jump to the last non-blank character of the line
gg       # go to the first line of the document
G        # go to the last line of the document
5G       # go to line 5
fx       # jump to next occurrence of character x
Fx       # jump to previous occurrence of character x
tx       # jump to before next occurrence of character x
Tx       # jump to after previous occurrence of character x
;        # repeat latest f, F, t, or T motion
,        # repeat latest f, F, t, or T motion in the opposite direction
}        # jump to next paragraph or block
{        # jump to previous paragraph or block
zz       # center cursor on screen
<C-b>    # move back one full screen
<C-f>    # move forward one full screen
<C-d>    # move forward 1/2 screen
<C-u>    # move back 1/2 screen
```

## Insert mode

```text
i        # insert before the cursor
I        # insert at the beginning of the line
a        # append after the cursor
A        # append at the end of the line
o        # open a new line below the current line
O        # open a new line above the current line
ea       # append at the end of the word
<Esc>    # exit insert mode
```

## Vim grammar

Most normal-mode editing commands follow this shape:

```text
{count}{operator}{motion}
```

```text
3w       # move forward 3 words
5j       # move down 5 lines
2dd      # delete 2 lines
daw      # delete a word
ci"      # change inside double quotes
y$       # yank to the end of the line
gg=G     # auto-indent the whole file
```

Common operators:

```text
d        # delete
c        # change
y        # yank
>        # indent right
<        # indent left
=        # auto-indent
g~       # swap case
gu       # make lowercase
gU       # make uppercase
```

## Editing

```text
r        # replace a single character
R        # replace characters until <Esc>
J        # join line below to the current one
cc       # change entire line
cw       # change to the end of the current word
ce       # change to the end of the current word
cb       # change back to the start of the current word
c0       # change to the start of the line
c$       # change to the end of the line
s        # delete character and substitute text
S        # delete line and substitute text (same as cc)
xp       # transpose two letters
>>       # indent current line right
<<       # indent current line left
==       # auto-indent current line
.        # repeat last change
u        # undo
<C-r>    # redo
```

## Visual mode

```text
v        # start characterwise visual mode
V        # start linewise visual mode
<C-v>    # start blockwise visual mode
o        # move to other end of marked area
O        # move to other corner of block
>        # shift selection right
<        # shift selection left
y        # yank selection
d        # delete selection
~        # switch case
<Esc>    # exit visual mode
```

## Text objects

Text objects are usually used after an operator, such as `d`, `c`, or `y`.

```text
iw       # inner word
aw       # a word, including surrounding whitespace
is       # inner sentence
as       # a sentence
ip       # inner paragraph
ap       # a paragraph
i"       # inside double quotes
a"       # around double quotes
i'       # inside single quotes
a'       # around single quotes
i`       # inside backticks
a`       # around backticks
ib       # inside parentheses
ab       # around parentheses
iB       # inside braces
aB       # around braces
it       # inside an HTML/XML tag
at       # around an HTML/XML tag
```

Examples:

```text
ciw      # change inner word
daw      # delete a word
yi"      # yank inside double quotes
da)      # delete around parentheses
```

## Yank, delete, and paste

```text
yy       # yank current line
2yy      # yank 2 lines
yw       # yank from cursor to the start of the next word
y$       # yank to end of line
p        # paste after cursor or below current line
P        # paste before cursor or above current line
dd       # delete current line
2dd      # delete 2 lines
dw       # delete from cursor to the start of the next word
D        # delete to the end of the line
d$       # delete to the end of the line
d^       # delete to the first non-blank character of the line
d0       # delete to the beginning of the line
x        # delete character under the cursor
X        # delete character before the cursor
```

Registers:

```text
"ayy     # yank current line into register a
"ap      # paste from register a
"+y      # yank selection to the system clipboard, when available
"+p      # paste from the system clipboard, when available
:reg     # show registers
```

## Search and replace

```text
/pattern       # search forward for pattern
?pattern       # search backward for pattern
\vpattern      # very magic pattern: fewer regex characters need escaping
n              # repeat search in same direction
N              # repeat search in opposite direction
*              # search forward for word under cursor
#              # search backward for word under cursor
gn             # visually select next search match
:%s/old/new/g  # replace all old with new throughout file
:%s/old/new/gc # replace all old with new throughout file with confirmations
:noh           # remove highlighting of search matches
:set ignorecase smartcase # ignore case unless the pattern contains uppercase
```

## Search in multiple files

```text
:vimgrep /pattern/ **/* # search for pattern in files under the current directory
:cn                    # jump to the next match
:cp                    # jump to the previous match
:copen                 # open the quickfix list
:cclose                # close the quickfix list
```

## Marks, jumps, and macros

```text
ma       # set mark a at the cursor
`a       # jump to exact position of mark a
'a       # jump to the first non-blank character on mark a's line
''       # jump back to the previous line
<C-o>    # jump to older cursor position
<C-i>    # jump to newer cursor position
qa       # start recording macro into register a
q        # stop recording macro
@a       # play macro in register a
@@       # replay the last macro
```

## Exiting

```text
:w              # write (save) the file, but do not exit
:w !sudo tee %  # write the current file using sudo
:wq             # write and quit
:x              # write and quit if the file changed
ZZ              # write and quit
:q              # quit (fails if there are unsaved changes)
:q!             # quit and discard unsaved changes
ZQ              # quit and discard unsaved changes
```

## Buffers and windows

```text
:edit file  # edit a file in the current buffer
:bnext      # go to the next buffer
:bn         # go to the next buffer
:bprev      # go to the previous buffer
:bp         # go to the previous buffer
:bd         # delete a buffer
:ls         # list open buffers
:sp file    # open file in a horizontal split
:vsp file   # open file in a vertical split
<C-w>s      # split window horizontally
<C-w>v      # split window vertically
<C-w>w      # switch windows
<C-w>q      # quit a window
<C-w>h      # move cursor to the left window
<C-w>l      # move cursor to the right window
<C-w>j      # move cursor to the window below
<C-w>k      # move cursor to the window above
```

## Tabs

```text
:tabnew              # open a new tab
:tabnew file         # open a file in a new tab
<C-w>T               # move the current split window into its own tab
gt                   # move to the next tab
:tabnext             # move to the next tab
:tabn                # move to the next tab
gT                   # move to the previous tab
:tabprev             # move to the previous tab
:tabp                # move to the previous tab
{number}gt           # move to tab {number}
:tabmove {number}    # move current tab to position {number}, indexed from 0
:tabclose            # close the current tab
:tabc                # close the current tab
:tabonly             # close all tabs except the current one
:tabo                # close all tabs except the current one
:tabdo command       # run command on all tabs, such as :tabdo q
```
