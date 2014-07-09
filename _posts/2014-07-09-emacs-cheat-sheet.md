---
layout: post
title: "GNU Emacs Cheat Sheet"
description: "Quick reference"
category: Computer Science
tags: ['Editor', 'Emacs']
---
{% include JB/setup %}

{% highlight java %}
Pick up the old tradition. Written in 2012 Summer. 
{% endhighlight %}

### ACTION  
c-v  
m-v view  
c-l clear  
  
c-p c-n (previous, next)  
c-b c-f (backward, forward)  
m-f m-b  
  
META defined unit  
CONTROL independent unit  
  
c-a c-e beginning ending  
m-a m-e  
  
** m-\< m-\> (shift) (beginning of a file, end of a file)  
  
c-u 8 c-f (prefix argument)  (not supported in PyCharm Emacs mode)  
Emacs and terminal are intercommunicated  
  
m-x shell (open the cmd inside the emacs) m-x (in PyCharm, like c-k, but will also delete \n)  
  
c-g give up the operation (disreagard)  
  
### KILL DELETING YANKING  
c-x 1 (digit 1)  kill all other windows   
//c-x series of cmd from the c-x; many of them have to do with windows, files, buffers, and related things.  
\<backspace\> c-d (character delete) (opp. delete)  
m-\<backspace\> m-d word  
c-k m-k kill the line/sentence from the cursor  
  
c-\<space\> (mark set)  
c-w like always: "kill"  
  
kill != del (kill is like cut)  
c-y yanking (can yanke multiple lines) (can combine with Market Set)  
m-y yanking history (change the yanking history)  
  
m-w COPYING  
c-y 	pasting  
  
m-shit-% replace query  
  
### UNDO  
c-x u  
c-_ (shift) (c-shift-'-')  
  
### FILE  
c-x c-f find the file (bottom screen)  
c-x c-s save the file (specify the path and name)  
  
### BUFFERS  
multiple files in buffers  
c-x c-f  
c-x c-b list the buffers  
c-x 1 make only one buffer   
c-x b (switch buffer)  
c-x s (save the buffers into files) (auto detect the changes)  
  
### EXTENDING the command set  
c-x c-c (terminate the emacs) (when log out)  
c-z (suspend emacs and return Terminal fg or %emacs to come back) (when turn to another thing)  
  
REPLACE  
m-x repl s\<Return\>Changed\<Return\>altered\<Return\> (REPLACE) (auto fill)  
  
AUTO SAVE: find the unfinished file and m-x recover-file \<Return\>  

### ECHO AREA  
m-x text-mode (Switch to the text mode)  
c-h m (see the mode info)  
  
### MODE  
major mode/minor mode  
m-x auto-fill-mode (for human-langugage test)  
c-u 20 c-x f (set the column number) (useful in auto-fill-mode)  
m-q (refill the paragraph)  
  
### SEARCH  
c-s (forward search)("incremental" search) \<after, c-s for the next, \<Delback\> for the previous\>  
c-r (reversed search)  
Control: c-s \<Delback\> c-r  
  
put blanks: . one character, .* string (a slice of character)  
  
### WINDOWS  
c-u 0 c-l (mark)  
c-x 2(split into 2)  
c-m-v to scroll the bottom window)  
c-x o (o for ohter, change position of the cursor to another buffer)  
  
c-x 1 c-x 2 (horizontally) c-x 3(vertically)  
c-x 0 (kill this window and go to another window)  
  
c-x 4 c-f open another file and create an another window  
  
c-x k (PyCharm, like c-w in windows)  

### FRAMES  
m-x make-frame  
m-x delete-frame (shortcut: c-x 5 0)  
  
### Recursive level  
type \<ESC\> \<ESC\> \<ESC\> to get out of a recursive editiong level  
c-g cannot, since c-g for within the recursive editiong level.  
  
### HELP  
c-h for help  
c-h ?  
c-h c c-p (brief)  
c-h k c-p (thorough discribtion of the cmd)  
  
c-h f (describe a function)  
c-h a file (for Apropos cmd)  
c-h i (info)  