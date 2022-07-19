# Learn Vim

## macro

| q+char    | start recording | save to character |
| --------- | --------------- | ----------------- |
| recording |                 |                   |
| q         | end recording   |                   |
| @+char    | replay          |                   |

## Basic

| basic |                    |
| ----- | ------------------ |
| :q    | exit               |
| :wq   | save exit          |
| u     | undo               |
| \<c-r\> | redo               |
| .     | repeat last change |

## Navigate

### Character Navigation

| by character |       |
| ------------ | ----- |
| h            | left  |
| j            | down  |
| k            | up    |
| l            | right |

### Word Navigation

| by word |                         |
| ------- | ----------------------- |
| w       | next beginning word     |
| W       | next beginning Word     |
| e       | next ending word        |
| E       | next ending Word        |
| b       | backward beginning word |
| B       | backward beginning Word |
| ge      | backward ending word    |
| gE      | backward ending Word    |

### Inline Navigation

| inline |                            |
| ------ | -------------------------- |
| 0      | line start                 |
| $      | line end                   |
| ^      | first char                 |
| g_     | last char                  |
| f+char | search to char             |
| F+char | search back to char        |
| t+char | search to before char      |
| T+char | search back to before char |
| ;      | repeat search              |

### Paragraph Navigation

| by sentence |                    |
| ----------- | ------------------ |
| (           | previous sentence  |
| )           | next sentence      |
| {           | previous paragraph |
| }           | next paragraph     |

| to match |        |
| -------- | ------ |
| %        | {[()]} |

### Window Navigation

| by window |        |
| --------- | ------ |
| H         | top    |
| M         | middle |
| L         | bottom |

### Scroll

| scroll  |                              |
| ------- | ---------------------------- |
| \<c-D\> | down half screen             |
| \<c-F\> | down whole screen            |
| \<c-U\> | up half screen               |
| \<c-B\> | down whole screen            |
| zz      | bring current line to middle |

### Search

| search   |                                          |
| -------- | ---------------------------------------- |
| /        | search forward                           |
| ?        | search backward                          |
| n        | repeat last search                       |
| N        | repeat last search in opposite direction |
| *        | next word under cursor                   |
| #        | next word under cursor backward          |
| m + char | mark position with char                  |
| 'char    | jump to position marked with char        |
| gd       | to variable declaration                  |
| gi       | to implementation                        |

### Jump

| jump |                     |
| ---- | ------------------- |
| nG   | to line n           |
| \[\[ | to previous section |
| \]\] | to next section     |

## Insert Mode

| \<c-o\> | command submode |
| ------- | --------------- |

### To Insert Mode

| to insert |                          |
| --------- | ------------------------ |
| i         | insert before            |
| a         | append                   |
| I         | insert at line beginning |
| A         | append at line end       |
| o         | inset new line below     |
| O         | insert new line above    |
| s         | delete char and insert   |
| S         | delete line and insert   |

## Visual Mode

| to visual mode |                |
| -------------- | -------------- |
| v              | character-wise |
| V              | line-wise      |
| \<c-v\>        | block-wise     |

| navigate |        |
| -------- | ------ |
| o or O   | toggle |

## Edit

| delete |                         |
| ------ | ----------------------- |
| dd     | delete line             |
| D      | delete rest of the line |
| x      | delete cursor           |
| daw    | delete a word           |
| diw    | delete a word           |

| change     |                         |
| ---------- | ----------------------- |
| cc         | change line             |
| C          | change rest of the line |
| c-i-\[\{\( | change inside           |
| c-a-\[\{\( | change block            |
| r          | swap letter             |
| R          | swap letters            |
| ~          | swap cases              |
| gu         | to lower case           |
| gU         | to upper case           |

## Register

| register |                         |
| -------- | ----------------------- |
| "+char   | tell target of register |

`"ayy`: copy text in register "a"
`"ap` : paste text from register "a"

## g

| g           |                  |
| ----------- | ---------------- |
| gt          | to next tab      |
| gT          | to previous tab  |
| :action Run | run current file |
| gu          | to lower case    |
| gU          | to Upper case    |

## my favorite

|               |                                             |
| ------------- | ------------------------------------------- |
| d/words`<cr>` | delete to                                   |
| ==            | auto aline current line                     |
| ggvG=         | format file                                 |
| `<space>rc`   | format file                                 |
| cc            | change current line (move cursor to indent) |
| cgn           | search and replace                          |
|               |                                             |
