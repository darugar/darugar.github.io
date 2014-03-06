---
layout: parand
title:  "How To Enable Vi Syntax Highlighting In Ubuntu"
date:   2009-10-28 10:00:00
categories: say/index.php
---
Note to self, as I seem to need to do this on every new install:

Ubuntu ships with vim-tiny, which doesn't support syntax highlighting. Do this:
    
    
    sudo apt-get remove vim-tiny
    sudo apt-get install vim
    sudo vi /etc/vim/vimrc
    ( Remove the quote mark from the "syntax on" line, uncommenting it)
    
