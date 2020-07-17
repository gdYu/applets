主要讨论以下三种模式：   
    设计模式
    编码模式
    反模式(错误的模式)


设计模式范例主要包括：
    singleton // 单例
    factory  // 工厂
    decorator  // 装饰
    observer  // 观察者


对象主要有两种类型：
    原生的（Native） 
        内置对象 （Array/Date）
        自定义对象 （var o = {};）
    主机的（Host）在主机环境中定义的（例如浏览器环境）
        windows对象
        DOM对象

原型（prototypes）
    原型是一个对象，创建的每一个都会自动获取一个prototypes属性，该属性指向一个新的空对象。
    该对象几乎等同于采用对象字面量或Object()创建的对象，区别在于它的constructor属性指向了所创建的函数，而不是指向内置的Object函数。


DOM 文档对象模型(Document Object Model)。代表着被加载到浏览器窗口里的当前网页。
BOM 浏览器对象模型(Browser Object Model),BOM的最根本对象是window。`[例如:打开新窗口、打开新选项卡、关闭页面、把网页设为主页、加入收藏夹...这些涉及到的对象就是BOM]`

console.dir  枚举传递过来的对象，并打印出所有属性

基础知识：
    从右至左的操作符优先级。
    变量的声明会提升到函数的最顶层。

优化建议：
    DOM操作非常耗时，尽可能做缓存处理
    内存节点片段：document.createDocumentFragment()
    不要增加内置原型属性（Object()/Array()/Function()...） // 可能严重影响可维护性

JSLint
  网址：http://jslint.com
  nomen: false // 去掉下划线前缀警告
  

代码规范：
    应该一直使用大括号并将开发的大括号放置在前面语句的同一行
    ```
    // 错误写法，返回undefined
    function func(){
      return
      {
        name:'test'
      };
    }
    // 正确写法,返回对象
    function func(){
      return {
        name:'test'
      };
    }
    ```
    应该一直使用分号，甚至JavaScript解析器会隐式增加。
    命名约定
        构造函数首字母大写 var adam = new Person();
        
 
