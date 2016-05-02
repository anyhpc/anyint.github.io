表现
Remmina 提示消息： Unable to connect rdp server

解决方法
删除   ~/.freerdp/known_hosts 文件，即：

rm ~/.freerdp/known_hosts


原因
可能是域名对应的机器变了，所以要把缓存的密钥删除掉