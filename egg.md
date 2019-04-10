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
        };
