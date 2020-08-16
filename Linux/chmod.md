---
title: file permissions
description: Explanation of basic file and directory permissions in Linux, as well as chmod usage
published: true
date: 2020-08-16T18:14:50.481Z
tags: linux
editor: markdown
---

When listing a directory with `ls -l`, the file mode of each file and directory is shown in a symbolic format such as `-rwxr-xr--`.

This 10-character code is made up of four parts:
|||
|-|-|
**File type**|may be `-` for file, `d` for directory, or `l` for symbolic link.
**User permission** | Applies to assigned user owner of the file.
**Group permission** | Applies to the file's assigned [group](/Linux/groups).
**Other permission** | Applies to all other users. Sometimes referred to as "world" permission.

<img src="/assets/classes.png.webp" style="filter: invert(.8); padding: 32px" />

An `s` in the group permission class of a directory indicates that new files in that folder will explicitly inherit its group permissions. See [using setgid](/Linux/groups#using-setgid). File permissions in Linux are technically stored in 4 sets, but the special modes set will not be covered in this page.

# Permissions formats
Each of the 3 permission classes is stored in 3 bits. Permission values can be represented in octal (numeric), binary, or symbolic format. 

For example, a file which is read/write/execute for the user owner, read/execute for itd group, and read-only all other users, can be represented the following ways:

<br>
<pre style="background-color: #181818; width: 35%">
  symbolic   - rwx r-x r--
  binary       111 101 100
  numeric       7   5   4
</pre>
<br>

## Permissions guides {.tabset}
### Permissions table

Below is a list of all possible permission set values in each format:
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

### Binary-octal conversion
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

# chmod usage
`chmod` is the Linux command used to change file and directory permissions. It can be used either with numeric or symbolic mode.  For the examples below, we will imagine starting with the following read-only file (numeric permission value = 444):
<br>
<pre>
  -r--r--r-- file.txt
</pre>

## numeric mode
Numeric mode works with the octal value as described above, and modifies an entire permission set:
||command|result|
-|-|-
Set to full control for user, read/execute for group, and read-only for other|`chmod 754 file.txt`|<pre>-rwxr-xr-- file.txt</pre>
Set to read-only for user and group, and no access for other|`chmod 440 file.txt`|<pre>-r--r----- file.txt</pre>

## symbolic mode
With symbolic mode, you can modify individual parts of the permission set using symbolic representation.
`all` is implied if no other permission class is specified, therefore can be omitted.

<img src="/assets/chmod.png" style="filter: invert(.9); padding: 32px 0 16px 16px" />

Examples:
|                                                   | command                  | result
|-|-|-|
add execute permission for all                      |`chmod +x file.txt`       |<pre>-r-xr-xr-x file.txt</pre>
add write permission for user owner                 |`chmod u+w file.txt`      |<pre>-rw-r--r-- file.txt</pre>
remove read permission for other users              |`chmod o-r file.txt`      |<pre>-r--r----- file.txt</pre>
add write/execute to user and group owners          |`chmod ug+wx file.txt`    |<pre>-rwxrwxr-- file.txt</pre>
add write to user and group, remove read from other |`chmod ug+w,o-r file.txt` |<pre>-rw-rw---- file.txt</pre>
set write-only to group and other                   |`chmod go=w file.txt`     |<pre>-r---w--w- file.txt</pre>

## directory usage
Modifying directory permissions works much in the same way as files. Below are a couple examples given the following directory:
<br>
<pre>
  dr--r--r-- directory
</pre>
| command                 | result
|-|-|
`chmod 754 directory`     |<pre>drwxr-xr-- directory</pre>
`chmod u+w,ug+x directory`|<pre>drwxr-xr-- directory</pre>

To change permissions of all files and subfolders within a directory, use the `-R` recursive flag:
`chmod -R u+wx directory`

## verbose flag
The `-v` flag can be used to explicitly print out the resulting changes from a chmod command.
```shell-session
$ chmod -v ug+wx file.txt
mode of 'file.txt' changed from 0444 (r--r--r--) to 0774 (rwxrwxr--)
```

# References
[An Introduction to Linux File Permissions - Boolean World](https://www.booleanworld.com/introduction-linux-file-permissions/)