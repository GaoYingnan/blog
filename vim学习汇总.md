#VIM学习汇总
### 1.vim简介
vim是一种有*模式*的文本编辑器，如：普通模式、插入模式、可视模式等。初入门最常用的是普通模式和插入模式。
Git Bash下输入“vim a.md”进入vim编辑页面。
编辑页面下“i”命令进入插入模式；插入模式下“ESC”键进入编辑模式。
编辑模式下有很多命令，这些命令可以通过组合输入来快速高效的完成对文本的编辑，例如：“dd”表示删除光标所在行，而输入“2dd”（“dd”重复两次）则表示删除光标后两行。
### 2.编辑模式
编辑模式的主要功能是*移动光标*，然后对文本进行剪切、删除、复制、插入、替换等
tips：

 - 编辑模式下光标指向它右侧的字符，与windows下的word不同。例如要删除字符“M”，在word中要先把光标移到“M”的右侧，然后删除。而vim的编辑模式下使用<code>*x*</code>命令时。要先把光标移动到“M”的左侧，然后使用。
 -  Vim 编辑器经常以一对大、小写字母（如 p 和
   P）来提供一对相似的功能。通常，小写命令在光标的后面进行操作，大写命令在光标的前面进行操作。
 - 普通模式下有很多命令，这些命令可以通过组合输入来快速高效的完成对文本的编辑，例如：“dd”表示删除光标所在行，而输入“2dd”（“dd”重复两次）则表示删除光标所在行及下一行。

2.1打开、保存、退出文本
<pre>
:e path_to_file/filename        打开path_to_file/filename文本
:w                              保存当前修改，不退出
:w file_temp                    文件另存为file_temp
:q                              在未作修改的情况下退出（修改后不保存直接退出会提示）
:q!                             放弃所有修改，退出编辑程序。
:wq                             先保存后退出的组合命令
</pre>
<p>&nbsp;</p>
2.2移动光标
移动一个字符：
<pre>
k                上移
j                下移
h                左移
l                右移
</pre>
tips：在命令前加上数字代表命令执行次数，如：5k，表示上移5行。
<pre>
H            移动到屏幕顶端的行
M            移动到屏幕中央的行
L            移动到屏幕底端的行

nH           移动到屏幕顶端往下的第n行
nL           移动到屏幕顶端往上的第n行
</pre>
tips：这些命令（全都是*大写*）不会滚屏，只是对当前页面进行操作。（感觉用5k这样的方式也可以很快的实现啊。）
**按单词移动（ew大小写啥的没整明白）**
<p>&nbsp;</p>
整行移动
<pre>
0            移动到行首
$            移动到行末
+            移动到下一行开头
-            移动到上一行开头
</pre>
tips：“+”“-”不管你的光标在当前行何处，总是移动到下一行或上一行的行首。假如现光标在第二行的第二个字符，按“k”/“j”就会移动到上一行或下一行的第二个字符处。
<p>&nbsp;</p>
滚屏
<pre>
Ctrl+f            往前滚动一整屏
Ctrl+b            往后滚动一整屏
Ctrl+d            往前滚动半屏
Ctrl+u            往后滚动半屏

zEnter          将光标所在行移动到屏幕顶端
z.              将光标所在行移动到屏幕中间
z-              将光标所在行移动到屏幕低端

Ctrl+g            显示当前行信息
nG                转至第n行
G                 转至文本末尾
gg　　　　　　  　  移至文本开头
</pre>
tips：10zEnter，是把第10行移    滚动到屏幕顶端。
<p>&nbsp;</p>
根据文本块移动
<pre>
（           移动到当前句子开头
）           移动到下一个句子开头

{            移动到当前这一段开头   
}            移动到下一段开头

[[           移动到当前这一节的开头
]]           移动到下一节的开头
</pre>
**疑问：什么是区分段落、句子、节的区别？？？**
<p>&nbsp;</p>
2.2删除和替换
<pre>
rc        用 c 替换光标所指向的当前字符；
x         删当前光标所在的一个字符。
dd        删除当前行，并把删除的行存到剪贴板里（去除空隙）
d$        从当前光标起删除字符直到行的结束
d0        从当前光标起删除字符直到行的开始
J         删除本行的回车符（CR），并和下一行合并
p         粘贴剪贴板
</pre>
tips:

 - "3dd”表示删除光标所在行和下两行。“3p”表示复制三次
 - “3x”表示删除光标所指向的前 3 个字符；“3rA”用 A 替换光标所指向的前 5 个字符
**“光标指向的前”是光标指向的字符以及它右边的文本。**（等我学会怎么整图片后用图片表示更清楚些）
**？替换的命令没搞明白，后续整明白了再写。**
<p>&nbsp;</p>
2.4复制粘贴
<pre>
yy              复制当前行到内存缓冲区
nyy             复制 n 行内容到内存缓冲区
5yy             复制 5 行内容到内存缓冲区
“+y             复制 1 行到操作系统的粘贴板
“+nyy           复制 n 行到操作系统的粘贴板
</pre>
tips：**缓冲区与粘贴板是什么区别？是什么？**
<pre>
p               小写字母 p，将剪切板的内容粘贴到光标的后面
P               大写字母 P，将剪切板区的内容粘贴到光标的前面
</pre>
tips:
 - 如果剪切板的内容是字符或字，直接粘贴在光标的前面或后面；如果缓冲区的内容为整行正文，执行上述粘贴命令将会粘贴在当前光标所在行的上一行或下一行
 - 这里光标前就是光标的左边，光标后就是光标的右边**（注意区分“光标指向前”与“光标前”的不同）**
 - 注意上述两个命令中字母的大小写。
 <p>&nbsp;</p>
2.5字符串搜索
<pre>
:/str/                  正向搜索，将光标移到下一个包含字符串 str 的行
:?str?                  反向搜索，将光标移到上一个包含字符串 str 的行
</pre>
<p>&nbsp;</p>
新人初学，有很多地方难免有错，恳请各位指正，在此感谢。其中没搞明白的问题，在学习后再做更新。