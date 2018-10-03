
看一些ksh的代码的时候，经常看到使用read来给变量赋值的写法，但是bash脚本中却鲜见这种写法，猜测是有区别。测试如下：


###### Oracle Linux 6.6 Bash

    [root@OraL66 tmp]# cat /etc/redhat-release 
    Red Hat Enterprise Linux Server release 6.6 (Santiago)
    [root@OraL66 tmp]# 
    [root@OraL66 tmp]# echo "w1" "w2" | read w1 w2 
    [root@OraL66 tmp]# 
    [root@OraL66 tmp]# echo $w1
    
    [root@OraL66 tmp]# echo $w2


##### AIX 5.3 Ksh

    $ echo "w1" "w2" | read w1 w2 
    $ echo $w1
    w1
    $ echo $w2
    w2
    $ uname -a
    AIX p570 3 5 00C2DC404C00
    $ 

很明显，在Bash和Ksh中read是有明显的区别。

--End
Mason
