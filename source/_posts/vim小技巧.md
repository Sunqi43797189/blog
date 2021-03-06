---
title: vim小技巧
date: 2020-07-07 17:12:27
tags:
  - Vim
categories:
  - Vim
---

1. 插入模式转变为normal模式 `crtl + c`或者 `ctrl + [`
2. 删除一个字符，一个单词，一行 `ctrl + h` `ctrl + w` `ctrl + u`
3. hjkl 左下上右
4. w 移动到下一个单词的开头 e 移动到下一个单词的末尾 非空白分割
5. W 移动到下一个单词的开头 E 移动到下一个单词的末尾 空白分割
6. b 上一个单词的开头 非空白分割， B 上一个单词的开头空白分割
7. 行内快速向前搜索字符f{char} 分号下一个 逗号上一个
8. 行内快速向后搜索字符F{char}
9. 0 移动到行首 ^ 移动行首的第一个非空字符
10. $ 移动到行尾 g_ 移动到行为的第一个非空字符
11. gg 移动到文件开头 G移动到文件末尾，ctrl + o 返回上一次位置
12. ctrl + u 向上翻页 ctrl+f  向下翻页 zz 屏幕中间, zt 将当前行放在最上边
13. x 删除一个字符
14. dw 删除一个单词包含空格
15. diw 删除一个单词不包含空格
16. dt) 快速删除直到括号
17. d$ 快速删除到行尾
18. d0 快速删除到行首
19. 数字加d或者x可以删除多行或多个字符
20. r s c  cw 到单词的末尾，caw整个单词
21. viw 选中一个单词
22. vaw 选中一个单词以及周围的空格
23. 类似命令还有 vis  句子 vip 段落
24. ciw 选中一个单词并进入到插入模式进行修改，单词被替换为空
25. caw 选中一个单词和周围的空格并进入到插入模式进行修改，单词被替换为空
26. ci " 选中双引号中的内容替换为空并进入到插入模式
27. ci + 成对出现的字符，选中成对出现的字符中间的内容，然后进入到插入模式
28. dd 删除一行，行内容到寄存器，可以p直接粘贴
29. yy 复制一行，可以p直接粘贴
30. "+ yy 可以复制内容到系统剪切板
31. "寄存器名字 y 可以复制内容到指定寄存器
32. "+p粘贴系统剪切板的内容
33. :set clipboard=unnamed 设置vim使用系统剪切板
34. 关闭缩进粘贴 :ser paste，粘贴粘贴后开启缩进 :set nopaste
35. cmd + n cmd + p代码补全

### 插件

- vim-surround
  - ys : ysiw" 加双引号 ysiw[  ysiw]
  - cs: cs"'双引号切换为单引号
  - ds: ds' 删除单引号 
- nerdtree
  - 文件数
- ctrlp
  - 文件搜索
- easy-motion
  - 内容快速模糊搜索
- vim-go
- junegunn/fzf.vim 可以替代 ctrlp