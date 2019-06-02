git 不能committed出现warning: LF will be replaced by CRLF输入git config core.autocrlf false
# vue学习笔记
## vue-cli3.0生成项目
  vue create 项目名
## vue的属性
* data(){}//数据
* props: [] //父传子接受的值
  注意：要么传，都么不传，当出现中间的情况的时候用计算属性裁解决，不要写默认值
* computed: {}//计算属性
* methods: {}//方法


## vue的生命周期
* <img src="https://cn.vuejs.org/images/lifecycle.png" />

## nuxt跨域（nuxt.config.js）配置


    server: {
      port: 3121, // default: 3000
      host: '192.168.0.195', // default: localhost
    },//设置启动端口
    modules: [
      ['@nuxtjs/axios', {
      //设置axios的相对路径的端口，因为页面的axios请求的路径都是相对路径，由于页面跳转的时候是发起的前台的ajax请求，而页面加载受后端发起的http请求
        baseURL: 'http://127.0.0.1:3121'
      }],
      '@nuxtjs/proxy',
    ]
    proxy: {
    ////前端发起的带/api的请求代理到这个地址上，即api的端口号
      '/api': {
        target: 'http://127.0.0.1:3120',
        pathRewrite: {
          '^/api' : '/'
        }
      }
    }
  
  ## vue插件开发 npm包开发
  
     1.package.json 配置
        {
         "name": "vue-quill-img-editor", // 引入包时的名称
          "main": "dist/vue-quill-img-editor.js", // 引入包时对应的文件
        }
     2. webpack，babel配置
        
