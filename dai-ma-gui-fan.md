# 代码规范

* 提交代码前格式化代码\(webstrom:Ctrl+Alt+L\)
* 输入提醒。xxx不能为空 =&gt; 请输入xxx
* 打包提交的备注：bundle。gulp-updateRev之后，要commit:bundle，push
* css命名:
  * 名过长用 - 隔开而非驼峰式命名
  * 按功能命名\(simulation-blue/simulation-red 会带来维护的问题：如果将来通知和警告分别用了green、yellow，那这样式名就错了,改为 proclamation-default、proclamation-warning 、 proclamation-danger\)
* 代码注释/取消注释的操作：选中一块区域，只用 ctrl + / \(ctrl + shift + / 造成的大段注释，容易带来格式断裂问题\) 
* 尽量不使用 ng-init。ng-init 在每一个 ng-if 或加载时或可能都会执行一次。而往往你编辑的页面状态并不应该随着ng-if就初始化一次。
  为避免滥用，不使用 ng-init ，赋初使值在 controller 里写 js 实现。
* 把你的webstorm设置为LF。即类似linux换行。
* 回退的时候，使用 git compare或者git history来确认代码无遗漏。
* 注释里含英文的情况，请把英文单词前后都加个空格。可读性提高。、
* 尽量减少、简化参数传递。reject 想返回各式各样的带title 或者不带 title 的错误提示语。会导致promise reject 时得到的结果奇奇怪怪难以约束，试试 当场 wbkAlertService.error\(xxx\); q.reject\(\);
* 常用的前缀。is、has、need、ensure、get、set、query
* 函数名称与内容 职责分明。函数内容与名称一致。
* 使用 var vm = $scope 。而不要到处用 $scope/scope
* 注意验证多个控件同一个ngModel值。多个编辑指令里ngModel对象是否同一个
* 加一个特性：给 hostSelector、hostListViewer、hostTypeahead支持ngMessages的required验证。
* 指令带来的消耗最适合销毁的时机就是：指令的scope destroy的时候
  scope的watcher、dom的bind、timeout、interval、暴露出去的大变量对象
* 除非不得已，不要使用margin-top。
  两个原因：
  1. 某些浏览器上，如果你任意的使用margin-top、margin-bottom，当这两个特性相遇的时候，会产生不确定的渲染。
  2. padding是属于元素的一部分。margin是元素想要给自己保留一定的舒适空间，对环境的外部要求。统一使用margin-right、margin-bottom，可以满足样式简单一致性，便于摆放元素。
     当你的任意组合不同元素的时候，不需要再次去考虑该元素margin-top与前一元素的margin-bottom的组合冲突兼容。
     改用设置上面的元素的margin-top，或者父元素的padding-top，或者使用自身的padding-top。
* 统一用create/edit/remove 这样的动词，set太泛化了，少用。
* 判断组件是否含有某属性，判断 attrs.xxx 而不是scope.
* 不要阻塞原有流程。99%时候这个检查是会通过的，只会让页面打开变慢。

# 代码优化

* 判断数组长度大于0，array.length&gt;0 =&gt; array.length
* 建议对于0的判断，如果不确定数值类型（int、string），只使用 ===0 或 String\(xx\) == '0'。
* 一个结果只使用一个dom是为了提升性能。dom越多越卡，1000行一个dom来显示远比1000个dom省性能
* 主动发送change比watch省性能（angularjs尽量使用change事件而非watch监听事件）
* JSON.parse\(jobSchema.source.sqlStat\|\|'{}'\) = &gt; jobSchema.source.sqlStat && JSON.parse\(jobSchema.source.sqlStat\) \|\| {}
* 防重复点击。加一个标识 isStarting ，以免提示过程中用户重复点击。
* 检查正则，同时补上trim
* 点编辑器的全屏按钮后，编辑器不是聚焦状态。esc无用了。建议：所有按钮点击后，调用 editorInstance.focus\(\)
* 下载的txt文档，在windows下不能换行显示。建议，判断当前的环境，如果是windows，那么把所有 \n 替换成 \r\n ，如果是其他系统，直接下载。
* 复制粘贴不要在key事件里做。直接用onPaste,类似的onCut、onCopy
* 避免使用button、input\[submit\] 按钮。使用a.btn-link 、 div.btn-primary之类的实现。button、input\[submit\]会引发form的提交。
* 进入 aomp.configList 页面时，要等到 queryConfig 加载完成后，再去读缓存，以确保从缓存读到的是刚更新过的
* 请使用私有变量。不要把cache对象暴露到service级别。
* JSON.parse 附近用 try ，对于无配置或错误配置的情况，返回默认值
* 试试用 $parsers、$formatters、$render 来替代 $watch\( $modelValue \) ?   **【待确认】**   
  相比 $watch\( $modelValue \) ，最大的区别是：   
  $render 在$formatters之后渲染页面显示值之前\(来自于外部“初始”赋值\)
  $parsers 用于控件内修改后 $setViewValue   
  $formatters 来自于控件外部修改值。   
  $watch 无法辨识变化由什么事件产生。所以，以上三个处理器触发的时候，都会触发$watch   
  请确认：$render 在哪些情况下会被触发？ - - 可能我描述的是错误的：‘仅在初始赋值时触发’   
* $\(\)是全局查找的，试试在Controller里注入$element，限定在$element内查找
* 界面里包含了太多的逻辑判断，ng-if，这本该移到controller里，用一个switch逻辑来替换

# 其它

* 在线终端，你知道～符号什么意思吗？参考macbook的终端terminal。也是linux系统的
* ngModel.$dirty/ $setDirty 等逻辑，当用户手动修改的时候$setDirty，记录每个快照对应的dirty。在快照里加入当时的dirty状态，作为是否可回退的附加判断。
* 这有一个非常不优雅的hack方式：
  var contribution = monacoEditorInstance.contributions\['editor.action.commentLine'\];
  contribution.\_shouldShowInContextMenu= true;

# 视觉

* 一般情况下避免深灰色背景 + 黑色文字。因为看不清。
* 相近的元素，如果想表达有差异，那么差异明显些。如果想表达无差异，那么就完全无差异。
  界于明显与不明显之间的模糊效果，给用户的感觉是质量粗糙。
  上图的图标背景色是若有若无的淡灰色。
* 检查你的文字段落是否有使用留白。
* 界面改版的目标和思考方向应该是顺着：   
   优化用户操作流程体验   
  ```
   => 优化界面布局   
   => 优化控件交互细节　＋　显示样式
  ```



