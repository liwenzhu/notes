Ubuntu 重置密码
==============

* ESC 进入grub引导

* 选择第一项 Ubuntu, 按e进入编辑页面

* 替换ro quiet splash 为 rw init=/bin/bash

* ctrl-x 继续进入单机模式

* passwd <username>

重起后就可以使用新设置的密码了。