推荐书籍：
《High Performance JavaScript by Nicholas Zakas》(O'Reilly)

for循环优化
for(var i=0;i<myArray.length;i++){}  =>  for(var i=0,max=myArray.length;i<max;i++){}

确认不了对象内容时，最好加上hasOwnProperty过滤条件
```
var man = {hands:2};
if(typeof Object.prototype.clone==="undefined"){
  Object.prototype.clone = function(){};
}

// 方式一
for(var i in man){
  if(man.hasOwnProperty(i)){
    console.log(i,":",man[i]);
  }
}

// 方式二
(function(){
  var i,hasOwn=Object.prototype.hasOwnProperty;
  for(i in man){
    if(hasOwn.call(man,i)){
      console.log(i,':',man[i]);
    }
  }
})()
```

switch模式
    避免使用 fall-throughs (有意不适用break语句，使得程序会按顺序一直向下执行)

避免使用隐式类型转换，比较语句时使用===和!==

避免使用eval()。
①如果一定需要使用eval()，可以考虑使用new Function()来替代。new Function()中的代码将在局部函数空间中运行
②将eval()调用封装到一个即时函数中
```
    以下只有un这个变量仍然是一个全局变量
    var jsstring = 'var un=1;console.log(un);';
    eval(jsstring);   
    
    jsstring = 'var deux=2;console.log(deux);';
    new Function(jsstring)();   
    
    jsstring = 'var trois=3;console.log(trois);';
    (function(){
        eval(jsstring);
    })();
    
    console.log(typeof un);
    console.log(typeof deux);
    console.log(typeof trois);
```

Number() 和 parseInt() 区别
Number()比parseInt()快很多，因为parseInt是解析而不是简单的转换。
parseInt('08 hello')会返回数值，其它的方法都会失败并返回NaN。
ECMAScript 3中 parseInt('08'),08会被当做八进制处理parseInt('08',8)，结果为0。最好带上第二个参数parseInt('08',10);ECMAScript 5中不存在该问题

常用的几种对象创建模式

    使用 new 关键字创建 （基础创建）
        var gf = new Object();
        gf.name = 'test';
        gf.say = function(){
          console.log(this.name);
        };
        
    使用字面量创建
        var gf = {
          name:'test',
          say:function(){
            console.log(this.name);
          }
        }
        
    工厂模式 （批量生产）
        function createGf(name){
          var o = new Object();
          o.name = name;
          o.say = function(){
            console.log(this.name);
          }
        }
        
    构造函数 （可区分对象具体类型）
        function Gf(name){
          this.name = name;
          this.say = function(){
            console.log(this.name);
          }
        }
        
    创建多个实例，调用的 say 方法不是同一个Function实例
        function Gf(name){
          this.name = name;
          this.say = say;
        }
        function say(){
          console.log(this.name);
        }
        
    // 定义成具备封装性的对象
    // 原型模式，不必再构造函数中定义实例属性，可以将属性信息直接赋予原型对象
        function Gf(){
          Gf.prototype.name = 'test';
          Gf.prototype.say = function(){
            console.log(this.name);
          }
        }
        
    // 此处 constructor 属性不再指向对象 Gf ,因为每定义一个函数，就会同时为其创建一个 prototype 对象，这个对象也会自动获取一个新的constructor属性，这里使用Gf.prototype覆写了原有的prototype对象，因此constructor指向Object
        function Gf(){}
        Gf.prototype = {
          name:'test',
          say:function(){
            console.log(this.name);
          }
        }
        
    // 如果对 constructor 有特殊需求，可以显示指定 Gf.prototype 的 constructor 属性
        Gf.prototype = {
          constructor:Gf,
          name:'test',
          say:function(){
            console.log(this.name);
          }
        }
        
    // ☆☆☆☆☆
    // 实际开发中，可以使用构造函数来定义对象的属性，使用原型来定义共享的属性和方法，这样就可以传递不同的参数，来创建出不同的对象，同时又拥有了共享的方法和属性
        function Gf(name,bar){
          this.name = name;
          this.bar = bar;
        }
        Gf.prototype = {
          constructor:Gf,
          say:function(){
            console.log(this.name);
          }
        }
        
使用Object构造函数创建对象，与使用字面量创建对象区别
    // 字面量
    var car = {name:'fast'};
    // 构造函数
    var car = new Object();
    car.name='fast';
    ①字面量模式需要输入字符更短；
    ②字面量模式强调对象仅是一个可变哈希映射，而不是从对象中提取的属性或方法；
    ③自面量没有作用域的解析。而Object构造函数，可能一同样的名字创建了一个局部构造函数，解释器需要从调用Object()的位置开始一直相差查询作业域链，直到发现全局Object构造函数。
   
    
new Object()构造函数的‘特征’(或者说另一个不使用构造函数的原因)
Object()仅接受一个参数，并且还依赖传递的值，该Object()可能会委派另一个内置构造函数来创建对象，并且返回了一个并非期望的不同对象。
```
var o = new Object();
o.constructor === Object; // true

var o = new Object(1);
o.constructor === Number; // true
o.toFixed(2); // 1.00    

var o = new Object('I am string');
o.constructor === String; // true

var o = new Object(true);
o.constructor == Boolean; // true
```
    
可重用的成员，都应该放置到对象的原型中。

自调用构造函数
// 在构造函数中检查this是否为构造函数的一个实例，如果不是，则调用自身（防止用户调用时遗漏 new 关键字，从而导致实例创建不成功）
function Waffle(){
    if(!(this instanceof Waffle)){
        return new Waffle();
    }
    this.state = 'test';
}
Waffle.prototype.want = true;

// 另一种用于检测实例对象的通用方法是将其与arguments.callee进行比较，而不是在代码中硬编码构造函数名称。
// 每个函数内部，当该函数被调用时，将会创建一个名为arguments的对象，其中包含了传递给该函数的所有参数，同时，arguments对象中有一个名为callee的属性，该属性会指向被调用的函数。
// 注意：在ES5的严格模式中，不支持arguments.callee属性。
if(!(this instanceof arguments.callee)){
    return new arguments.callee();
}


数组构造函数的特殊性
var a = new Array(3); // 将返回长度为3，内容为undefined的数组`[empty*3] a[0]=undefined`
var white = new Array(3).join('1');// 11 注意，join只会加在数组中间，所有只有两个1

ECMAScript5定义了一个新方法Array.isArray(),该函数在参数为数组时返回true
Array.isArray([]);// true
如果当前环境无法使用Array.isArray(),可以通过调用Object.prototype.toString()方法对其检测
if(typeof Array.isArray=== 'undefined'){
  Array.isArray = function(arg){
    return Object.prototype.toString().call(arg) === '[object Array]';
  }
}


JavaScript库 YUI3

正则表达式
g  全局匹配
m  多行
i  兼容大小写

调用RegExp()，不使用new的行为与使用new的行为是相同的

JavaScript五个基本的值类型：Number、String、Boolean、null、undefined。除了null和undefined以外，其它三个都有所谓的基本包装对象。可以使用内置构造函数Number()...创建包装对象。

charAt()返回指定位置的字符（从0开始）
charCodeAt()返回指定置未字符的Unicode编码。返回值是0-65535之间的整数。

var a =1234;
NumberObject.toFixed(num); num位于0~20,省略num则用0代替。
a.toFixed(2); // 1234.00

NumberObject.toExponential(num); num位于1~20之间,将数字转换为指数计数法  
a.toExponential(2); // 1.23e+3 

NumberObject.toPrecision(num); 在值超出指定位数时将其转换为指数计数法。num位于1~21之间，如果省略则调用toString()。
a.toPrecision(2); // 1.2e+3 将数字转换为指数计数法  

自定义错误对象
```
try{
  throw{
    name:'MyErrorType',
    message:'oops',
    extra:'this was rather embarrassing',
    remedy:genericErrorHandler
  };
  console.log('try');
}catch(e){
  console.log(e.message);

  e.remedy();
}

function genericErrorHandler(){
  console.log('save log');
}
```

①function add(){}           // 函数的声明
②var add = function(){}     // 函数表达式     （函数对象的name属性为空字符串）
③var add = function add(){} // 命名函数表达式 （函数对象的name属性为'add'）

回调与作用域
var myapp = {}
myapp.color = 'red';
myapp.paint = function(){
  console.log(this.color);
}
var find = function(callback,callback_obj){
  if(type callback ==='function'){
    callback.call(callback_obj);
  }
}
find(myapp.paint,myapp);


闭包
var setup = function(){
  var count = 0;
  return function(){
    return count +=1;
  }
}
var aaa = setup();
aaa();


当函数有一些初始化准备工作要做，并且仅需执行一次，可以自定义函数，更新自身的实现。
var scareMe = function(){
  console.log('foo');
  scareMe = function(){
    console.log('new');
  }
}
scareMe(); // 第一次执行输出foo;
scareMe(); // 第一次之后都输出new

即时函数
①(function(){
    console.dir({});
}());  // JSLint偏好使用？
②(function(){
    console.dir({});
})()

即时对象初始化 
// 优点：相比即时函数，如果初始化任务更复杂，会使整个初始化过程显得更有结构化。
// 缺点：绝大多数minifier(缩小器)工具并不会像仅包装在函数中的代码那样有效的缩减这种模式。
①({
  width:600,
  height:300,
  gimmeMax:function(){
    return this.width+' x '+this.height;
  },
  init:function(){
    return this.gimmeMax();
  }
}).init();
②({}.init());

浏览器嗅探(功能检测)
// 反模式
var utils = {
  addListener:function(el,type,fn){
    if(typeof window.addEventListener === 'function'){
      el.addEventListener(type,fn,false);
    }else if(typeof document.attachEvent === 'function'){  // IE浏览器
      el.attachEvent('on' + type,fn);
    }else{  // 更早版本浏览器
      el['on'+type] = fn;
    }
  }
  removeListener:function(el,type,fn){
    // 几乎一样的代码
  }
}
// 优化后效果
var util = {
  addListener:null,
  removeListener:null
};
if(typeof window.addEventListener === 'function'){
  util.addListener = function(el,type,fn){
    el.addEventListener(type,fn,false);
  };
  util.removeListener = function(el,type,fn){
    el.removeEventListener(type,fn,false);
  }
}else if(typeof document.attachEvent === 'function'){
  ......
}else{
  ......
}

函数属性——备忘模式
var myFunc = function(){
  var cacheKey = JSON.stringify(Array.prototype.slice.call(arguments)),
  result;
  if(!myFunc.cache[cacheKey]){
    result = {};
    myFunc.cache[cacheKey] = result;
  }
  return myFunc.cache[cacheKey];
}
myFunc.cache = {};

以下在ECMAScript5的严格模式中并不支持
var myFunc = function(param){
  var f = arguments.callee,
  result;
  if(!f.cache[param]){
    result = {};
    f.cache[param] = result;
  }
  return f.cache[param];
}
myFunc.cache = {};


typeof 一元运算符
普通字面量定义的变量可以区分出以下几种类型：string/number/boolean/object
内置对象定义的变量、[]  ==>  object 
new Function('') ==> function
/abc/g 、 new RegExp('meow')   ==>  object(function in Nitro/V8)  

// 标准获取变量类型方法
function is(type,obj){
  var clas = Object.prototype.toString.call(obj).slice(8,-1);
  return obj !== 'Undefined' && obj !=='null' && clas ===type;
}
is('String',new String('test')) // true

typeof特殊作用
typeof foo !== 'undefined' // 检测foo是否定义，如果没有定义而直接使用会导致ReferenceError的异常

类数组：
可以通过索引访问元素，并且拥有length属性，没有数组的方法

类数组转换为数组
var foo = {
  0:'Java',
  1:'Python',
  2:'Scala',
  length:3
}
Array.prototype.slice.call(foo); // ["Java", "Python", "Scala"]  注意此处的length若为2 则仅返回前两个


Curry化
Curry化是一个转换过程，即我们执行函数转换的过程。
// curry化的add()函数
function add(x,y){
  if(typeof y === 'undefined'){
    return function(y){
      return x+y;
    }
  }
  return x+y;
}

// 通用curry化函数示例
function schonfinkelize(fn){
  var slice = Array.prototype.slice;
  var stored_args = slice.call(arguments,1);
  return function(){
    var new_args = slice.call(arguments);
    var args = stored_args.concat(new_args);
    return fn.apply(null,args);
  }
}
function add(x,y){
  return x+y;
}
var newAdd = schonfinkelize(add,1);
newAdd(2);
或
schonfinkelize(add,1)(2);

何时使用Curry化？
  当发现正在调用同一个函数，并且传递的参数绝大多数都是相同的。
  可以通过将一个函数集合部分应用到函数中，从而动态创建一个新函数。新函数将会保存重复的参数，并且还会使用预填充原始函数所期望的完整参数列表。

函数提供了局部作用域，而其他大括号并不能提供局部作用域。

call、apply、bind区别
var obj = {name:'lixi'};
function func(first,last){
  console.log(first+this.name+last);
}
func.call(obj,'A','B');
func.apply(obj,['C','D']);
// bind返回的是函数
var func1 = func.bind(obj,'E','F');
func1();

// Function.prototype.bind()实现方法
```js
if(typeof Function.prototype.bind === 'undefined'){
    Function.prototype.bind = function(thisArg){
        var fn = this,
        slice = Array.prototype.slice,
        args = slice.call(arguments,1);
        
        return function(){
            return fn.apply(thisArg,args.concat(slice.call(arguments)));
        }
    }
}
var one = {
    name:'object',
    say:function(greet){
        return greet+','+this.name;
    }
};
var two = {
    name:'another'
};
var twoSay2 = one.say.bind(two);
twoSay2('Bonjour');
```



通用命名空间函数  // 方便创建深层次对象
var MYAPP = MYAPP||{};
MYAPP.namespace = function(ns_string){
  var parts = ns_string.split('.'),
  parent = MYAPP,
  i;
  
  // 剥离最前面冗余全局变量
  if(parts[0] === 'MYAPP'){
    parts = parts.slice(1);
  }
  
  for(i=0;i<parts.length;i+=1){
    if(typeof parent[parts[i]]==='undefined'){
      parent[parts[i]] = {};
    }
    parent = parent[parts[i]];
  }
  return parent;
}


沙箱模式  // 提供了一个可用于木块运行的环境，且不会对其它模块和个人沙箱造成任何影响
```js
function Sandbox(){
    var args = Array.prototype.slice.call(arguments),
    callback = args.pop(),
    modules = (args[0]&&typeof args[0]==='string')?args:args[0],
    i;
    if(!(this instanceof Sandbox)){
        return new Sandbox(modules,callback);
    }
    this.a = 1;
    this.b = 2;
    if(!modules||modules==='*'){
        modules = [];
        for(i in Sandbox.modules){
              if(Sandbox.modules.hasOwnProperty(i)){
                    modules.push(i);
              }
        }
  }
      if(!Sandbox.modules){
            Sandbox.modules = {};
      }
      for(i=0;i<modules.length;i+=1){
            Sandbox.modules[modules[i]](this);
      }
      callback(this);
}
Sandbox.prototype = {
      name:'My Application',
      version:'1.0',
      getName:function(){
            return this.name;
      }
};

//预定义模块
Sandbox.modules = {};
Sandbox.modules.ajax = function(box){
      box.makeRequest = function(){};
      box.makeResponse = function(){};
};
Sandbox.modules.event = function(box){
    box.attachEvent = function(){};
    box.dettachEvent = function(){};
};
Sandbox('ajax','event',function(box){
  console.log(box);
})
```


常见四种Content-Type类型
application/x-www-form-urlencoded 常见的form提交
multipart/form-data 文件提交
application/json 提交json格式的数据
text/xml 提交xml格式的数据


几种类型判断区分
typeof
instanceof


对象常量  // 方便常亮定义不可被修改
```js
var constant = function(){
    var constants = {},
        ownProp = Object.prototype.hasOwnProperty,
        allowed = {
            string:1,
            number:1,
            boolean:1
        },
        prefix = (Math.random()+'_').slice(2);
    
    return {
        set:function(name,value){
            if(this.isDefined(name)){
                return false;
            }
            if(!ownProp.call(allowed,typeof value)){
                return false;
            }
            constants[prefix+name] = value;
            return true;
        },
        isDefined:function(name){
            return ownProp.call(constants,prefix+name);
        },
        get:function(name){
            if(this.isDefined(name)){
                return constants[prefix+name];
            }
            return null;
        }
    }
}
```

链模式  // 
```js
var obj  ={
    value:1,
    increment:function(){
        this.value+=1;
        return this;
    },
    add:function(v){
        this.value+=v;
        return this;
    },
    shout:function(){
        alert(this.value);
    }
};
obj.increment().add().shout();

```


类式继承
```js
function Parent(name){
    this.name = name ||'Adam';
}
Parent.prototype.say = function(){
    return this.name;
};
function Child(name){}
```
1、默认模式  // 使用Parent()构造函数创建一个对象，并将该对象赋值给Child()的原型。
```js
inherit(Child,Parent);
function inherit(C,P){
    C.prototype = new P();
}
```
2、借用构造函数  // 该继承是一个一次性的操作，它仅会复制父对象的属性并将其作为子对象自身的属性，仅此而已，因此也不会保留_proto_链接
```js
function Child(){
    Parent.call(this,arguments);
}
```
3、共享原型  // 可复用成员应转移至原型中，而不是放置在this中。 【此方法中，子对象修改了原型会影响到所有父对象】
```js
function inherit(C,P){
    C.prototype = P.prototype;
}
```
4、临时构造函数
```js
function inherit(C,P){
    var F = function(){};
    F.prototype = P.prototype;
    C.prototype = new F();
}
```
5、圣杯版本
```js
function inherit(C,P){
    var F = function(){};
    F.prototype = P.prototype;
    C.prototype = new F();
    c.uber = P.prototype;
    C.prototype.constructor = C;
}

// 优化版本
var inherit = function(){
    var F = function(){};
    return function(C,P){
        F.prototype = P.prototype;
        C.prototype = new F();
        C.uber = P.prototype;
        C.prototype.constructor = C;
    }
}
```
// 通过复制属性实现继承
```js
// 浅继承
function extend(parent,child){
    var i;
    child = child||{};
    for(i in parent){
        if(parent.hasOwnProperty(i)){
            child[i] = parent[i];
        }
    }
    return child;
}

// 深度继承
function extendDeep(parent,child){
    var i,
    toStr = Object.prototype.toString,
    astr = '[object Array]';
    
    child = child ||{};
    for(i in parent){
        if(parent.hasOwnProperty(i)){
            if(typeof  parent[i] ==='object'){
                child[i] = (toStr.call(parent[i])===astr?[]:{})
                extendDeep(parent[i],child[i]);
            }
            else{
                child[i] = parent[i];
            }
        }
    }
}

// 混入 
function mix(){
    var arg,prop,child = {};
    for(arg=0;arg<arguments.length;arg+=1){
        for(prop in arguments[arg]){
            if(arguments[arg].hasOwnProperty(prop)){
                child[prop] = arguments[arg][prop];
            }
        }
    }
    return child;
}
```

// 借用和绑定
```js
// 将 m 方法始终和 o 对象绑定
function bind(o,m){
    return function(){
        return m.apply(o,[].slice.call(arguments));
    }
}
```

// 工厂模式
```js
function CarMaker(){}
CarMaker.prototype.drive = function(){
    return 'Vroom, I have'+this.doors+' doors';
};
CarMaker.factory = function(type){
    var constr = type, newcar;
    if(typeof CarMaker[constr]!=='function'){
        throw{
            name:'Error',
            message:constr+"doesn't exist"
        }
    }
    if(typeof CarMaker[constr].prototype.drive !=='function'){
        CarMaker[constr].prototype = new CarMaker();
    }
    newcar = new CarMaker[constr]();
    return newcar
};
CarMaker.Compact = function(){
    this.doors = 4;
};
var corolla = CarMaker.factory('Compact');
corolla.drive();
```

// 装饰者模式[不改变对象自身的基础上]
```js
function Sale(price){
    this.price = price||100;
}
Sale.prototype.getPrice = function(){
    return this.price;
};
Sale.decorators = {};
Sale.decorators.fedtax = {
    getPrice:function(){
        var price = this.uber.getPrice();
        price += price*5/100;
        return price;
    }
};
Sale.decorators.quebec = {
    getPrice:function(){
        var price = this.uber.getPrice();
        price += price*7.5/100;
        return price;
    }
};
Sale.decorators.money = {
    getPrice:function(){
        return '$'+this.uber.getPrice().toFixed(2);
    }
};
Sale.prototype.decorate = function(decorator){
    var F = function(){},
    overrides = this.constructor.decorators[decorator],
    i,newobj;
    F.prototype = this;
    newobj = new F();
    newobj.uber = F.prototype;
    for(i in overrides){
        if(overrides.hasOwnProperty(i)){
            newobj[i] = overrides[i];
        }
    }
    return newobj;
};
var sale = new Sale(100);
sale = sale.decorate('fedtax');
sale = sale.decorate('money');
sale.getPrice();
// 关键点解析：uber做原型存储，getPrice通过this.uber.getPrice()实现调用上一层中的原型方法


// 方法二 更简单
function Sale(price){
    this.price = (price>0)||100;
    this.decorators_list = [];
}
Sale.decorators = {};
Sale.decorators.fedtax = {
    getPrice:function(price){
        return price+price*5/100;
    }
};
Sale.decorators.quebec = {
    getPrice:function(price){
        return price+price*7.5/100;
    }
};
Sale.decorators.money = {
    getPrice:function(price){
        return '$'+price.toFixed(2);
    }
};
Sale.prototype.decorate = function(decorator){
    this.decorators_list.push(decorator);
};
Sale.prototype.getPrice = function(){
    var price = this.price,
        i,
        max = this.decorators_list.length,
        name;
    for(i=0;i<max;i+=1){
        name = this.decorators_list[i];
        price = Sale.decorators[name].getPrice(price);
    }
    return price;
}

```

```js
var validator = {
  types:{},
  messages:[],
  config:{},
  validate:function(data){
    var i,msg,type,checker,result_ok;
    this.messages = [];
    for(i in data){
      if(data.hasOwnProperty(i)){
        type = this.config[i];
        checker = this.types[type];
        if(!type){
          continue;
        }
        if(!checker){
          throw {
              name:'ValidationError',
              message:'No handler to validate type'+type
          };
        }
        result_ok = checker.validate(data[i]);
        if(!result_ok){
            msg = 'Invalid value for *'+i+'*, '+checker.instructions;
            this.messages.push(msg);
        }
      }
    }
    return this.hasErrors();
  },
  hasErrors:function(){
      return this.messages.length!==0;
  }
};
validator.config = {
    first_name:'isNonEmpty',
    age:'isNumber',
    username:'isAlphaNum'
};
validator.types.isNonEmpty = {
    validate:function(value){
        return value !== '';
    },
    instructions:'the value connot be empty'
};
validator.types.isNumber = {
    validate:function(value){
        return !isNaN(value);
    },
    instructions:'the value can only be a valid number,e.g. 1, 3.14 or 2010'
};
validator.types.isAlphaNum ={
    validate: function(value){
         return !/[^a-z0-9]/i.test(value);
    },
    instructions:'the value can only contain characters and numbers'
}
```



















