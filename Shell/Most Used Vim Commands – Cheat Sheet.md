
### Navigation

|Command|Description|
|---|---|
|`h` / `l`|Move left / right|
|`j` / `k`|Move down / up|
|`w`|Move to next word|
|`b`|Move to previous word|
|`0`|Start of line|
|`^`|First non-blank character of line|
|`$`|End of line|
|`gg`|Start of file|
|`G`|End of file|
|`:n`|Go to line number `n`|

---

### Editing

|Command|Description|
|---|---|
|`i`|Insert before cursor|
|`I`|Insert at beginning of line|
|`a`|Append after cursor|
|`A`|Append at end of line|
|`o`|Open new line below|
|`O`|Open new line above|
|`r`|Replace one character|
|`R`|Replace multiple characters (overtype)|
|`x`|Delete character under cursor|
|`s`|Delete character and insert|

---

### Copy & Paste

|Command|Description|
|---|---|
|`yy`|Yank (copy) current line|
|`2yy`|Yank two lines|
|`yw`|Yank one word|
|`y$`|Yank to end of line|
|`p`|Paste after cursor|
|`P`|Paste before cursor|
|`"+y`|Yank to system clipboard|
|`"+p`|Paste from system clipboard|

---

### Deleting

|Command|Description|
|---|---|
|`dd`|Delete current line|
|`2dd`|Delete 2 lines|
|`dw`|Delete a word|
|`d$`|Delete to end of line|
|`dG`|Delete to end of file|

---

### Undo / Redo

|Command|Description|
|---|---|
|`u`|Undo last change|
|`U`|Undo all changes on current line|
|`Ctrl + r`|Redo last undo|

---

### Search

|Command|Description|
|---|---|
|`/word`|Search **forward** for "word"|
|`?word`|Search **backward** for "word"|
|`n`|Repeat last search (same direction)|
|`N`|Repeat last search (opposite)|

---

### Visual Mode

|Command|Description|
|---|---|
|`v`|Start visual mode (character-wise)|
|`V`|Start linewise visual mode|
|`Ctrl + v`|Start blockwise visual mode|
|`y`|Yank selection|
|`d`|Delete selection|
|`>` / `<`|Indent / unindent|

---

### File Operations

|Command|Description|
|---|---|
|`:w`|Save|
|`:q`|Quit|
|`:wq`|Save and quit|
|`:q!`|Quit without saving|
|`:e filename`|Open a file|
|`:ls`|List open buffers|
|`:bn` / `:bp`|Next / previous buffer|