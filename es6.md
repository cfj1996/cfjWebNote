 ## 异步操作
  1. Promise <br>
  例如现在nodejs要读取两个表中的数据然后res.json({data: data})
  
    //读取homevideo表中的数据
    let prom1 = function () {
        return new Promise(function (resolve, reject) {
        //resolve为成功后的回调函数（就是下面.then的参数），reject为失败后的回调函数（就是下面。catch的参数）
            homevideo.findOne({name: 'videolist_img'}, (err, data) => {
                if (err) reject(err)
                else resolve(data)
                console.log('查询执行1')
            })
        })
    }
    //读取Vdeolsit表中的数据
    let prom2 = function () {
        return new Promise(function (resolve, reject) {
            Vdeolsit.find({ifoff: true}, (err, data) => {
                if (err) reject(err)
                else resolve(data)
                console.log('查询执行2')
            })
        })
    }
    Promise.all([prom1(), prom2()]).then(
        //都成功查询后执行的函数data为两次查询的结果为一个数组
         (data)=>{
          res.json({data: data})
          }
      ).catch(
      //查询失败后执行的函数
      (err) => {console.log(err)}
      )
  
