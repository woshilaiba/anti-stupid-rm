# anti-stupid-rm
This is a "rm" alternative written in shell. A simple yet effictive tool for most cases.
Modify it to suit for your case.

To arm it into your system do as follow:
1. put anti-stupid-rm into your PATH
2. add alias into your profile. such as append "alias rm=anti-stupid-rm" and "alias realrm=/bin/rm"  to "~/.bashrc" or "/etc/profile" etc.
3. give it executive permission
   chmod 755 anti-stupid-rm
4. done


It just create a "#recycle" directory on each root of mount point which source is block device, 
and move the target to the proper "#recycle".
behavior like this:
 $ rm -rf /home/user/myoldbin/ddddddd
it will read /tmp/mymounts to find which patition does "/home/user/myoldbin/ddddddd" belong to, say /home,
then check to ensure directory "/home/#recycle" is present or creates it, then move "/home/user/myoldbin/ddddddd" into "/home/#recycle".


中文：
上面的英文比较蹩脚，欢迎各位修改。
安装的主要步骤是：
1. 将 anti-stupid-rm添加到 PATH中,可以将其复制到/usr/bin这类的路径中，也可以在环境中
   export PATH="anti-stupid-rm——PATH":$PATH
   添加两个alias到你的环境中(比如"~/.bashrc"或者"/etc/profile"). 
   "alias rm=anti-stupid-rm"
   "alias realrm=/bin/rm"
2. 给定可执行权限
   chmod 755 anti-stupid-rm


这个小玩具是损失惨重的产物，rm -rf 有时候简直是噩梦。
它主要功能就是将待删除的文件回收到它所在的 分区的根目录下的 #recycle目录下，
要求这个分区的设备必须是块设备（因为其他特殊设备没办法建立#recycle目录）。
当前并没有检查分区挂载点是否是只读的，这个不影响使用。

兼容wsl中的分区。

删除非block device上的文件或者没办法创建#recycle目录的分区内的文件时直接使用 /bin/rm -i来询问用户。


如果想要真正的删除某文件需要 使用 "realrm  ddddd"或者  "/bin/rm -rf ddddd"  
^_^

