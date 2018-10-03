

***结论***：

    Linux会cache命令的路径，即使你在PATH中新增了该命令，也还是会读取旧路径的命令。
    
    比如，如下操作：
    1. /bin/下有文件 a.sh
    2. 执行 a.sh
    3. 我在PATH增加路径/root/huayd到PATH的最前面，并放上文件a.sh。
    4. 执行a.sh，此时还是执行的是 /bin下的a.sh，而不是 /root/huayd下的
    
###
***为什么***?
    
    shell的默认选项：
    [root@huayd1 ~]# echo $-
    himBH

    set [--abefhkmnptuvxBCEHPT] [-o option-name] [arg ...]
       set [+abefhkmnptuvxBCEHPT] [+o option-name] [arg ...]
              Without  options, the name and value of each shell variable are displayed in a format that can be reused as
              input for setting or resetting the currently-set variables.  Read-only variables cannot be reset.  In posix
              mode, only shell variables are listed.  The output is sorted according to the current locale.  When options
              are specified, they set or unset shell attributes.  Any arguments remaining  after  option  processing  are
              treated  as  values for the positional parameters and are assigned, in order, to $1, $2, ...  $n.  Options,
              if specified, have the following meanings:
              
              ......
              -h      Remember the location of commands as they are looked up for execution.  This is enabled by default.

*默认打开的-h选项会记住命令旧的路径，在同一session中，再次执行相同命令时，不再进行命令的路径寻找。*
###
***场景重现如下：***    
    
    [root@huayd1 huayd]# chmod +x /usr/bin/a.sh
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# a.sh
    b
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# export PATH=/root/huayd:$PATH
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# a.sh
    b
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# echo $PATH
    /root/huayd:/root/huayd:/usr/lib64/qt-3.3/bin:/root/perl5/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/root/bin:/root/go/bin:/usr/local/mysql-proxy/bin:/root/bin:/root/go/bin:/usr/local/mysql-proxy/bin
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# chmod +x *
    [root@huayd1 huayd]# ./a.sh 
    a
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# a.sh 
    b
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# find / -name 'a.sh'
    /root/huayd/a.sh
    /usr/bin/a.sh
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# cat /root/huayd/a.sh
    echo a
    [root@huayd1 huayd]# 
    [root@huayd1 huayd]# cat /usr/bin/a.sh
    echo b
    [root@huayd1 huayd]# 

    
 --End
Mason
