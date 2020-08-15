---
title: chmod
description: 
published: true
date: 2020-08-15T17:19:04.676Z
tags: linux
editor: markdown
---



## File permission explanation

When listing a directory with `ls -l`, the file mode of each file and directory is shown in a symbolic format:

<img src="/assets/classes.png.webp" style="filter: invert(.8)" />

File type may be `d` for directory, `-` for file, or `l` for symbolic link.

An `s` in the group permission class of a directory indicates that new files in that folder will explicitly inherit its group permissions. See [using setgid](/Linux/groups#using-setgid).

### Permissions guides {.tabset}
#### Permissions table
Each permission class can be represented in octal (numeric), binary, or symbolic format:
<br />
<pre style="font-size: 1.25em; background-color: #181818; width: 50%">
<span style="color: #5a9"> oct  bin    sym    description</span>
  0   000   - - -   no permissions
  1   001   - - x   execute only
  2   010   - w -   write only
  3   011   - w x   write and execute
  4   100   r - -   read only
  5   101   r - x   read and execute
  6   110   r w -   read and write
  7   111   r w x   full control
</pre>
<br />

<pre>

</pre>

#### octal conversion
<pre>
<span style="color: #777"> r w x      r - x      r - -</span>
 1 1 1      1 0 1      1 0 0
 4 2 1      4 2 1      4 2 1
 - - -      - - -      - - -
 4+2+1      4+0+1      4+0+0
  = 7        = 5        = 4
</pre>

## chmod usage
### numeric mode
### symbolic mode