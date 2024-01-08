---
icon: simple/vim
tags: [Updating]
comments: true
---

# Vim

1. [Link's vimrc](https://github.com/linkch0/vimrc)
2. [missing-semester](https://missing.csail.mit.edu/2020/editors/)
3. [missing-semester 中文](https://missing-semester-cn.github.io/2020/editors/)
4. [VimAwesome](https://vimawesome.com/)
5. [Vim Tips Wiki](https://vim.fandom.com/wiki/Vim_Tips_Wiki)
6. [Vim Cheat Sheet](https://vim.rtorr.com/)

## vimtutor 总结

### Lesson 1

```plaintext
  1. The cursor is moved using either the arrow keys or the hjkl keys.
         h (left)       j (down)       k (up)       l (right)

  2. To start Vim from the shell prompt type:  vim FILENAME <ENTER>

  3. To exit Vim type:     <ESC>   :q!   <ENTER>  to trash all changes.
             OR type:      <ESC>   :wq   <ENTER>  to save the changes.

  4. To delete the character at the cursor type:  x

  5. To insert or append text type:
         i   type inserted text   <ESC>         insert before the cursor
         A   type appended text   <ESC>         append after the line

NOTE: Pressing <ESC> will place you in Normal mode or will cancel
      an unwanted and partially completed command.
```

### Lesson 2

```plaintext
  1. To delete from the cursor up to the next word type:    dw
  2. To delete from the cursor to the end of a line type:    d$
  3. To delete a whole line type:    dd

  4. To repeat a motion prepend it with a number:   2w
  5. The format for a change command is:
               operator   [number]   motion
     where:
       operator - is what to do, such as  d  for delete
       [number] - is an optional count to repeat the motion
       motion   - moves over the text to operate on, such as  w (word),
                  $ (to the end of line), etc.

  6. To move to the start of the line use a zero:  0

  7. To undo previous actions, type:           u  (lowercase u)
     To undo all the changes on a line, type:  U  (capital U)
     To undo the undo's, type:                 CTRL-R
```

### Lesson 3

```plaintext
  1. To put back text that has just been deleted, type   p .  This puts the
     deleted text AFTER the cursor (if a line was deleted it will go on the
     line below the cursor).

  2. To replace the character under the cursor, type   r   and then the
     character you want to have there.

  3. The change operator allows you to change from the cursor to where the
     motion takes you.  eg. Type  ce  to change from the cursor to the end of
     the word,  c$  to change to the end of a line.

  4. The format for change is:

         c   [number]   motion
```

### Lesson 4

```plaintext
  1. CTRL-G  displays your location in the file and the file status.
             G  moves to the end of the file.
     number  G  moves to that line number.
            gg  moves to the first line.

  2. Typing  /  followed by a phrase searches FORWARD for the phrase.
     Typing  ?  followed by a phrase searches BACKWARD for the phrase.
     After a search type  n  to find the next occurrence in the same direction
     or  N  to search in the opposite direction.
     CTRL-O takes you back to older positions, CTRL-I to newer positions.

  3. Typing  %  while the cursor is on a (,),[,],{, or } goes to its match.

  4. To substitute new for the first old in a line type    :s/old/new
     To substitute new for all 'old's on a line type       :s/old/new/g
     To substitute phrases between two line #'s type       :#,#s/old/new/g
     To substitute all occurrences in the file type        :%s/old/new/g
     To ask for confirmation each time add 'c'             :%s/old/new/gc
```

### Lesson 5

```plaintext
  1.  :!command  executes an external command.

      Some useful examples are:
         (Windows)        (Unix)
          :!dir            :!ls            -  shows a directory listing.
          :!del FILENAME   :!rm FILENAME   -  removes file FILENAME.

  2.  :w FILENAME  writes the current Vim file to disk with name FILENAME.

  3.  v  motion  :w FILENAME  saves the Visually selected lines in file
      FILENAME.

  4.  :r FILENAME  retrieves disk file FILENAME and puts it below the
      cursor position.

  5.  :r !dir  reads the output of the dir command and puts it below the
      cursor position.
```

### Lesson 6

```plaintext
  1. Type  o  to open a line BELOW the cursor and start Insert mode.
     Type  O  to open a line ABOVE the cursor.

  2. Type  a  to insert text AFTER the cursor.
     Type  A  to insert text after the end of the line.

  3. The  e  command moves to the end of a word.

  4. The  y  operator yanks (copies) text,  p  puts (pastes) it.

  5. Typing a capital  R  enters Replace mode until  <ESC>  is pressed.

  6. Typing ":set xxx" sets the option "xxx".  Some options are:
        'ic' 'ignorecase'       ignore upper/lower case when searching
        'is' 'incsearch'        show partial matches for a search phrase
        'hls' 'hlsearch'        highlight all matching phrases
     You can either use the long or the short option name.

  7. Prepend "no" to switch an option off:   :set noic
```

### Lesson 7

```plaintext
  1. Type  :help  or press <F1> or <HELP>  to open a help window.

  2. Type  :help cmd  to find help on  cmd .

  3. Type  CTRL-W CTRL-W  to jump to another window.

  4. Type  :q  to close the help window.

  5. Create a vimrc startup script to keep your preferred settings.

  6. When typing a  :  command, press CTRL-D to see possible completions.
     Press <TAB> to use one completion.
```

## 模式 Modal

-   Normal _正常模式_：在文件中四处移动光标进行修改
-   Insert _插入模式_：插入文本
-   Replace _替换模式_：替换文本
-   Visual _可视化（一般，行，块）模式_：选中文本块
-   Command-line _命令模式_：用于执行命令

在不同的操作模式下，键盘敲击的含义也不同。

## 命令行 Command-line

-   `:q` 退出（关闭窗口）
-   `:w` 保存（写）
-   `:wq` 保存然后退出
-   `:e {文件名}` 打开要编辑的文件
-   `:ls` 显示打开的缓存
-   `:help {标题}` 打开帮助文档
    -   `:help :w` 打开 `:w` 命令的帮助文档
    -   `:help w` 打开 `w` 移动的帮助文档

## 移动/名词 Movement/Nouns

-   基本移动： `hjkl` （左， 下， 上， 右）
-   词： `w` （下一个词）， `b` （词初）， `e` （词尾）
-   行： `0` （行初）， `^` （第一个非空格字符）， `$` （行尾）
-   屏幕： `H` （屏幕首行）， `M` （屏幕中间）， `L` （屏幕底部）
-   翻页： `Ctrl-u` （上翻）， `Ctrl-d` （下翻）
-   文件： `gg` （文件头）， `G` （文件尾）
-   行数： `:{行数}<CR>` 或者 `{行数}G`
    -   `<CR> \r 0x0D`: Carriage Return 回车
    -   `<LF> \n 0x0A`: Line Feed 换行
-   匹配： `%` （找到配对，比如`([{}])`，`/* */` 之类的注释对，`#if, #ifdef, #else, #elif, #endif`）
-   查找：
    -   `f{字符}`，`t{字符}`，`F{字符}`，`T{字符}`
    -   查找在本行的{字符}，光标停在该字符，光标在该字符之前，向前查找，向后查找
    -   `;` 正向，`,`反向
-   搜索：`/{正则表达式}`，`n`正向，`N`反向

## 选择 Selection

可视化模式:

-   可视化：`v`
-   可视化行： `V`
-   可视化块：`Ctrl+v`

可以用移动命令来选中。

## 编辑/动词 Edits/Verbs

-   `i` 进入插入模式
-   `O` / `o` 在之上/之下插入行
-   `d{移动命令}` 删除 {移动命令}
    -   例如， `dw` 删除词, `d$` 删除到行尾, `d0` 删除到行头。
-   `c{移动命令}`改变 {移动命令}
    -   例如， `cw` 改变词
    -   类似于`d{移动命令}` 再 `i`
-   `x` 删除字符（等同于 `dl`）
-   `s` 替换字符（等同于 `xi`）
-   可视化模式 + 操作
    -   选中文字, `d` 删除 或者 `c` 改变
-   `u` 撤销, `<C-r>` 重做
-   `y` 复制 / “yank” （其他一些命令比如 `d` 也会复制）
-   `p` 粘贴
-   `~` 改变字符的大小写

## 计数 Count

用一个计数来结合“名词”和“动词”，这会执行指定操作若干次。

-   `3w` 向前移动三个词
-   `5j` 向下移动 5 行
-   `7dw` 删除 7 个词

## 修饰语 Modifiers

可以用修饰语改变“名词”的意义。修饰语有 `i`，表示“内部”或者“在内”，和 `a`， 表示“周围”。

-   `ci(` 改变当前括号内的内容
-   `ci[` 改变当前方括号内的内容
-   `da'` 删除一个单引号字符串， 包括周围的单引号

## 常用方法

没有特别说明都是在 normal modal 下，`<...>`表示 keys，`[...]`表示 optional

1. 查找整个单词 search a whole word: `/\<word\>`, `\<` represents the beginning of a word, and `\>` represents the end of a word
2. 插入多个空行 insert multiple new lines: `[count]o<Esc>`, `[count]O<Esc>`
3. 在行首第一个非空字符插入 insert at the first non-blank character of the line: `I`, `Shift+i`
4. 在行尾插入 insert at end of line: `A`, `Shift+a`
5. 注释插件 [nerdcommenter](https://github.com/preservim/nerdcommenter), visual and normal modal: 块注释`[count]<Leader>cs`，行注释`[count]<Leader>cc`，取消注释`[count]<leader>cu`，行尾注释 `<Leader>cA`
6. 选中所有 select all: `ggVG`
7. 修改一个单词 change a word: `cw`
8. 在多行同样的位置进行修改 visual-block mode: `<C-q>[hjkl]I[...]<Esc>`
9. 修改括号内的内容 change in the parentheses:`ci(`，修改括号以及内容 change around parentheses: `ca(`
10. 分屏 split a window: `:split`/`:sp`, vertically `:vsplit`/`:vsp`，换屏 change a window`<C-w> [whjkl]`
11. 标签页 `:tabnew [filename]`，切换 next tab `gt`, previous tab `gT`
12. 快速用`()`包括 [auto-pairs](https://github.com/LunarWatcher/auto-pairs) fast wrap: insert mode `<C-f>`, (|)'hello' after fast wrap at |, the word will be ('hello')
13. 复制到系统剪切板[vim-oscyank](https://github.com/ojroques/vim-oscyank) copy to system clipborad: visual mode `<Leader>c`
14. 得到一个配置的值 get a set's value: `:set name?`
15. 跳转下一个光标的位置 go to new cursor position in jump list: `<C-i>`，跳转上一个光标的位置 go to older cursor position in jump list: `<C-o>`
16. 查看 yank 的 register `:reigsters` ，粘贴并覆盖一个单词，在 visual mode 下 `vep`

## neovim :simple-neovim:

1. [neovim GitHub](https://github.com/neovim/neovim)

2. [NvChad Quickstart](https://nvchad.com/docs/quickstart/install)
