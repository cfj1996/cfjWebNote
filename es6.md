 ## 异步操作
  # 1. Promise 
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
    //并行执行，没有先后顺序
    Promise.all([prom1(), prom2()]).then(
        //都成功查询后执行的函数data为两次查询的结果为一个数组
         (data)=>{
          res.json({data: data})
          }
      ).catch(
      //查询失败后执行的函数
      (err) => {console.log(err)}
      )
    //先后顺序 注意要由于第一次查询的数据再后面的.then中是访问不到的，要么设置全局接受后存储要么在上面的prom2函数中就收data合并在prom2查询到的值中
    prom1().then((data)=>{return prom2(data)}).then((data2)=>{
        console.log(data2)
    })
    // async操作
      let Al = async function() {
         let po2 = await videos()
         let po1 = await homev()
         console.log(po1, po2)
     }
    Al()
