# 命令：cat #

cat 命令用于连接文件并打印到标准输出设备上。

**使用权限**

所有使用者

**语法格式**

    cat [-AbeEnstTuv] [--help] [--version] fileName

**参数说明：**

    -n 或 --number：由 1 开始对所有输出的行数编号。
    
    -b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。
    
    -s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。
    
    -v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。
    
    -E 或 --show-ends : 在每行结束处显示 $。
    
    -T 或 --show-tabs: 将 TAB 字符显示为 ^I。
    
    -A, --show-all：等价于 -vET。
    
    -e：等价于"-vE"选项；
    
    -t：等价于"-vT"选项；

**把 textfile1 的文档内容加上行号后输入 textfile2 这个文档里：**

    cat -n textfile1 > textfile2

**清空 /etc/test.txt 文档内容：**

    cat /dev/null > /etc/test.txt

# Linux less命令 #

less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。

**语法**

    less [参数] 文件

**浏览多个文件**

    less log2013.log log2014.log

说明：

输入 ：n后，切换到 log2014.log

输入 ：p 后，切换到log2013.log 

全屏导航

- ctrl + F 向前移动一屏
- ctrl + B 向后移动一屏
- ctrl + D 向前移动半屏
- ctrl + U 向后移动半屏

**单行导航**

- j 向前移动一行
- k 向后移动一行

**其它导航**

- G 移动到最后一行
- g 移动到第一行
- q / ZZ 退出 less 命令

# Linux mv命令 #

Linux mv命令用来为文件或目录改名、或将文件或目录移入其它位置。

**语法**

    mv [options] source dest
    mv [options] source... directory

**参数说明：**

- -i: 若指定目录已有同名文件，则先询问是否覆盖旧文件;
- -f: 在mv操作要覆盖某已有的目标文件时不给任何指示;