

> 问题：Centos 7.3环境，把命令放到 /etc/rc.local后，发现并没有在服务器重启后自动执行。

#### /etc/rc.local 7.x 后有变化

    [root@localhost ~]# 
    [root@localhost ~]# cat /etc/redhat-release 
    Red Hat Enterprise Linux Server release 6.7 (Santiago)
    [root@localhost ~]# 
    [root@localhost ~]# cat /etc/rc.local 
    #!/bin/sh
    #
    # This script will be executed *after* all the other init scripts.
    # You can put your own initialization stuff in here if you don't
    # want to do the full Sys V style init stuff.
    
    touch /var/lock/subsys/local
    
    [root@huayd1 huayd]# cat /etc/redhat-release 
    CentOS Linux release 7.2.1511 (Core) 
    [root@huayd1 huayd]# cat /etc/rc.local 
    #!/bin/bash
    # THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
    #
    # It is highly advisable to create own systemd services or udev rules
    # to run scripts during boot instead of using this file.
    #
    # In contrast to previous versions due to parallel execution during boot
    # this script will NOT be run after all other services.
    #
    # Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
    # that this script will be executed during boot.
    
    touch /var/lock/subsys/local
    
注意到 7.x的环境，多了这么一句描述：

> Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure

除此之外，还有一个区别，6.x的版本中，明确说明，这个脚本是在其他所有的启动脚本之后执行：
> This script will be executed *after* all the other init scripts.

但7.x的描述有了变化，不在保证 /etc/rc.local一定是在最后执行。
> this script will NOT be run after all other services.

实际上，从 7.x 版本开始，引入了 systemd 来管理服务，/etc/rc.local 是为向前兼容而保留。

--End
Mason
