+ 编码规范
    - 为方便调试，函数要么始终返回一个值，要么永远都不返回值。
    
+ 性能优化
    - 管理内存
        - 解除引用。优化内存占用的最佳方式，就是为执行中的代码只保留必要的数据。一旦数据不再有用，通过将其值设置为null来释放其引用。
           这一做法适用于大多数全局变量和全局对象的属性。局部变量会再他们离开执行环境时自动被解除引用。
        
+ toString()、toLocalString()和String()  

    - toString()  
        可以传参：输入数值的技术。默认情况下以十进制格式返回数值的字符串表示。  
        null和undefined没有这个方法  
    ```js
        var num = 10;
        num.toString(2); // "1010"
    ```    
    
    - toLocalString()
        dateObject.toLocalString() // 把时间对象转换为字符串
    ```js
        new Date().toLocaleString()  //"2019/9/16 下午7:26:49"
    ```
    
    - String()  
        可将任何类型的值转换为字符串，包括null和undefined。  
        如果值有toString()方法，则调用该方法；  
        如果值为null，则返回"null"；  
        如果值为undefined,则返回"undefined"。  
 
    
+ object 类型  

    - Object 的每个实例，都具有下列属性和方法：  
    ```
                           constructor:保存着用于创建当前对象的函数。
          hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中（而不是实例的原型中）是否存在。
                 isPrototypeOf(object):用于检查传入的对象是否是当前对象的原型
    propertyIsEnumerable(propertyName):用于检查给定的属性是否能够使用for-in语句来枚举。
                      toLocaleString():返回对象的字符串表示，改字符串与执行环境的地区对应。
                            toString():返回对象的字符串表示。
                             valueOf():返回对象的字符串、数值或布尔值表示。通常与toString()方法返回值相同。
    ```


+  for循环和break、continue  （label语句搭配for循环，可以跳出多重循环语句）                            
    - break 会完全退出循环，执行for循环后面的语句。
    - continue 会退出当前循环，继续下一个循环。
    ```js
    // 实例：语句中break会中断最外层for循环
    labelName:
    for(var i=0;i<10;i++){
       for(var j=0;j<10;j++){
           for(var m=0;m<10;m++){
               if(i===5&&j===5&&m===5){
                   break labelName;
               } 
           } 
       }
    }
    ```  


+ 基本类型值、引用类型值
    - 基本类型值。指的是简单的数据段
        - 5种基本数据类型：Undefined、Null、Boolean、Number、String。这5种基本数据类型是按值访问的，因为可以操作保存在变量中的实际值。
        - 基本类型值，在内存中占据固定大小的空间，因此被保存在栈内存中。
        - 从一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本。
    
    - 引用类型值。指的是由多个值构成的对象
       - 引用类型的值是保存在内存中的对象。JavaScript不允许直接访问内存中的位置，操作对象时，实际上是在操作对象的引用。引用类型的值是按引用访问的。
       - 引用类型的值是对象，保存在堆内存中。
       - 包含引用类型值的变量实际上包含的并不是对象本身，而是一个指向该对象的指针。
       - 从一个变量向另一个变量赋值引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象。 
    
       
+ typeof / instanceof
    - typeof可以检测：基本数据类型中undefied/string/number/boolean，(typeof null==='object')
    
    - instanceof 可检测：Object/Array/RegExp。([] instanceof Array)===true 
    
    
+ 声明变量
    - 使用 var 声明的变量会自动添加到最接近的环境中。在函数内部，最接近的环境就是函数的局部环境。
    - 如果初始化变量时，没有使用var声明，该变量会自动被添加到全局环境。
    

+ zoom scale 区别
    - zoom:0.5;/transform:scale(0.5);
    - 渲染性能差异明显。zoom缩放会改变元素的真实空间大小，可能会引起整个页面的重新渲染。
    - zoom的缩放是相对于左上角，scale的缩放是居中缩放
    - zoom缩放文字依然受限于最小12像素，scale不受限
    - scale可以为负数，为负数时翻转并缩放。
    - ElementUI中scale实现zoom效果原理：
        scale效果加在div上，div中嵌套iframe，内容放置iframe中显示
    
    
