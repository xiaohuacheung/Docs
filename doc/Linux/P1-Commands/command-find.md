# Command: FIND




例子：

1. 列出结尾不是 .rpm 的文件，并删除

    find -type f \( ! -iname "*.rpm" \) -print -exec rm {} \;^C
