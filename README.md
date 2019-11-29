# happyVIIIM
vim cheatsheet XD

## Delete all lines containing pattern

```
:g/pattern/d
```

Delete all lines that are empty

```
:g/^$/d
```

Delete all lines that are empty or contain only whitespace:

```
:g/^\s*$/d
```

Delete all lines that do **not** contain a pattern `g!` (equivalent to `v`)

```
:g!/^\s*$/d
```

or

```
:v/^\s*$/d
```

Using `\|` as or: Delete all lines except those contain "error", "warn" or "fail"

```
:v/error\|warn\|fail/d
```

## Counting occurrences of a pattern

```
:%s/pattern/gn
```


## Replace space with newline

```
:%s/ /<Ctrl v><Enter>/g
```

## Search

`*`to search for the current word under cursor

`[I` to list all occurrences of word under the cursor (same as `:g/`


for complex search use

```
:g/pattern
```
or
```
:il pattern
```

search "pattern" and open a clickable list

```
:w
;vimgrep /pattern/ %
:copen
```

## Copy or delete matching lines

```
qaq
:g/pattern/y A
:let @+ = @a
```

The first of the following commands deletes all lines containing *pattern*, while the second deletes all lines matching the last search:

```
:g/pattern/d
:g//d
```

Use `:v//d` to delete all lines that do *not* match the last search pattern, or `:v/pattern/d` to delete all lines that do *not* match the given pattern.

## Insert line numbers before each line

```
:%s/^/\=printf('%-4d', line('.'))
```

## Insert something before or after each line

```
gg<Ctrl v>G0A<something><Esc>
gg<Ctrl v>G$A<something><Esc>
```

## Record and execute from file
write all keystrokes in `test.keys`
```
vim -s test.keys myInput.file
```

| magics for saving | and reading and etc. |
| ----------------------------- | --------------------------------------------------- |
| :w >>foo                      | append the whole buffer to a file                   |
| :.w >>foo                     | append current line to a file                       |
| :$r foo                       | read foo into the end of the buffer                 |
| :0r foo                       | read foo into the start, moving existing lines down |
| :.,$w foo                     | write current line and below to a file              |
| :r !ls                        | read ls output into cursor position                 |
| :w !wc                        | send buffer to wc and display output                |
| :.!tr ‘A-Za-z’ ‘N-ZA-Mn-za-m’ | apply ROT-13 to current line                        |
| :w\|so %                      | chain commands: write and then source buffer        |
| :e!                           | throw away unsaved changes, reload buffer           |
| :hide edit foo                | edit foo, hide current buffer if dirty              |

# Sorting columns of text

```
:%!column -t
:%!sort -k2nr    column 2 asnumber reverse
:%!sort -k4 -bk3g    sort by the the 4th column (-k4), followed by the 3rd column, but this time we require a few more switches. We ignore leading blank spaces (b), and this time we sort using a general numeric sort (g).
```
