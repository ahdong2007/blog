
### 使用sed插入tab

#### 需求

把以下文本的3和4之间的空格换成tab。

    hua$ cat 1.txt 
    1 2 3 4 5 6

期望的结果

    1 2 3   4 5 6    



这是sed最擅长的替换操作，最先想到的方法是:

    hua$ cat 1.txt | sed -E -e 's/ /\t/3'
    1 2 3t4 5 6

很遗憾，\t不能被正确解释。


看回sed的man page，也没有明确的说明如果解决。

但是以前看文档的时候记得有这么一条记录：

    Bash will process escapes, such as \t, inside $' ' before passing it as an arg to sed.

试验证明，以下的写法是可以的：
    
    hua$ cat 1.txt | sed -e $'s/ /\t/3'
    1 2 3	4 5 6

--End
Mason
