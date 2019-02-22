# 一,	模块化开发
1，运用立即执行函数（）（）

		传入全局对象如：window，jQuery将立即执行函数中将数据向外暴露！window.foo=foo;
		
2,模块化引入

	1，commonJS规范运用
		通过 module.exports 语句来导出对象为模块
		module.exports = value；
		再通过 require 语句来引入
		var s=require(’文件地址‘)
		value为任意数据
			原理运用browserify解析与相关依赖的文件即打包，让require可以使用但是不能将ES6转义为ES5
			还要用 babel将ES6转为ES5
			命令：
				babel包安装：（babel是将ES6转为ES5的包）
				1.创建.babelrc文件{
					“presets”：[ //设定转码规则
					"es2015"
					(还有react , stage-2)
					],
					"plugins":[]
					}
				
				2.npm install --save-dev babel-cli 局部安装babel转码器
				3.npm install --save-dev babel-preset-es2015 安装转es2015的规则包
				4.转码命令
					babel 要转码的文件名 -o 输出的文件名  //单个文件转码
					babel 要转码的文件夹名 -d 输出的文件夹名  //整个文件夹转码
				
			由于浏览器不支持comonJs所以安装browserify
				npm instrall browserify -g
				全局安装browserify；
				npm instrall browserify --save-dev
				再本地安装browserify开发板！
				运行browserify 输入文件地址 -o 输出文件地址
	2，es6的规范使用
			向外暴露export value；
			引用 import {value} from '文件地址'
			{value}是ES6的对象解构
		模块化开发的流程ES6 - ES5  - 浏览器识别（打包）	
		
# 二，ES6语法
	1.let
	2.const
	3.箭头函数 
		（）=>console.log("a")
	4.模块化
	5.数据解构
	6.Promise
# 三，webpack使用
	1.webpackde 的单个文件的打包：webpack 打包文件 输出文件
	2.webpack.config.js配置
		module.exports={
			entry:''//(绳子头)所有关联文件的集合
		}，
		output:{
		path:__dirname+'/dist',//打包文件的路径
		filename;''//文件名
		}，
		module:{ //需要的工具包
			loaders:[
				{
					text:'//'
				}
			]
		}
		3.例如安装jQuery库打包库
		nom install jquery --save-dev
		4.在需要使用的地方直接var $=require（''jquery）;
		然后就可以用“$”了
		5.最后用：webpack命令进行编译后用：webpack命令进行编译
		6.将文件打包到服务端
			1.安装webpack-dev-server模块 npm insrall webpack-dev-server --save-dev
			2.package.json配置
				“script”:{ 
					"start"：“webpack-dev-server --entry 输入文件 --output-filename 输出文件”
					"build":"webpack --watch"//添加监听
				}
			3.启动webpack:npm run build;//和package.json中的build同名
			4.启动项目：npm start
# 四，vue的使用
## vue最常用的属性

* data:Vue 实例的数据对象
* components：Vue实例配置局部注册组件
* computed:计算属性
* watch：侦听属性
* filters：过滤器
* methods:Vue实例方法
* created：在实例创建完成后被立即调用，完成初始化操作
* mounted：el挂载到Vue实例上了，开始业务逻辑操作
* beforeDestroy：实例销毁之前调用
* props:用于接收来自父组件的数据
* template：组件模板
* render：渲染函数，创建虚拟DOM
		
1.v-on时当要获取原始的事件对象时用$event当实参传
2.局部注册组件

	 首先引入：import 组件的别名 form 组件路径,
	 然后注册：export default{
		components : {
			组件别名   //es6简写
		}
	}
	3.全局注册
		Vue.component('组件名'，{
			组件的字符串
			})
			
4.解决闪烁增加指令v-cloak
* 增加css[]

5.双向数据绑定的原理运用Object.defineProperty(Obj,key,{})监听Obj下的属性
		
	封装函数如下：
		function defineReactive (obj,key,val) {
        	Object.defineProperty(obj,key,{
		    enumerable: true,
		    configurable: true,
		    get: function () {
			return val;
			console.log('get')
		    },
		    set: function (newVal) {
			if(newVal === val || (newVal !== newVal && value !== value)){
			    return ;
			}
			val = newVal;
			console.log('set')
		    }
		});
	    }
	    
