# 示例项目applets

+ github创建项目applets（必须同时创建readme）

+ gitbook editor随便创建一个项目，项目会默认放置Import文件夹下

+ 将github上项目clone至本地Import文件夹下

+ 通过gitbook editor打开applets，编辑内容，并保存

### 方法一：

+ gitbook editor中内容编辑完毕，在cmd窗口中执行gitbook build

+ git bash中add 、commit 、 push

+ 拉取新的分支 gh-pages

+ 将gitbook build生成的\_book中内容拷贝置gh-pages分支根目录下，删除其它文件

+ add 、commit、push

+ 打开页面[https://gdyu.github.io/applets/](https://gdyu.github.io/applets/) 即可访问

### 方法二：

+ 本地applets文件夹下执行npm init，生成package.json文件，添加npm命令配置
``` js
"scripts":{
    "build":"gitbook build ./ ./docs"
}
```

+ 在applets文件夹下创建docs文件夹

+ 执行npm run build

+ add 、commit、push

+ 在github上applets项目的Settings中，将github pages的source由gh-pages branch修改为master branch/doocs folder

+ 打开页面[https://gdyu.github.io/applets/](https://gdyu.github.io/applets/) 即可访问

### 问题：

+ 菜单无法跳转。
    - E:\workCodes\book\Import\applets\\_book\gitbook\theme.js
    - 搜索`if(m)for(n.handler，将m修改为false`

+ [https://gdyu.github.io/applets/](https://gdyu.github.io/applets/) 访问404了
    - 需等待几分钟

