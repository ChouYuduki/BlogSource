+++
date = '2024-11-19'
title = 'Basic Operation of Vim'
author = 'Saka'
description = "Some Operation of Vim"
categories = [
    "Linux"
]
tags = [
    "Vim",
    "Tutorial"
]
+++

here is some basic operation of vim:

```Shell

# delete left 1 char
d j

# delete left 3 char
d 3 j  

# delete right 1 char 
d l     

# delete right 3 char
d 3 l  

# cut the whole line
d d     

# copy the whole line
y y     
 
# paste
p       

# undo the last change
u       

# go to the next word
w       

# back to last word
b

# delete next word and into insert mode
# (which means you can change the word directly)
c w     

# change the content in "" or <> or whatever
# h, which means in  
c h "
c h <>

# redo the undo change             
<ctrl> + r 

# find something
f

# find a letter
f [letter you want to find]

# delete until =  
d f =

 
0   # go to start of the line
A   # goto end and insert
```
