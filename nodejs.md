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
# nodejs常用的插件
1.express 框架<br>

        const express = require('express');
        const app = express();
2.express-fileupload 文件上传<br>
   
        const upload = require('express-fileupload')
        app.use(upload({
                limits: {fileSize: 50 * 1024 * 1024}//文件上传大小限制
        }))

3.express-session session设置(注意session的use一定要路由的前面，否则获取不到session)<br>

        const session = require('express-session') //session
        app.use(session({
            secret :  'secret',
            resave : true,
            saveUninitialized: false,
            cookie : {
                maxAge : 1000 * 60 * 3,
            },
        }));
        
4.mongoose 数据库<br>

        const mongoose = require('mongoose')
        //mongodb://mao:aaa123456@ds037768.mlab.com:37768/jia-juan-mao
        const url = 'mongodb://127.0.0.1:27017/myapp' //数据库地址
        mongoose.connect(url, {useNewUrlParser: true})
        mongoose.connection.on('error', console.error.bind(console, 'connection error:'));
        mongoose.connection.once('open', function (callback) {
            console.log("数据库成功连接");
        });
5.pug 模板引擎<br>
        
        const cookieParser = require('cookie-parser');
        const logger = require('morgan');
        app.set('views', path.join(__dirname, 'views'));
        app.set('view engine', 'pug');

        app.use(logger('dev'));
        app.use(express.json());
        app.use(express.urlencoded({ extended: false }));
        app.use(cookieParser());
        app.use(express.static(path.join(__dirname, 'public')));
        
6.svg-captche svg验证码<br>
        
        //这个是在路由文件中注册的验证码
        const express = require('express');
        const router = express.Router();
        const svgcode = require('svg-captcha')
        router.get('/imgecho', function(req, res){
        let conf = {
                size: 4,
                ignoreChars: '0OoliI',
                noise: 2,
                height: 50
        } 
            let imgcode = svgcode.create(conf)
            req.session.yzma = imgcode.text.toLowerCase()
            let codeData = {
                img: imgcode.data
            }
            res.send(codeData);
        })
        module.exports = router;
        
7.crypto md5加密<br>
        
        const crypto = require('crypto')
         let md5poss = crypto.createHash('md5').update('数据').digest('hex')
## mongoose操作数据库
 1.要在数据库建立对应的数据库如：myapps <br>
 2.链接的数据库链接为： mongodb://127.0.0.1:27017/myapps （本地的数据）
 3.model模块操作数据库
        
        const mongoose = require('mongoose')
        //一切起于schema
        let Schema = mongoose.Schema;
        //设计表格式
        let VideolsitSchema = new Schema({
            name: String,
            describe: String,
            videocode: String,
            videoimg: String,
            ifoff: {type: Boolean, default: true},
            time: {type: Date, default: Date.now}
        })
        //创建数据表 会在myapps中生成username的数据表
        let UserTable = mongoose.model("username", VideolsitSchema)
        //向外暴露模块
        module.exports = UserTable
        <hr>
        增删改查
        > new UserTable(data).save(fn)
        > 
        
