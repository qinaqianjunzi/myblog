### grep可以实现文件搜索过滤

`grep 'word' filename`

### grep递归搜索目录及子目录的所有文件

`grep -rn 'word' dirname`

### grep实现多个关键词搜索（或）

`grep -E 'word|word1|word2' filename`

### grep实现多个关键词搜索(且)

`grep 'word' filename | grep 'word1' | grep 'word2'`

\-v	不包含的字符串

\-i	不区分大小写

\-n	不显示行号
