# 翻墙工具
* Shadowsocks.exe 小飞机 
* SSTap-beta 人人翻墙 https://free.ssrbest.com/

# 编辑工具
      webstorm替换网址的正则表达式(https?:\/\/)(www\.).[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&\/\/=]*)
# js 的 IntersectionObserver API 使用教程
元素可见监听器
* 语法

      let io = new IntersectionObserver(callback, option);
      
* api

      io.observe(document.getElementById('example'));
      // 停止观察
      io.unobserve(element);
      // 关闭观察器
      io.disconnect();
* 回调函数参数entries 
   
      {
        time: 3893.92,//可见性发生变化的时间毫秒
        rootBounds: ClientRect { //根元素的矩形区域的信息
          bottom: 920,
          height: 1024,
          left: 0,
          right: 1024,
          top: 0,
          width: 920
        },
        boundingClientRect: ClientRect { //目标元素的矩形区域的信息
           // ...
        },
        intersectionRect: ClientRect { //目标元素与视口（或根元素）的交叉区域的信息
          // ...
        },
        intersectionRatio: 0.54, 目标元素的可见比例
        target: element //被观察的目标元素
      }


