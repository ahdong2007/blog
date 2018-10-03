>工作中，我们有时需要通过脚本来增加或修改crontab job，但是crontab -e的方式增加是交互式的，因此总结了如下两种通过脚本增加crontab job的方法。

    # 方法1

    [root@Mason cron]# crontab -l
    0 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    1 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    [root@Mason cron]# 
    [root@Mason cron]# echo "2 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1" >> root
    [root@Mason cron]# 
    [root@Mason cron]# crontab -l
    0 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    1 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    2 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    [root@Mason cron]# pwd
    /var/spool/cron
    [root@Mason cron]# 
    
    # 方法2
    
    [root@Mason cron]# crontab -l > /tmp/crontab.out
    [root@Mason cron]# echo "3 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1" >> /tmp/crontab.out 
    [root@Mason cron]# crontab /tmp/crontab.out 
    [root@Mason cron]# crontab -l
    0 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    1 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    2 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    3 3 * * * sh /u01/scripts/del_arch.sh >/dev/null 2>&1
    [root@Mason cron]# 

--End
Mason
