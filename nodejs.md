# 1.ubuntu下的pm2的常用命令
创建文件夹：mkdir name<br>
创建文件：touch name<br>
删除一个文件夹：rm -rf name<br>
删除一个文件：rm -f name<br>
编辑文件：vim name <br>
进入vim的输入模式：i  <br/>
退出输入模式：按Esc + ：+ q(不保存)或者wq(保存)<br/>
启动node项目：pm2 start name<br/>
查看已启动的项目: pm2 list<br/>
    3. 根据进程pid查端口：

       netstat -nap | grep pid

    4.  根据端口port查进程

       netstat -nap | grep port
# ubuntu下的apache命令
apache启动: /etc/init.d/apache2 start<br/>
apache暂停：/etc/init.d/apache2 stop<br/>
apache重启：/etc/init.d/apache2 restart<br/>
赋予文件的写入权限： chmod -R 777 name<br/>

# 2.ubuntu下的安装node
## 更新ubuntu软件源
* sudo apt-get update
* sudo apt-get install -y python-software-properties software-properties-common
* sudo add-apt-repository ppa:chris-lea/node.js
## 安装node
* sudo apt-get install nodejs
* sudo apt install nodejs-legacy
* sudo apt install npm
## 安装 n 管理包
* sudo npm install n -g
## 安装最新的nodejs（stable版本）
* sudo n stable
* sudo node -v

# 3.ubuntu下的nginx命令
## nginx信号操作 kill -信号选项 nginx主进程号
### nginx常用信号
TERM, INT：	Quick shutdown <br>
QUIT:	Graceful shutdown  优雅的关闭进程,即等请求结束后再关闭 <br>
HUP :	Configuration reload ,Start the new worker processes with
        a new configuration Gracefully shutdown the old worker processes
        改变配置文件,平滑的重读配置文件 <br>
USR1:	Reopen the log files 重读日志,在日志按月/日分割时有用 <br>
USR2:	Upgrade Executable on the fly 平滑的升级<br>
WINCH:	Gracefully shutdown the worker processes 优雅关闭旧的进程(配合USR2来进行升级)<br>

# 4.小白兔（navicat）连接不上服务器的数据库的解决方案
* 报错 80070007: SSH Tunnel: Server does not support diffie-hellman-group1-sha1 for keyexchange
1. 进入 /etc/ssh/sshd_config 在最下面 加入下面代码

        KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-                   nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1
        Ciphers 3des-cbc,blowfish-cbc,aes128-cbc,aes128-ctr,aes256-ctr

2. 执行下面代码

        ssh-keygen -A
        
3. 重启SSH

        service ssh restart

查看启动的端口： netstat -toln<br/>
停止项目：pm2 stop id<br/>
查看配置文件是否正确： nginx -t <br/>
nginx查看进程：ps -ef|grep nginx<br/>
杀死nginx进程：kill -TERM 进程号<br/>
启动nginx：nginx，<br/>
查看php-fpm位置：whereis php-fpm<br/>
停止php-fpm:pkill php-fpm<br/>
启动php-fpm:运行php-fpm位置<br/>
重启nginx: nginx -s reload<br/>
优雅启动： nginx -HUP 进程号 或者 kill -HUP `cat /run/nginx.pid` （反引号中的是nginx的pid文件，cat返回进程号）<br>

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
8. compression gzip压缩
        
        let compression = require('compression')
        app.use(compression()) //最前面
        
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
        
        增删改查
        > new UserTable(data).save(fn)
        > 
        
##nodejs的请求值
        1.get请求值的获取 req.query <br>
        2.post请求 要载入 body-parser 中间件 才能用req.body <br>
        3.file文件 req.files <br>

## mysql数据库的操作
1. sql语句

        let sql = 'SELECT * FROM `books` WHERE `author` = "David"'
        //变量用反引号
        
2. 连接数据库
        
        const mysql = require('mysql')
        let connection = mysql.createConnection({
            host: 'localhost',
            user: "root",
            password: "root",
            database: "waijie"
        })
        connection.connect()
        
        let chacun = function () {
        let inquire = `SELECT * FROM user WHERE name = "陈方杰"`
            return new Promise(function (resolve, reject) {
                connection.query(inquire, function (err, data) {
                    if (err) reject(err)
                    else connection.end()
                        resolve(data)
                })
            })
        }
        app.get('/', async function (req, res) {
        let data = await chacun()
        console.log(data[0].name)
        res.send(data)
        // data = JSON.stringify(data)

        })
        
    3.sequelizejs ORM 操作联表查询
        
        1. 定义模型的关系
            1：1 关系
                Model1.associate = () => {
                    Model1.belongsTo(model2,{键值对关系})
                }
            1：n 关系
                  Model1.associate = () => {
                    Model1.hasMany(model2,{键值对关系})
                }
            n: 1 关系
                   Model1.associate = () => {
                    Model1.belongsTo(model2,{键值对关系})
                }
            n: m 关系
                
                   Model1.associate = () => {
                    Model1.belongsToMany(model2,{键值对关系})
                }
            
            ps: 
                Model1: 源模型
                model2: 目标模型
            
                键值对关系说明：
                1.targetKey： 目标建 表示目标模型上的与资源模型匹配的键 （默认是和foreignKey ）
                2.foreignKey： 外键 设置源模型上的外键
                3.sourceKey: 资源key 表示源模型上的资源匹配键 ？？？？
        2. 查询语法：
        
        mode1.findAll或者findAndCountAll ({
                include: [{model2,where,...}]
                where,...
            })
        const res = await app.model.User.findOne({
            attributes: [ app.Sequelize.col('img.imgurl'), 'id', 'amount', 'username' ],
                include: [{
                model: app.model.Userimg,
                as: 'img',
                attributes: [ ],
            }],
            raw: true,
            where: { username: ctx.request.body.userName },
        });
