## 1. 常用
  1. 查看服务安装的位置
    1. which redis 或者 whereis redis
    2. ps -aux | grep nginx 查看进程号 5533 然后 ll /proc/5393/cwd  
  2. 清空命令行 
    ctrL + L
  3. 查看当前路径
    pwd 显示工作路径 
  4. mkdir fileName 创建文件夹
  5. rm -f fileName 删除文件
  6. rmdir fileNames 删除目录
  7. mv filesName1 filesName2 重命名/移动 一个目录 
  8. cp file1 file2 复制一个文件
  9. find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录
  10. rz  sz 文件上传下载

## 2. 查看进程
  1. ps -aux | grep nginx 进程名查看进程号
  2. netstat -ntlp 查看所有的端口占用
  3. netstat -ntulp |grep 80 查看80端口占用
  4.  kill[参数][进程号] 结束进程 
## 3. nginx
  1. nginx -s quit nginx -s quit 
  2. nginx -s reload     优雅重启
  3. nginx -s reopen     重新打开日志文件
  4. nginx -v            查看版本
  5. nginx -t            检查nginx的配置文件
  6. nginx常用信号
    TERM, INT：	Quick shutdown 
    QUIT:	Graceful shutdown 优雅的关闭进程,即等请求结束后再关闭 
    HUP :	Configuration reload ,Start the new worker processes with a new configuration Gracefully shutdown the old worker processes改变配置文件,平滑的重读配置文件 
    USR1:	Reopen the log files 重读日志,在日志按月/日分割时有用 
    USR2:	Upgrade Executable on the fly 平滑的升级
    WINCH:	Gracefully shutdown the worker processes 优雅关闭旧的进程(配合USR2来进行升级)
