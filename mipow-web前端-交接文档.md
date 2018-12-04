## 职位职责
1. [负责官网的新品上架](#一-新品上架)
3. [负责官网活动](#二-官网活动页面的制作)
3. [官网的图片替换](#三-官网的图片替换)
4. [负责官网的维护](#四-负责官网的维护)

## 一. 新品上架
1. 要准备的东西
    * 产品详细页面 （Description）
    * 产品的细节图片800*800 （Images）
    * 首页的轮播图
    * 首页的 NEW ARRIVALS 两张图
2. 操作步骤
    1. 进入后台
    2. 进入All products 栏目 点击Add product
    3. 填写 Title, Description
    4. 上传导航栏的一张图片800*800，并将图片上的Alt设为nev
    5. 上传产品的细节图800*800，并将图片上的Alt设为color或者size或者other
    6. 上传首页的2张新品图片700*640，图片命名为new-hover与new-active（如果此产品不在首页的NEW ARRIVALS处展示，可以省去这一步）
    7. 设置Pricing或者Variants
    8. 可以编辑此产品页面的Search engine listing preview ，默认是自动生成的（此页面的seo）
    9. 可以设置产品的可见性Product availability（默认是全部可见的，如果是测试页面，记得将这个栏目下的所有选项关掉，不然搜索引擎会录取）
    10. 设置Vendor，此处的文本对应的是导航栏处的产品描述
    11. 设置产品所属的集合,这个很重要。常用的集合是导航栏上的 Living, Playbulb, Chargers， Distribution，首页上的一个新品集合 NEW ARRIVAL 还有SELECTIONS模块下的多个集合
    12. 设置选择页面的模板Theme templates。
    13. 替换轮播图，电脑端的轮播图在进入 OnlineStore -> Customize -> Home page - hero slideshow替换掉相应的图片和连接。替换手机端的图片首先在Settings -> files 上传图片，拿到图片链接后进去
        Online Store -> Actions -> Edit code 页面找到 home-hero.liquid文件，你会看到5个类型下面的代码片段，你需要找到你要替换的图片，换成你刚刚复制的图片链接，a标签的链接缓存对应的产品链接。

            <div class="swiper-slide">
                 <img src="https://cdn.shopify.com/s/files/1/1268/0357/files/20181201151801.jpg?14021924991585366913" style="width:100%">
                <a href="/products/power-cube-x2" class="btn hero__cta">
                Shop Now <span class="icon icon-arrow-right" aria-hidden="true"></span>
                </a>
            </div>

## 二 官网活动页面的制作
1. 单纯的产品集合打折页面 新建一个集合在Products -> Collections -> Create collections
    * 填写Title
    * 填写Description (optional)页面的内容
    * 保存Save
    * 添加产品
2. 内容营销页面 新建一个page页面 Online Store -> Pages -> Add page
    * 填写 title
    * 填写 页面的主体内容
    * 选择模板
## 三 官网的图片替换
1. media kit页面图片
    * 在mediakit.liquid文件中对应的对方增加代码！
2. 集合页面的轮播图
    * 在对应的产品集合页面的模板页面文件
## 四 负责官网的维护
1. POWER CUBE X2页面的倒计时到这月的14号到期，到时候将这个活动下架，就是将这个产品页面的模板换成 product.wu-style-product
2. 官网首页的主体内容在 featured-collections.liquid 文件中
3. shopify使用的是Liquid模板引擎官方教程的网址 https://help.shopify.com/en/themes/customization
4. 导航栏的编辑在 Online Store -> Navigation