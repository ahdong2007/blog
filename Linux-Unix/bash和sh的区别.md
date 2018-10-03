>**问题**：我们通常不会赋予bash脚本可执行权限，需要使用的时候使用 sh <脚本名>来执行。因为从可执行程序看，sh只是bash的一个link，因此我们通常认为这两者是等价。

    [root@huayd1 huayd]# which sh
    /usr/bin/sh
    [root@huayd1 huayd]# ls -l /usr/bin/sh
    lrwxrwxrwx. 1 root root 4 Feb 23  2017 /usr/bin/sh -> bash

**但是，实则不然。**以下部分摘自bash的man page。

>If  bash  is  invoked  with  the  name  sh, it tries to mimic the startup behavior of historical versions of sh as  closely as possible, while conforming to the POSIX standard as well.  When invoked as an interactive login  shell,  or  a non-interactive shell with the --login option, it first attempts to read and execute commands from /etc/proâ€  file and ~/.profile, in that order.  The --noprofile option may be used to inhibit this behavior.  When invoked as  an  interactive  shell  with the name sh, bash looks for the variable ENV, expands its value if it is defined, and uses the expanded value as the name of a file to read and execute.  Since a shell invoked as sh does  not  attempt to  read  and execute commands from any other startup files, the --rcfile option has no effect.  A non-interactive  shell invoked with the name sh does not attempt to read any other startup files.  When invoked as sh, bash  enters   posix mode after the startup files are read.

>When  bash  is  started  in posix mode, as with the --posix command line option, it follows the POSIX standard for  startup files.  In this mode, interactive shells expand the ENV variable and commands are read and  executed  from  the file whose name is the expanded value.  No other startup files are read.


    [root@huayd1 huayd]# cat t1.sh 
    #!/bin/bash

    source ~/.bash_profile

    function f1() {
          echo 1
    }

    function f1-1() {
          echo "f1-1"
    }

    function f1_1() {
        echo "f1_1"
    }  


    f1  
    f1-1
    f1_1
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# sh t1.sh 
    t1.sh: line 11: `f1-1': not a valid identifier
    [root@huayd1 huayd]#  
    [root@huayd1 huayd]# bash t1.sh 
    1
    f1-1
    f1_1
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# bash --posix t1.sh
    t1.sh: line 11: `f1-1': not a valid identifier
    [root@huayd1 huayd]# 

***结论***： sh 等价于  bash --posix

--End
Mason
