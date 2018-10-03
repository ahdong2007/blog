


***结论***：find命令中使用通配符(*)时，务必加上双引号，虽然有时不加双引号也能正常工作，但这是偶然的，有前提的。如下：

> When you run find . -name *.bak, the third command-line argument, *.bak, is expanded by the shell before it is passed to find. Shell expansion will convert it to a space-delimited list of all the filenames in the current directory that match it, i.e., all the files whose names consist of zero or more characters (*) followed by .bak. When you enclose *.bak in quotes, that escapes the * wildcard, so the expression is passed unexpanded. You could alternatively use find . -name \*.bak. 


> -name pattern
     Don't forget to enclose the pattern in quotes in order to protect it from expansion by the shell.

    # 通配符(*)会被shell展开
    [root@huayd2 ~]# echo *
    anaconda-ks.cfg Desktop Documents Downloads huayd initial-setup-ks.cfg install_docker.sh mariadb-10.1.23-rhel-7-x86_64-rpms.tar mariadb-10.2.6-rhel-7-x86_64-rpms mariadb-10.2.6-rhel-7-x86_64-rpms.tar Music p13390677_112040_Linux-x86-64_1of7.zip p13390677_112040_Linux-x86-64_2of7.zip passwd.txt Percona Percona.txt perl5 Pictures Public Templates tp.sh Videos
    [root@huayd2 ~]# 

    # /root目录下有 zip结尾的文件，通配符(*)会被展开，展开后命令不再符合find命令的语法规则，直接报错
    [root@huayd2 ~]# pwd
    /root
    [root@huayd2 ~]# find /root -name *.zip
    find: paths must precede expression: p13390677_112040_Linux-x86-64_2of7.zip
    Usage: find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec] [path...] [expression]
    [root@huayd2 ~]# 
    [root@huayd2 ~]# 
    
    
    # /tmp目录下没有 zip结尾的文件，因此通配符(*)不会被展开
    # 也因此虽然通配符(*)上没有加双引号，find也能正常工作
    [root@huayd2 ~]# cd /tmp/
    [root@huayd2 tmp]# find /root -name *.zip
    /root/p13390677_112040_Linux-x86-64_1of7.zip
    /root/p13390677_112040_Linux-x86-64_2of7.zip
    [root@huayd2 tmp]# 
    [root@huayd2 tmp]# 
    [root@huayd2 tmp]# cd -
    /root
    [root@huayd2 ~]# pwd
    /root
    [root@huayd2 ~]# find /root -name "*.zip"
    /root/p13390677_112040_Linux-x86-64_1of7.zip
    /root/p13390677_112040_Linux-x86-64_2of7.zip
    [root@huayd2 ~]# 
    [root@huayd2 ~]# 
    [root@huayd2 ~]# find /root -name \.zip
    [root@huayd2 ~]# find /root -name \*.zip
    /root/p13390677_112040_Linux-x86-64_1of7.zip
    /root/p13390677_112040_Linux-x86-64_2of7.zip
    [root@huayd2 ~]# 

--End
Mason
