# 1.ubuntu下的pm2的常用命令
创建文件夹：mkdir name<br
创建文件：touch name<br>
删除一个文件夹：rm -rf name<br>
删除一个文件：rm -f name<br>
编辑文件：vim name <br>
进入vim的输入模式：i  <br/>
退出输入模式：按Esc + ：+ q(不保存)或者wq(保存)<br/>
启动node项目：pm2 start name<br/>
查看已启动的项目: pm2 list<br/>
查看启动的端口： netstat -toln<br/>
停止项目：pm2 stop id<br/>
nginx查看进程：ps -ef|grep nginx<br/>
杀死nginx进程：kill -TERM 进程号<br/>
启动nginx：nginx，<br/>
查看php-fpm位置：whereis php-fpm<br/>
停止php-fpm:pkill php-fpm<br/>
启动php-fpm:运行php-fpm位置<br/>
重启nginx: nginx -s reload<br/>
apache启动: /etc/init.d/apache2 start<br/>
apache暂停：/etc/init.d/apache2 stop<br/>
apache重启：/etc/init.d/apache2 restart<br/>
赋予文件的写入权限： chmod -R 777 name<br/>
## nginx.conf的文件配置：
在/etc/nginx/conf.d的目录下新增.conf的配置文件
server {
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
