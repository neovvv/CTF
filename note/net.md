Unix安全初始化快照
 - 获取所有suid和sgid的文件列表：
 find / -type f -perm -4000
 find / -type f -perm -2000
 - 获取所有隐藏文件列表： find / -name ".*"
 - 获取初始化进程列表： ps -ef -aux
 - 获取开放的端口列表： netstat -anp