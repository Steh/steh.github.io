---
title: "My little VIM guide"
categories: 
- informationsecurity
tags:
- VIM
- Linux
classes: 
- wide
excerpt: "A little Guide to the open source text editor VIM (VI Improved)"
toc: true
toc_icon: "cog"
--- 

### Using tabs

```bash
#open tab
:tabnew

## switch tab
:tabn   ### next
:tabp   ### previuos
gt      ## switch forward
gT      ## switch backwards

#open file 
e: folder
e: file
```

### navigation

```bash
h (left)       j (down)       k (up)       l (right)

0   -   beginning of line
$   -   end of line
w   -   imove to the start of the next word
e   -   move to the end of the word
b   -   nove to the beginn of the word

2e  -   move two words forward 
3w  -   move three words forward   
gg  -   move to the top of the file
G   -   move to the bottom of the file
502G    -   go to line 502
```

### editing

```bash
i   -   insert ON the curser
a   -   insert AFTER the curser
A   -   append AFTER the line
o   -   insert on the line before
O   -   insert on the next the line

x   -   remove character
u   -   undo
r   -   redo

## delete text
dw  -   delete word
de  -   delete until end of the word
d$  -   delete until end of line
d2w -   delete the next two words

dd  -   deltes line and stores it in register
p   -   insert deleted line on curser

## replace text
r[char] -   replace the letter with the char
R       -   replace the following chars 

## change text
ce  -   deletes the word and places you in Insert mode
cc  -   does the same for the whole line
c2w -   deletes the next to words and places you in Insert mode
c$  -   deletes until line end and places you in Insert mode
```

## copy/paste

```bash
## copy/past
dd  -   cut the line
3dd -   cut three lines
yy  -   copy 1 line
3yy -   copy 3 lines
p   -   paste

## visual copy/paste
v   -   mark the text
y   -   copy text (yank)
p   -   paste the text (put)

## past from systemclipboard
"+p - paste from system
```

## search

```bash
## search
/   -   search for a phrase (after hitting enter)
n   -   show next appearance
N   -   show previous appearance
%   -   moves the cursor to the next matching bracket ( (,),[,],{ or } )

*   -   find the next occurence of the word under the curser
##   -   find the last occurence of the word under the curser

## search and replace
:s/old/new/g    -   replaces the first occourance of old with new in the line
:#,#s/old/new/g    where #,## are the line numbers of the range of lines where the substitution is to be done.
:%s/old/new/g      to change every occurrence in the whole file.
:%s/old/new/gc     to find every occurrence in the whole file, with a prompt whether to substitute or not.
```

## Execute commands

```bash
## execute external comands
:!ls    -   list files
:sh     -   starts a shell (exit gets you back)

## Retrieving files
:r FILE -   writes the file content above the curser
:r !ls  -   writes the output to the file

## Selecting text to write
:w TEXT -   writes that text to a file  
```

## using vim help

```bash
## using the help windows
F1  -   open help
:help
CTRL+W  -   jump between windows
:q      -   close help
```

## set default config

```bash
# vim /etc/vim/vimrc

" Set tabs to have 4 spaces
 set tabstop=4
 set shiftwidth=4
 set expandtab
 
 " Set line numbers
 set number
 
" Set incremental search
set incsearch

" Highlight search results
set hlsearch

" Enable command line completion
set wildmenu

" Allow backspacing over everything in insert mode
set backspace=indent,eol,start

" Open new lines with the same indentation
set autoindent

" Show matching brackets and parentheses
set showmatch

" Faster keyword completion menu appearance
set completeopt=menu,menuone,noselect

" Wrap lines at convenient points
set linebreak

" Set encoding to UTF-8
set encoding=utf-8

" Disable visual bell (no flashing)
set visualbell
set t_vb=

" Enable file type detection and plugins based on file type
filetype plugin on
filetype indent on
```

## references

* [linuxlinks.com: 8 Excellent Free Books to Learn Vim](https://www.linuxlinks.com/excellent-free-books-learn-vim/)
* [VIM User Manual by Bram Moolenaar](https://www.eandem.co.uk/mrw/vim/usr_doc/index.html)
* (vimtutor(1) - Linux man page)[https://linux.die.net/man/1/vimtutor]
* [How to Copy, Cut and Paste in Vim / Vi](https://linuxize.com/post/how-to-copy-cut-paste-in-vim)
* [neovim Teil 3 – Plugin Manager, umfangreiche Einstellungen und Erweiterungen](https://schimana.net/2021/neovim-teil-3-plugin-manager-umfangreiche-einstellungen-und-erweiterungen/)
* [Vim tips: Working with external commands](https://www.linux.com/training-tutorials/vim-tips-working-external-commands/)
* [VIM Tutorial](https://www.openvim.com/tutorial.html)
