###AngularJs的生命周期分为六个阶段：

+ 编译。
    - AngularJs会遍历浏览器提供的dom树，尝试参照已注册的指令集来匹配每个元素、属性、注释和css类。
    - 每当匹配一个指令时，ag就会调用该指令的编译函数，该函数返回一个连接函数，ag会收集所有的连接函数。
    
+ 链接。
    - 一旦所有指令被编译完成，AngularJs就会创建作用域，然后通过调用每个指令对应的链接函数将指令和作用域连接起来。
    
+ 注册监视。
    - 作用域一旦生成，指令就会在它身上注册一个监视，就是我们平时用到的$scope.$watch()，顾名思义监视数据有没有变化。
    
+ 模型变化。
    - 这个时候一旦模型发生了变化，会执行用户自己定义的回调函数。其中关键的是，在模型发生变化时，如何从浏览器的js环境进入到angular的环境中操作在ag模型上的数据，此时，ag会调用一个内置指令$scope.$apply，这样就能进去ag的环境。
    
+ 观察。
    - 在这个阶段会启动脏检测机制，先检测根scope，然后传播到所有的子作用域上，这个时候检测到变化就会执行监听函数$watch的回调函数。
    
+ 摧毁。
    - 当我们不需要一个作用域，需要将它移除掉。原则是谁创建的谁摧毁，使用的方法是$scope.$destroy()。