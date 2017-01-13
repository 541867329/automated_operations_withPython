# automated_operations_withPython
Python批量登录到服务器执行任务
http://www.niceru.com/topic/870.html
感谢作者

根据信息系统安全等级保护的要求，需要对IDC所有数据库服务器进行安全检查，以确认服务器的安全设置是否符合等级保护要求，需要在所有数据库服务器上执行以下命令：
wget http://10.4.4.140/tools/check.sh
bash check.sh

对于目前现状，我们总共目前约有mysql数据库约60台左右，加上oracle数据库会更多，如果通过单一的登录到每个数据库服务器执行，效率是非常低的，所以写了一个批量执行的Python脚本。该脚本会读取一个定义好的服务器列表和命令列表，然后利用了python的多进程特性，每个服务器一个独立进程，自动登录到对应的服务器，运行相应的脚本。登录认证方式包括密码登录和密钥登录，如果定义了密钥，则脚本会使用密钥登录，否则则使用密码登录。该脚本比较通用，在自动化监控和运维过程中比较实用，下面将对脚本做简单的分析。

代码解析：
该脚本共有两个文件，linux_batch_command.py和linux_servers.list。linux_batch_command.py用于执行自动登录和运行脚本。linux_servers.list用于定义主机列表。

linux_batch_command.py代码如下：需要执行的命令定义在cmds=”’ ”’里面，需要执行多个命令用，分隔。timeout用于定义登录服务器和执行脚本的超时时间，运行时间比较长的话该值请修改的比较大些。
