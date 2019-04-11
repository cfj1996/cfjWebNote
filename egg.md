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
            })
            return User
          }
