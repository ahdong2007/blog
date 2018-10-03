
#### 查看ISO文件信息

我们下载Linux操作系统的ISO文件时，如果没有及时的重命名，可能会分不清哪个ISO文件对应的是哪个版本系统。

比如，Oracle Linux 6.6的ISO文件。

    V52218-01.sio

从文件名上，我们完全无从判断该ISO文件是哪个版本的系统。

所幸，我们有**isoinfo**。

    [root@huayd ~]# isoinfo -d -i V52218-01.iso 
    CD-ROM is in ISO 9660 format
    System id: LINUX
    Volume id: OL6.6 x86_64 Disc 1 20141018
    Volume set id: 
    Publisher id: 
    Data preparer id: 
    Application id: GENISOIMAGE ISO 9660/HFS FILESYSTEM CREATOR (C) 1993 E.YOUNGDALE (C) 1997-2006 J.PEARSON/J.SCHILLING (C) 2006-2007 CDRKIT TEAM
    Copyright File id: 
    Abstract File id: 
    Bibliographic File id: 
    Volume set size is: 1
    Volume set sequence number is: 1
    Logical block size is: 2048
    Volume size is: 1881190
    El Torito VD version 1 found, boot catalog is in sector 632
    Joliet with UCS level 3 found
    Rock Ridge signatures version 1 found
    Eltorito validation header:
        Hid 1
        Arch 0 (x86)
        ID ''
        Key 55 AA
        Eltorito defaultboot header:
            Bootid 88 (bootable)
            Boot media 0 (No Emulation Boot)
            Load segment 0
            Sys type 0
            Nsect 4
            Bootoff 279 633
        
从isoinfo的输出中，我们可以清晰的看到该ISO文件所包含的操作系统版本等信息。

--End
Mason
