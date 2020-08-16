---
title: chmod
description: 
published: true
date: 2020-08-16T16:47:09.307Z
tags: linux
editor: markdown
---

`chmod` is a Linux shell command that allows you to modify the permissions of a file or directory.

## File permission explanation

When listing a directory with `ls -l`, the file mode of each file and directory is shown in a symbolic format such as `-rwxr-xr--`.

This 10-character code is made up of four parts:
|||
|-|-|
**File type**|may be `-` for file, `d` for directory, or `l` for symbolic link.
**User permission** | Applies to assigned user owner of the file.
**Group permission** | Applies to the file's assigned [group](/Linux/groups).
**Other permission** | Applies to all other users. Sometimes referred to as "world" permission.

<img src="/assets/classes.png.webp" style="filter: invert(.8)" />

An `s` in the group permission class of a directory indicates that new files in that folder will explicitly inherit its group permissions. See [using setgid](/Linux/groups#using-setgid).

### Permissions guides {.tabset}
#### Permissions table
Each of the nine total permissions is stored as a single bit. A permission class is 3 bits. Permission values can be represented in octal (numeric), binary, or symbolic format:
<br>
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

#### Binary-octal conversion
![binary_counter_3digits.gif](/assets/binary_counter_3digits.gif)

If you can't count in binary, here's an easy trick for converting binary to numeric. Multiply each bit by its numeric place value (4-2-1), then sum the resulting numbers. For example:
<pre style="font-size: 1.25em; background-color: #181818; width: 50%">
<span style="color: #777"> r w x      r - x      r - -</span>
 1 1 1      1 0 1      1 0 0
 4 2 1      4 2 1      4 2 1
 - - -      - - -      - - -
 4+2+1      4+0+1      4+0+0
  = 7        = 5        = 4
</pre>

## chmod usage
`chmod` can be used either with numeric or symbolic mode.  For the examples below, we will imagine starting with the following read-only file:
<br>
<pre>
  -r--r--r-- file.txt
</pre>

### numeric mode
Numeric mode works with the octal value as described above, and modifies an entire permission set:
||command|result|
|-|-|-|
|Change to full control for user, read/execute for group, and read-only for other|`chmod 754 file.txt`|<pre>-rwxr-xr-- file.txt</pre>|

### symbolic mode
With symbolic mode, you can modify individual parts of the permission set using symbolic representation.

<img src="/assets/chmod.png" style="filter: invert(.8)" />



||command|result|
|-|-|-|
add execute permission for all|`chmod +x file.txt`|<pre>-r-xr-xr-x file.txt</pre>
add write permission for user owner|`chmod u+w file.txt`|<pre>-rw-r--r-- file.txt</pre>
remove read permission for other users|`chmod o-r file.txt`|<pre>-r--r----- file.txt</pre>
add write/execute to user and group owners|`chmod ug+wx file.txt`|<pre>-rwxrwxr-- file.txt</pre>
add 

<pre>
<code>chmod +x file.txt</code>  ==>  -r-xr-xr-x file.txt
<code>chmod u+w file.txt</code> ==>  -rw-r--r-- file.txt
</pre>

