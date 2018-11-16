# 1.ubuntu下的pm2的常用命令
> 创建文件夹：mkdir name 
> 创建文件：touch name
> 删除一个文件夹：rm -rf name
> 删除一个文件：rm -f name
> 编辑文件：vim name
> 进入vim的输入模式：i
> 退出输入模式：按Esc + ：+ q(不保存)或者wq(保存)
> 启动node项目：pm2 start name
> 查看已启动的项目: pm2 list
> 查看启动的端口： netstat -toln
> 停止项目：pm2 stop id
> nginx查看进程：ps -ef|grep nginx
> 杀死nginx进程：kill -TERM 进程号
> 启动nginx：nginx，
> 查看php-fpm位置：whereis php-fpm
> 停止php-fpm:pkill php-fpm
> 启动php-fpm:运行php-fpm位置
> 重启nginx: nginx -s reload
> apache启动: /etc/init.d/apache2 start
> apache暂停：/etc/init.d/apache2 stop
> apache重启：/etc/init.d/apache2 restart
> 赋予文件的写入权限： chmod -R 777 name
> nginx.conf的文件配置：
> 在/etc/nginx/conf.d的目录下新增.conf的配置文件
> server {
        listen       80; //检测端口
        server_name  order.lookk.cn;    #要访问的域名或者ip，如果有多个，用逗号分开
 
        charset utf8;
 
        location / {
            proxy_pass       http://127.0.0.1:8080;               #映射到代理服务器，可以是ip加端口, 
            proxy_set_header Host      $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
 
       }
    }
