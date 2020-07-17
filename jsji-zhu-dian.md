
 ## 前端工作 
 
   连接用户与后台，设计和实现UI交互；   
   小的方面考虑字体、色彩、布局；   
   大的方面从用户的整个操作流程上来优化交互体验。
 
 ## Js常用字典
 
  + html上展示html代码  
    `$('<div>').text(htmlCode).html(); `
    
    
  + js对象键值为数字时会自动从小到大排序
  
  
  + 随机数   
    Math.random().toString(radix); // radix使用2~36之间整数，默认为10，也就是随机0~9   
 	Math.random().toString(36); // 随机数36代表0~9个数字 + 26个英文字符   
 	
 	
  + 数组取值
    array.slice(x,y);  // 返回包含从起点开始，到终点之前所有元素的新数组   
    array.splice(x,y);  // 返回x开始y个元素新数组，并改变原数组，删除x开始y个元素   
    array.splice(x,y,parameter1,parameter2...);  // 返回x开始y个元素新数组，并改变原数组,在x处删除y个元素，并插入新的参数   
    array.filter((item,index,arr)=>arr.indexOf(item)===index);  // 数组去重   
  
  
  + 字符串取值  
    string.substr(start,length); // 返回一个从指定位置开始的指定长度字符串,如果length为0或负数，则返回'',如果没有指定length,则返回字符串本身。   
    string.substring(start,end); // 返回一个从start（包含）到end（不包含）的子字符串。   
 	注意：会使用start/end中较小值为起点，如果为NaN或负数则替换为0   
 
 
  + 监听输入
    element.on('input propertychange',function(){})
 
 
  + +'123'会被转换为123(int)
 
 
  + jquery根据多个属性选择$("element[name=''][value='']")
 
 
  + js性能测试   
    performance API     
    console.time  console.timeEnd
     
  + 创建文档碎片来离线升级节点信息
    document.createDocumentFragment();
    
  + 克隆更新dom
     var oldNode = document.getElementById('result'),
     clone = oldNode.cloneNode(true);
     // 处理克隆对象
     oldNode.parentNode.replateChild(clone,oldNode);
     

   
 ## 技术点
   
 + **eval和JSON.parse区别**：
 
   - JSON.parse只能解析属性名是双引号包裹的字符串对象（最后一个属性后不能有逗号）。 
   - eval函数，可以将一个js字符串求值成特定对象。   
     ``` 
     eval实例:
     var obj='{"a":1,"b":window.location.href="https://www.baidu.com"}';   
     eval("("+obj+")");   
     eval会将obj转换为json对象且跳转至www.baidu.com。
     ```
   - 为什么eval解析JSON字符串要加上括号？
    （1）json对象是以“{}”开始和结束，在js中会被当做一个语句块来处理。
    （2）加上括号为了将字符串转换为表达式，而不是语句（statement）来执行。  
   - 对象字面量{}，不加括号，eval会识别为js代码块的开始和结束标记，会被当成一个语句块来处理。   
     ```
     eval("{}");  // undefined;   
     eval("({})");  // object[object]
     ```
   - 勇哥提示：   
    （1）因为eval会有潜在的风险，比如：eval('window = null;')，  - _-   一个恶意代码毁你所有。
    （2）安全的方式：var obj = JSON.parse('{"property":"value"}');    
    （3）但是我们养成用 JSON.parse 替代 eval的习惯。可以避免出错。
    （4）使用JSON.parse，你的传参就必须简化为一个确定的对象。这样也符合《简化参数传递》的原则
 
 + **$.fn、$.extend()、$.fn.extend()**
   - jQuery.fn = jQuery.prototype 
   - jQuery.extend   
    （1）为jQuery添加方法  
      ```
      jQuery.extend({
         min:function(a,b){return a<b?a:b;}
         max:function(a,b){return a>b?a:b;}
      })
      ```
      （2）扩展对象并返回   
      ```
      jQuery.extend(target,object1,object2...)
      ```
   - jQuery.fn.extend(object)   
    对jQuery.prototype进行扩展，就是为jQuery类添加‘成员函数’。jQuery类的实例[$('#id')]可以使用这个‘成员函数’
        ```
        $.fn.tooltip = function(){}; 
        等价于
        var tooltip = {function(){}} / function(){}
        $.fn.extend(tooltip) = $.prototype.extend(tooltip) = $.fn.tooltip   
        ```
   
 + **代理与反向代理**
    - 背景
        跨域是由浏览器同源策略引起的，是指页面请求地址必须与页面url地址处于同域上(域名、端口、协议相同)。
        为了防止某域名下接口被其它域名下的网页非法调用，是浏览器对Js施加的安全限制。
    - 解决跨域问题常用解决方案（严重依赖后端）
        JSONP：利用script标签可跨域的特点，在跨域脚本中直接回调当前脚本的函数   
        CORS ：服务器设置HTTP相应头中Access-Control-Allow_origin值，接触跨域限制
    - 代理
    
 
 + **cookie的使用**
 
    - js 创建 cookie
        document.cookie = 'key=value';   
        // 设置过期时间（UTC/GMT）。默认情况下，cookie在浏览器关闭时删除。   
        document.cookie = 'key=value; expires='+new Date('2020/10/10');   
        // 设置path参数，告诉浏览器cookie的路径。默认情况下cookie属于当前页面。   
        document.cookie = 'key=value; expires=' + new Date('2020/10/10') + '; path=/';
    - js 获取 cookie
        document.cookie; // 多条数据间用  ; 和 空格  隔开
    - js 删除 cookie (只需设置expires为过期时间即可)   
        document.cookie = 'key=value; expires='+ new Date('2018/10/10');   
    - 获取GMT格式时间   
        new Date().toGMTString();
    - 获取UTC格式时间   
        Date.UTC(2019,1,23) // Date.UTC(year,month,day,hours,minutes,seconds,ms)  
    - cookie中的内容会被http请求默认添加至请求头中。
        若存在请求头中不存在新添加cookie，请检查cookie的Domain和path。   
        查看位置：chrome->Application->Storage->Cookie
        
        
 + **断点调试**

    - 条件断点调试
        断点处右键edit breakpoint,编辑条件（例：a===1）
        也可设置变量（例：var a = 1）
        
        
 + **数组方法**    
    
    -   
    
 + **for in / for of**
    
    - for of 是ES6新引入特性 遍历原型属性值  Object.values()
    - for in 遍历所有属性名称     Object.keys()
        
 + js检测脚本耗时
    - 启动计时器。 console.time('timeConsuming');
    - 停止计时器，并输出耗时。console.timeEnd('timeConsuming');
        