6.vue-router路由
* <router-view/>是存放变动的容器
* <router-link></router-link>相当于a标签，属性to跳转的模块
* 在router的文件下index.js配置路由引入相应的.vue文件
* 如：inpot Foot from '@/components/foot'
> 在routes数组中配置路由关系

	  {
	      path: '/', //路由路径
	      redirect: '/Tmain' //重定向的的路径
	      /*意思就是在地址栏输入www.qq.com时重定向到www.qq.com/Tmain*/
	    }, {
	      path: '/Tmain',
	      name: 'tmain',
	      component: Tmain //显示的模块
	    },
	    mode: 'history', //是否开启history模式
	  linkActiveClass: 'active' //当前的链接增加的class
    
# 五，css高级开发
1.css变量绑定

	  css：
		width: calc(var (--box-widyh,50)*1px);//--box-widyh变量名 50 变量默认值
	  js：
		//通过setProperty赋值给变量--box-watch
		document.documentElement.style.setProperty('--box-watch',this.value);
		//获取鼠标的相对位置
		document.querySelector(".button").onmousemove=funtion(e){	
		}
2.媒体查询注意事项

		当用最小宽度来分界时界限的书写规则只能从上到下依次增大！
		 例如：  @media (min-width: 1px){}
		 	@media (min-width: 768px){}
			@media (min-width: 992px){}
		 	@media (min-width: 992px）{}
			 （bootstrap的分界线）
	 界限的划分的规则min-width:768px的含义是在768px以上（包含768px）采用这个样式；
	 		max-width:767px的含义是在767px以下（包含767px）采用这个样式；
			
3.样式覆盖规则

	!important > 内联 > id > class （相同的选择器时style标签下的权限高于外部样式表，style下的相同样式的权限采取就近原则和定位越
	精确的权限就越高）
	
# 六,vue-cli安装
1. vue init webapck  //安装项目模板
2. npm install //安装依赖包
3. npm run dev //运行项目
4. npm run build 打包上线npm list name 查看插件name的版本
5. 安装jQuery，bootstrap

	1.安装各个包
		npm install jquery --save-dev //安装jQuery
		npm install bootstrap --save-dev //安装bootstrap
		npm view jquery versions //查看jQuery版本
	2.配置jQuery
		在build目录下webpack.base.conf.js
		开头引入webpack
		const webpack = require('webpack')
		在module.exports向外暴露加入
	  plugins: [
			new webpack.ProvidePlugin({
		  $: "jquery",
		  jQuery: "jquery",
		  "windows.jQuery": "jquery"
		})
	  ]
	3.引入bootstrap
		在程序入口app.js加入
		import 'bootstrap/dist/css/bootstrap.min.css'
		import 'bootstrap/dist/js/bootstrap.min.js'
			
# 七，Vuex使用
1.安装 npm insrall vuex --save
2.创建store.js

	1.引入vuex
		import Vue from 'vue'
		import Vuex from 'vuex'
		Vue.use(Vuex)
	2.实例化Vuex.Store对象
		new Vuex.Store()
	3.向外暴露
		export const store = new Vuex.Store({

		})
	4.挂在new Vue({store}
	
3.Vuex.Store构造函数的属性

	1.staict: true//开启严格模式
	2.state:{}//数据
	3.getters：{}//计算属性 //方法中默认接受的参数是state（ 数据）
	3.mutations：{}//方法 （注意：mutations中不能执行异步操作）//方法中默认
		接受state为第一个参数 可以传多个参数
	4.actions：{}//类似与mutations Action 提交的是 mutation，而不是直接变更状态。
		Action 可以包含任意异步操作。
		注册action  如increment (context) {
		context.commit('increment')
		}

4.在vue组件中使用

	1.在vue组件使用只能在计算属性中使用
		this.$store.state  //取到store中的数据
		this.$store.getters //取到store中的方法
	2.在vue组件中调用store中的getters中的方法
		在组件中新建方法不能用this.$store.mutations要采用this.$store.commt('方法名',[实参])
	3.调用actions如this.$store.dispatch('方法名',[实参])
# 八，canvas
	1.常用语法
		dom.getContext('2d')创建canvas执行上下文为2d对象
# 九，文件上传（图片）

1.ajax方式将数据放在FormData(form)对象中，js写的ajax：

  	    let xhr = new XMLHttpRequest()
            let formdata = new FormData($('#form')[0])
            xhr.open('post', 'http://127.0.0.1/weChet/upimg.php?id=1')
            xhr.onload = function () {
                if(xhr.responseText == 1){  //后台返回值判断
                    alert('上传ok')
                }
            }
            xhr.upload.onprogress = function (event) {  //文件上传进度检测
                //  console.log(event);
                let percent = event.loaded / event.total * 100 + '%';
                console.log(percent);
                // 设置 进度条内部step的 宽度
            }
            xhr.send(formdata) //发送
	    
2.文件上传预览

       	 运用FileReader()对象
	    let reader = new FileReader(); //实例化FileReader对象
            reader.readAsDataURL(files[0]) //设置文件源
            reader.onload = function () {  //实例化的对象加载完成后的回调函数
                let img = document.createElement('img')
                img.width = 50
                img.height = 50
                img.src = this.result      //实例化实例化对象的图片的地址（图片是base64位的图片格式）
                document.querySelector('.upimg').appendChild(img)
		
3.ajax跨域问题（cors）

        1.在请求页设置(php)
	
		header('Access-Control-Allow-Origin:*'); //设置允许访问的网站 * 统配 
		header('Access-Control-Allow-Methods:POST');//响应类型
		header('Access-Control-Allow-Headers:x-requested-with,content-type'); //响应头设置
		
	2.在请求页设置(node.js)
	
	 	//设置允许跨域请求
		app.all('*', function(req, res, next) {
		    res.header('Access-Control-Allow-Origin', '*'); //访问控制允许来源：所有
		    res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept'); 
		    //访问控制允许报头 X-Requested-With: xhr请求
		    res.header('Access-Control-Allow-Metheds', 'PUT, POST, GET, DELETE, OPTIONS'); //访问控制允许方法
		    res.header('X-Powered-By', 'nodejs'); //自定义头信息，表示服务端用nodejs
		    res.header('Content-Type', 'application/json;charset=utf-8');
		    next();
		}）;
		
	4.html5 自带表单验证setCustomValidity（）
	
		1.首先submit的条件是所有的表单的validity属性全部为fales才能提交成功
		2.绑定事件一般是oninput,onchange。
		例如：现在要判断用户修改密码时对用户进行错误提示
			window.onload = function () {
			    document.querySelector("input[name = 'new_password']").oninput = fn;
			}
			function fn() {
			    let poss1 = document.querySelector("#pa1").value
			    let poss2 = document.querySelector("#pa2").value
			    console.log(poss1,poss2)
			    if ($("#pa1").val() !== $("#pa2").val()) {
				document.querySelector("input[name = 'new_password']").setCustomValidity("两次密码不正确！");
			    } else {
				document.querySelector("input[name = 'new_password']").setCustomValidity("");
			    }
			}
			
# 十：js笔记：
##js常用的继承模式

		function Parent (name) {
		    this.name = name;
		    this.colors = ['red', 'blue', 'green'];
		}

		Parent.prototype.getName = function () {
		    console.log(this.name)
		}

		function Child (name, age) {

		    Parent.call(this, name);

		    this.age = age;

		}
		
		Child.prototype = new Parent();
		//constructor指向构造函数。因为Child.prototype = new Parent()会改变Child.prototype的constructor指向。
		Child.prototype.constructor = Child;

		var child1 = new Child('kevin', '18');

		child1.colors.push('black');

		console.log(child1.name); // kevin
		console.log(child1.age); // 18
		console.log(child1.colors); // ["red", "blue", "green", "black"]

		var child2 = new Child('daisy', '20');

		console.log(child2.name); // daisy
		console.log(child2.age); // 20
		console.log(child2.colors); // ["red", "blue", "green"]
## 操作提示框

              if(window.confirm('此操作不可逆，是否确认？')){
	      
	      }
	      
## js去除空格

	str为要去除空格的字符串:
	去除所有空格:
	str   =   str.replace(/\s+/g,"");
	去除两头空格:
	str   =   str.replace(/^\s+|\s+$/g,"");
	去除左空格：
	str=str.replace( /^\s/, '');
	去除右空格：
	str=str.replace(/(\s$)/g, "");
	
## js获取url的参数值

	let reg = new RegExp("(^|&)" + key + "=([^&]*)(&|$)", "i"),
	r = window.location.search.substr(1).match(reg),a = r[2]

		
# 十一.jq事件监听

 * on注册一个永久监听事件,
 * off用.on()绑定的事件处理程序，
 * bind调试绑定多个事件，
 * one为每一个匹配元素的特定事件（像click）绑定一个一次性的事件处理函数。
 # 十二.nuxt.js
 
* 每一个pages目录下的vue就是一条路由，
* 动态路由在文件名前面加‘_’,每次配置nuxt,config.js都要重启项目。
* 中间件不能再页面组件及components文件夹下的.vue文件，
* nuxt.config.js配置中间件在router下配置，
* pages与layouts直接配置。

