# 关联概要

* 网站：极客时间
* 地址：https://time.geekbang.org/column/intro/100039701?utm_campaign=guanwang&utm_source=baidu-ad&utm_medium=ppzq-pc&utm_content=title&utm_term=baidu-ad-ppzq-title

* 课时记录


# 课程内容

* 概要内容

    + **从零开始** 主要讲述构成JavaScript语言的基础——JavaScript语言的静态结构，主要包括词法环境、块级作用域、语句、声明、字面量、变量环境、模块（名字空间）等等。

    + **从表达式到执行引擎** 主要讲述JavaScript的执行过程，主要包括执行栈、执行队列、执行上下文、函数（函数对象/闭包）作为执行结构如何参与运算等等，还将讲述表达式（运算符+操作数）与优先级这个体系，说明表达式运算与语句运算间的不同。

    + **从原型到类** 主要讲述JavaScript面向对象编程体系中最核心的一些设计，包括类继承、原型继承、属性表的使用、内部方法等等，并对索引数组和关联数组在JavaScript中的应用与整合做深度分析。

    + **从粗通到精通的进阶之路** 主要讲述JavaScript作为动态语言的主要特性，包括动态的类型、动态的执行过程和动态的环境上下文等等。
    
* 作者知识点
    + JavaScript 主要包括 5 个方面的语言特性：结构化编程、面向对象编程、动态语言、函数式语言和并行语言

    + 表达式的值，在 ECMAScript 的规范中，称为“引用”。
    + delete x
        - 是删除 x 这个成员，而不是删除 x 这个值。不过终归有一点是没错的：既然没办法表达异常，而 delete 0 又不产生异常，那么它自然就该返回 true。
        - 如果x是值，则按照传统的 JavaScript 的约定返回 true；
        - 如果x是一个引用，那么对该引用进行分析，以决定如何操作。
        - delete 这个操作的正式语法设计并不是“删除某个东西”，而是“删除一个表达式的结果”
        - undefined是一个全局属性，而null是一个关键字。
        - 由于undefined是全局属性，所以`delete undefined`其实就是`delete global.undefined`，是删除引用，而不是删除值。而这个属性是只读的，所以就返回false了。
        
        - delete 运算符尝试删除值数据时，会返回 true，用于表示没有错误（Error）。
        - delete 0 的本质是删除一个表达式的值（Result）。
        - delete x 与上述的区别只在于 Result 是一个引用（Reference）。
        - delete 其实只能删除一种引用，即对象的成员（Property）。
    
    + var x=y=100
        - let x // 声明变量 x。不可在赋值之前读。(x is not defined)
        - var x // 声明变量 x。在赋值之前可读取到 undefined 值。
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    