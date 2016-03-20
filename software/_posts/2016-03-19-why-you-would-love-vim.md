---
title: "Why you would love vim"
ref: why-you-would-love-vim
layout: post
lang: en
---

Hello again! Today i want to talk about **Vim** and why i literally can't write code without him in IDE.
I'll try to not teach you how to use Vim, but i'll try to give you my opinion about Vim and show you the benefits of using him
, show that Vim has no disadvantages :open_mouth:

#### Why you would read this article?  
  To learn why Vim is so cool. Learning it you will:

  * write code faster, that's it. Simple :) But only if you dare to learn it.  
  * forget about mouse, arrow-keys and about Numpad, because vim requires your hands only at "home-row" (asdf + jkl;)  

#### About Vim for me in general
  Vim is just a convenient text-editor with a lot of(sure a lot) commands, which you can force to execute repeatedly.
  And when you will get used to Vim, you would want to use it everywhere, it's true, i swear  
  I am using it quite for a bit - 3 months, but every time i help somebody with code on different machine, i miss him hard :flushed:  
  Because of Vim's comfortableness, ~~Seriously, i have an addiction~~, you can use it everywhere: In most popular IDEs, in terminal, even in your browser :smile:

  I love Vim for 2 things: static hands layout and strong(really strong) engine for access to every place in text symbol!     

#### A bit mechanics to begin with
  Vim has 4 modes:

  * **normal mode** - mode for cursor movement in common, also for deletion, replacement, pasting, and undo
  * **Insert mode** - mode for inserting text, haha ~~It's kinda only mode for casual mortal text-editors~~
  * **Command-line mode** - mode for executing special commands like saving changes, closing file, finding things and etc.
  * **Visual mode** - mode for highlighting

  Cursor movement is available in normal mode with `h(left) j(down) k(up) l(right)`   
  You can exit to normal mode from every other by pressing `esc`

  By the way, you can remember hjkl with:

  * h - the most left key
  * j - look at symbol. It's like a down-arrow ~~psycho~~
  * l - the most right
  * k - residuary

#### What you can do in Vim
  * Move cursor for a single word `w(word)`,  
    for 3 words forward `3 - w(word)`,  
    for 42 words backwards `42 - b(backwards)`  

  * Move cursor for 4 lines up `4 - k(up)`,  
    delete 8 lines below just for 3 key presses `d(delete) - 8 - j(вниз)`,  
    delete 3 words `3 - w(word)`
    delete 2 chars `2 - x(extract)`

  * Move cursor for the next paragraph `}`,  
    for the next function's bracket(whatever bracket, really) `%`,  
    delete all inside brackets `d(delete) - %`

  * Move cursor to the beginning of the line `(0)`,  
    to the beginning of the text `(^)`,  
    to the end of the line `($)`,  
    delete/change every symbols from current position to the beginning of the text `d(delete)\c(change) + ^`

  * Replace one symbol `r(replace) - a/b/1/./...`

  * Move cursor to the top of the screen `H(high)`  
    to the middle `M(middle)`  
    to the bottom `L(low)`

  * You can jump to the symbol 'x'(or whatever different) in line `f(find) - x`,    
    delete text from current position to the symbol ';' `d(delete) - f(find) - ;`

  * Deletion on Vim is a "cut" operation, and pasting is executed from the next symbol. That's why delete + paste a char means swap  
  ```bash
  $ gcc --verison // esc(to the normal mode) - 0(to beginning of the line) - f(find) i - x(extract) - p(paste)  
  $ gcc --version // As it should be!
  ```

  * Also Vim supports all mere text-editor functions like open file, close file, undo action, re-undo and etc.

#### How to begin with Vim
  ```bash
  $ sudo apt-get install vim  
  $ vimtutor
  ```  

  The best way in my opinion is vimtutor, which is supplied with Vim itself. It's interactive tutorial for 20-30 minutes, which will ask you to fix typos as it continues. I really liked it :smile: Also, it's only my passion to have cheat-sheets for everything. So, just find "Vim cheat sheet" or yourself and peek in it from time to time.

  It's really handy to set relative line numbers in vim, so you can count easily.

#### How to get to full potential
  0. Remember, you can do everything(!) in Vim. It's because it was written for you, my friend :smile:
  1. When writing code, just wonder, it will be good to have {feature-name} in Vim
  2. Profit. Look up for the 0 point and google it

#### Afterwords
  Well, i do hope that there is not a lot of water in article :smile: I hope, that i gave you the basics in Vim and intrigued you.  
  My next post will be about Java programming in Web

  See you :smile: And stay awesome, my reader! :wink:
