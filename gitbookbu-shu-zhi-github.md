**示例项目applets**

1、github创建项目applets（必须同时创建readme）

2、gitbook editor随便创建一个项目，项目会默认放置Import文件夹下

3、将github上项目clone至本地Import文件夹下

4、通过gitbook editor打开applets，编辑内容，并保存

方法一：

1、gitbook editor中内容编辑完毕，在cmd窗口中执行gitbook build

2、git bash中add 、commit 、 push

3、拉取新的分支 gh-pages

4、将gitbook build生成的\_book中内容拷贝置gh-pages分支根目录下，删除其它文件

5、add 、commit、push

6、打开页面[https://gdyu.github.io/applets/](https://gdyu.github.io/applets/) 即可访问

方法二：

1、本地applets文件夹下执行npm init，生成package.json文件，添加npm命令配置

"scripts":{

"build":"gitbook build ./ ./docs"

},

2、在applets文件夹下创建docs文件夹

3、执行npm run build

4、add 、commit、push

5、在github上applets项目的Settings中，将github pages的source由gh-pages branch修改为master branch/doocs folder

6、打开页面[https://gdyu.github.io/applets/](https://gdyu.github.io/applets/) 即可访问

问题：

1、菜单无法跳转。

E:\workCodes\book\Import\applets\\_book\gitbook\theme.js

搜索`if(m)for(n.handler，将m修改为false`

