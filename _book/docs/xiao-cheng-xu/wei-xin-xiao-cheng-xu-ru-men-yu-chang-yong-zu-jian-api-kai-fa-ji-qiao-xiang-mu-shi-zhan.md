## 将要实现的小程序
+ 娜娜收卡
+ 花店
+ 剪发
+ 阮家
+ 抖音广告
+ 收租

## 小程序的特点
+ 小程序适合做简单的、用完即走的应用
+ 小程序适合低频的应用
+ 小程序适合性能要求不高的应用
+ 安装包<1MB
+ 对比传统APP
    - 传统APP 体验差成本高
    - 小程序 流程简单 跨平台

## 其它
+ B2C （人与商品）淘宝、京东
+ P2P （人与人）微信、QQ
+ C2P （人与服务）小程序

## 重要更新
+ 专栏地址   
    - https://zhuanlan.zhihu.com/oldtimes
+ 微信小程序122100版本分享、二维码功能解析 
    - https://zhuanlan.zhihu.com/p/24498136

## 微信小程序开发工具
+ 断点调试 F10跳过所有断点；F8下一个断点。
+ F1打开命令面板

## 其它知识点
+ mustache语法
    - mustache 模板，用于构造html页面内容。在实际工作中，当同一个模板中想要调用不同的函数来渲染画面，在已经自定义好了的前提下，可以在渲染页面时对传入的参数进行手动判断。
    - Mustache 的模板语法很简单，就那么几个：
    
+ 原码、反码、补码
```
[+1] = [00000001]原 = [00000001]反 = [00000001]补
[-1] = [10000001]原 = [11111110]反 = [11111111]补
1-1 = 1 + (-1) = [0000 0001]原 + [1000 0001]原 = [0000 0001]补 + [1111 1111]补 = [0000 0000]补=[0000 0000]原
```

## 第一个小程序
+ 文件类型和目录结构
+ 注册小程序页面
+ View、Image、Text等组件基本用法
+ Flex弹性盒子模型
+ 移动端分辨率及小程序自适应单位RPX

+ 移动设备分辨率与rpx
    - pt 逻辑分辨率
        * pt的大小和屏幕尺寸有关系。长度和视觉单位。
    - px 物理分辨率   
    - pt包含px 
+ 移动设备的分辨率与rpx（ip6 => iphone6）
    - 以ip6的物理像素750*1334为视觉稿进行设计，而在小程序中使用rpx为单位
    - ip6下1px = 1rpx = 0.5pt
    - 使用rpx，小程序会自动在不同的分辨率下进行转换，而使用为单位则不会
    - 为什么要用ip6的物理分辨率来做设计图
        * ip6下1px = 1rpx
        * ip6 plus下1px = 0.6rpx
    - ip6 下设计师的设计图为什么试试750*1334
        * ip6逻辑分辨率 375*667
        * ip6下，逻辑分辨率：物理分辨率  1:2（ip6 plus 是1:3）
        * 视网膜屏 2个像素点已经达到人眼极限
        
    - PPI怎么来的
        * ip6 物理分辨率 750*1344
        * ip6 屏幕尺寸 4.7
        * PPI = 750*750+1344*1344 = (326 *4.7)*(326*4.7)
   
+ 标签
    - text
        * 文本不用text标签也能显示
        * 小程序中，只有用text标签包裹的文字，才能长按选中
        * text标签可以嵌套text标签
        * text标签中添加\n 会换行

+ 首页添加全屏背景色
    - 首页背景色设置
        * 当前页最外层view设置固定高度和100%都不可取。（固定高度，存在滚动条就有问题）
        * 小程序最外层有一个page标签，添加样式height:100%;background-color:颜色
    - 顶部导航颜色设置（查看小程序api文档）
        * app.json中window 属性中添加"navigationBarBackgroundColor":颜色
        * 每个详情页可以单独设置顶部颜色，直接在.json文件中添加"navigationBarBackgroundColor":颜色。
        无需外层window

+ Swiper组件
+ 组件
    - 遍历
        * wx:for 
        * wx:for-item 
        * wx:for-index
+ 事件
    - 编写小程序时，出现事件触发两次的bug，需完全关闭小程序编写软件，再次打开可修复
    
+ js操作
    - data赋值。this.setData({key:value})
    - 页面跳转。wx.navigateTo({url:""})。路径为具体页面路径，无后缀
    - navigateTo/redirectTo/switchTo区别
        * navigateTo 页面可返回，原页面只是被hide
        * redirecTo 页面被关闭
    - 模拟数据设置
        * module.exports ={}
        * require 相对路径引入
    - template使用
        * template文件wxml wxss
        * 页面引入import相对路径，template标签 is 对应 name 
        * 页面wxss需@import 模板的样式，否则不生效

+ 页面传参
    - data={...item} // ...表示展开对象[需用花括号包裹]
    - data-post-id 自定义属性，取值e.currentTarget.dataset.postId


















