# 一.安装数据库
npm install mongoose --save
## 1.mongo.conf配置文件


    dbpath=D:\MongoDB\data
    #数据库文件存放位置
    logpath=D:\MongoDB\log\mongo.log
    #日志文件存放位置
    logappend=true
    journal=true
    quiet=true 
    port=27017 #启动端口

## 2.开启服务: ./mongod --config "mongo.conf配置文件路径"
## 3.mongoshell链接: 再新的cmd中输入 ./mongo (上一个窗口不能关)

## 4.常用数据库命令
  * 创建数据库: use name  (指定数据库） <br>
  * 删除数据库：db.dropDatabase() <br>
  * 创建集合: db.createCollection(name) <br>
  * 删除集合: db.name.drop() <br>
  * 查看集合: show collections <br>
  * 插入文档: db.collections_name.insert({data}) <br>
  * 更新文档: db.collections_name.updata(<query>,<update> ,{data})  <br>
    > query: update的查询条件 <br>
    > update: update的对象和一些更新的操作符 <br>
  * 删除文档: db.name.remove(<query>,<justOne>) <br>
    > justOne: （可选）如果设为 true 或 1，则只删除一个文 <br>
  * 查看文档: db.collections_name.find(<query>, projection).pretty() <br>
    > projection: 指定返回的键 <br>
    > pretty:格式化的方式来显示 <br>
  * 条件操作符： <br>
      > (>) 大于 - $gt <br>
      > (<) 小于 - $lt <br>
      > (>=) 大于等于 - $gte <br>
      > (<=) 小于等于 - $lte <br>
  * 如:db.name.find({likes : {$gt : 100}}) //"likes" 大于 100 的数据<br>
   
  * 类型操作符：db.name.find({"title" : {$type: type}}) 
      > type对应的类型： 
          >> Double	1	 
          >> String	2	 
          >> Object	3	 
          >> Array  4
    * 限制输出条数limit()方法与查询指针起点Skip()
       > 如：db.name.find({},{"title":1,_id:0}).limit(2).skip(3) 输出查询到的所有数据的第4，5条数据
    * 排序sort(1)

## egg-mongoose
     
    插件安装
        npm i  egg-mongoose --save
    插件配置
        plugin.js文件配置
        module.exports = {
            mongoose : {
                enable: true,
                package: 'egg-mongoose',
            }
        };
        config.default.js文件配置
          // mongoose
          config.mongoose = {
            client: {
              url: 'mongodb://127.0.0.1/test1',
              options: {},
              // mongoose global plugins, expected a function or an array of function and options
              plugins: [],
            },
          };
          模型定义
            module.exports = app => {
                const mongoose = app.mongoose;
                const Schema = mongoose.Schema;

                const UserSchema = new Schema({
                    name: { type: String  },
                    age: { type: Number  },
                });
                // egg对应的集合名默认加s，所以model方法的第三个参数传集合名
                return mongoose.model('User', UserSchema, 'user');
            }
