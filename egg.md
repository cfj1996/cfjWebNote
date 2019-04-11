## egg常用配置
  
  1. 监听端口
  
         config.cluster = {
              listen: {
                path: '',
                port: 7030,
                hostname: '127.0.0.7',
              },
            };
          
  2. 关闭csrf
  
         config.security = {
            csrf: {
              enable: false,
            },
          };

  3.  sequelize连接数据库
  
          config.sequelize = {
            username: 'root',
            password: 'root',
            dialect: 'mysql',
            host: '127.0.0.1',
            port: 3306,
            database: 'sequelize',
            timezone: '+08:00' // 时区
          };
        
  4.  模型的定义
  
          // egg会默认将模型名变为复数
            "use strict";
              module.exports = app => {
                const { INTEGER, STRING, DATE, NOW } = app.Sequelize
                let User = app.model.define('user', {
                  id: {
                    type: INTEGER,
                    primaryKey: true, // 表的主键
                    autoIncrement: true // 自动递增
                  },
                   name: {
                    type: STRING,
                    field: 'userName'映射到数据表的userName字段
                    set(val){ // 写入数据劫持
                      this.setDataValue('name', val + '123456')
                    },
                    get(){ // 读取数据劫持
                    return '数据被劫持' + this.getDataValue('add_time')
                    }
                  },
                  add_time: {
                    type: DATE,
                    allowNull: false, // 允许为空
                    defaultValue: NOW, // 当前默认时间
                    comment: "I'm a comment!" // 注释             
                  }
                },{          
                  timestamps: true, // 开启时间戳，关闭createdAt
                  createdAt: false, 
                  updatedAt: 'updateTimestamp' // 将updatedAt绑定到updateTimestamp字段上
                  tableName: 'user' // 表名
                  freezeTableName: true, // 取消egg将模型名改为复数
                })
                return User
              }
       
   5.模型的方法
   
            1.创建或查找
              const res = await modul.create(data) // 创建单条数据 返回的是一个Promise对象
              res.get({plain: true}) // 返回插入的数据 res.get('name') //返回插入的name字段值
              
              const res = await modul.bulkCreate([data1.data2,data3....])创建多条数据
              res[0].get({plain: true})
              
            2.更改，递增
              更改 modul.update(data, {where:{/*条件*/})
              递增 
              User.findByPk(1).then(user => {
                return user.increment('name', {by: 2})
              }).then(user => {
              })
            
            3.硬刪除,软删除
              硬删除 直接调用modul.destroy({where:{/*条件*/}})
              软删除在模型中增加 paranoid: true, 调用modul.destroy({where:{/*条件*/}})时会将deleted_at的字段添加当前时间，如果想硬删除增加                 force: true的属性，如果要取消删除model.restore({where:{/*条件*/});
            
            4.查询
            
            5.重新加载
            Person.findOne({ where: { name: 'john' } }).then(person => {
            person.name = 'jane'
            console.log(person.name) // 'jane'
            person.reload().then(() => {
              console.log(person.name) // 'john'
            })
          })