+ 数组的length属性

    - length属性
        - 从数组末尾移除项 
            var arr = [1,2,3];
            arr.length=2;
            arr[2]===undefined;
        - 从数组末尾增加项
            var arr = [1,2,3];
            arr.length=4;
            arr[3]===undefined;
    
    - 获取方法 pop()/shift()、
        - pop() // 数组最后一项
        - shift() //数组第一项
        
    - 添加方法push()/unshift()    
        - push() // 添加到数组末尾
        - unshift() // 添加到数组开头
        
    - 排序方法
        - reverse() // 翻转数组
        - sort() // 默认按升序排列【每项都调用toString()转型方法，然后比较得到的字符串，即使每一项都是数字】
        ```js
          // 从小到大[升序]
          var arr = [1,2,3];
          arr.sort(function(a,b){
              if(a>b){
                return 1;           
              }
              else if(a<b){
                  return -1;
              }else{
                  return 0;
              }
          })
        ```
    
    - 位置方法
        - indexOf() // 从前往后找
        - lastIndexOf() // 从后往前找
     
    - 迭代方法
        - every()  // 函数每一项都返回true,则返回true
        - filter()  // 返回函数 return true的项组成的数组
        - forEach()
        - map()
        - some()  // 函数存在一项返回true的，则返回true
    
    - 归并方法
        - reduce() // 从数组第一项开始
        - reduceRight()  // 从数组最后一项开始
        - 接收函数的4个参数：前一个值、当前值、项的索引、数组对象
        
+ Date类型
    - Date.parse() // 返回时间毫秒数 例如：Date.parse('2019.09.05 20:14')
    - Date.UTC()   // 返回UTC时间（正常时间小时数减8）毫秒数 例如：Date.UTC(2019,9,5,12,14)
    - Date.now()  // 返回调用这个方法时日期和时间的毫秒数，在不支持的浏览器中可使用 +new Date(); 效果一样
    
+ 日期的格式化方法
    - toDateString()  // 星期几、月、日、年
    - toTimeString()  // 时、分、秒、时区
    - toLocaleDateString()  // 星期几、月、日、年
    - toLocaleTimeString()  // 时、分、秒
    - toUTCString()  // 完整的UTC日期


+ RegExp类型
    - 3个标志
        - g  // 全局模式
        - i  // 不区分大小写
        - m  // 多行模式

+ 函数内部属性
    - arguments
        - arguments.callee  // callee属性是一个指针，指向拥有这个arguments对象的函数  
        【用到递归算法时，上面的属性可避免函数名称不固定，导致函数内部调用方法名错误】
        【严格模式不支持】

        - arguments.callee.caller/functionName.caller  // 保存着调用当前函数的函数的引用
        【如果在全局作用域中调用当前函数，它的值为null】

+ Number 类型提供数值格式化方法
    - toFixed
    - toExponential  // e表示法 var num=10;num.toExponential(1); 1.0e+1
    - toPrecision // 根据数值判断哪种格式合适就用哪种

+ String 类型
    - chatAt() // 返回给定位置字符 'abc'.chatAt(1);'b';
    - chatCodeAt() // 返回给定位置字符的字符编码
    - 方括号+数字索引访问字符 // var str='abc';str[1];'b';
    - slice(p1,p2) // p1:字符串开始位置（为负数时，倒着数），p2:字符串结束位置[包头不包尾]
    - substring(p1,p2) // p1:字符串开始位置，p2:字符串结束位置[包头不包尾]
    - substr(p1,p2) // p1:字符串开始位置，p2:字符串长度
    - toLowerCase()/toUpperCase() 
    - toLocaleLowerCase()/toLocaleUpperCase() // 推荐用法。针对特定地区的实现。少数语言会为Unicode大小写转换应用特殊的规则。
    - localeCompare() // str.localeCompare(str1); 比较字符串与字符参数在字母表中的排序，字符串大则返回1；小返回-1
    - String.fromCharCode() // 将多个字符编码转换为字符串 String.fromCharCode(104,101,108,108,111);'hello';
    
+ Html转码
    ```js
      function htmlEscape(text){
          return text.replace(/[<>"&]/g,function(match,pos,originalText){
            switch(match){
              case "<":
                return "&lt;";
              case ">":
                return "&gt;";
              case "\"":
                return "&quot;";
              case "&":
                return "&amp;";
          }
        })
    }
    ```

































