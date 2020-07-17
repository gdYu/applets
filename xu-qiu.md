 ## Css常用字典
 
 + box-sizing    
    box-sizing:border-box;  // 在指定宽高内绘制内边距、边框    
    box-sizing:content-box;  // 在指定宽高外绘制内边距、边框

  
 + box-shadow:   
    h-shadow   // 水平阴影位置，允许负值。必需   
    v-shadow   // 垂直阴影位置，允许负值。必需
    blur       // 模糊距离。可选   
    spread     // 阴影尺寸。可选   
    color      // 阴影颜色。可选   
    outset     // 阴影位置。默认outset,可修改为inset   
    
    
 + 文字换行
    word-break:keep-all    // 不换行    
    word-break:break-all  // 换行显示 一般用在长英文语句中
    white-space:nowrap     // 不允许换行
 
 
 + table-layout:fixed  列宽由表格宽度和列宽度设定
 
 
 + textarea拖动样式设置   
 	resize:none  //不允许拖动   
 	resize:vertical  // 只允许纵向拖动   
 	resize:horizontal  // 只允许横向拖动   
 
 
 + transform-origin // 旋转元素基点位置（一般和transform:rotate联用）
 
 
 + -webkit-tap-highlight-color // 设置点击链接的时候出现的高亮颜色。
 
 
 + svg->rect->fill  // 设置矩形填充色
 
 
 + clip-path  // 创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。
 
 
 + border-collapse:collapse // 表格边框合并为单一边框
 
 
 + border-spacing // 设置相邻单元格的边框间距
 
 
 + 文本开头缩进   
    text-indent,规定 文本块 中首行文本缩进。
    
    
 + animation-duration  定义动画完成一个周期所需要的时间，以秒或毫秒计
 
 
 + border-collapse: collapse 设置表格边框合并为一个单一边框
 
 
 ## 技术点
 
 
 + 页面上引入图标、图形字体出现锯齿   
     尽量使用倍数，才能让图标比较保真的显示。     
     比如原尺寸是16px * 16px ，那么你显示为32px * 32px、8px * 8px 都可以完美显示。   
     如果你调成 17px * 17px，就会有锯齿。   
     屏幕的最小显示单位是：像素。   
     你无法切割一个像素，所以多出来或少的一个，会形成剧齿   
     用户不会明显察觉锯齿，但会感觉到粗糙   
     至少要双数吧，更好的是4的倍数，8的倍数，16的倍数。对吧。   
     如果是双数，那么 150% 、50% 可以完美显示。   
     如果是4的倍数，那么75%、125%也可以流畅显示。
     
     
 + opacity会对元素层级有干扰
    CSS中parent opacity使用注意子元素z-index会受影响   
    如果仅针对文字。可以使用color: rgba(xx,xx,xx, .5)；   
    如果仅针对背景色，同理，使用rgba。
    
    
 + intro.js步骤内容渐显,透明层穿透，实现  
    div-bg-wrapper         position:fixed;z-index:1   
    div-bg-intro           position:absolute;z-index:2   
    div-point-intro        position:absolute;visibility:hidden;background-color:transparent;z-index:4  // 透明，不可见，但占据空间，方便提示定位   
    point-number           position:absolute;visibility:visible;   
    point-tooltip          position:absolute;visibility:visible;   
    point-intro            position:relative;z-index:3;  // 突出的文本内容   
    动画中，遮罩层渐显原理，原本文字的白色背景变成了遮罩层背景，所以看起来渐显。   
    注意，如果文本有设置背景色，则会失效
 
 
 + 超出文本显示...   
 	overflow:hidden;   
 	text-overflow:ellipsis;   
 	white-space:nowrap;   
 
 
 + div清除浮动   
   ①父div添加overflow:auto   
   ②最后添加一个含有clear:both样式的兄弟div   
   ③父div :after 伪元素添加   
     content: '';   
     clear: both;   
     display: block;   
     width: 0;   
     height: 0;   
     visibility: hidden;   
 
 
 + 元素不可选中样式：
    pointer-events:none;
    cursor:not-allowed;
 
 
 + css样式名称筛选   
   .form [attributeName]:not(:last-child):after{}
 
 
 + div中table宽度不能100%总是差一点像素，dispaly:table;
 
 
 + checkbox和文字不能上下对齐
    ```
    .checkbox{
 	    vertical-align:text-bottom;
 	    margin-bottom:2px;
 	    *margin-bottom:-2px;// 兼容IE6，IE7
    }
    ```
 
 
 + css3  ::selection 选择器[用户选取部分]   
    支持属性：color、background、cursor、outline
 
 
 + CSS3逐帧动画   
 	background-position动态改变雪碧图位置   
 	steps阶梯函数实现：animation-timing-function:steps(number_of_steps,direction)
 
 + 长方形切除四个角
   ```
    ① 一个右下角
    .box{
            width: 200px;
            height: 100px;
            background:linear-gradient(-45deg,transparent 15px,#eee 0) ;
            background-size:50% 50%;
            background-repeat:no-repeat;
        }
    
    ② 两个下边角
    .box{
            width: 200px;
            height: 100px;
            background:linear-gradient(-45deg,transparent 15px,#eee 0) right,
                       linear-gradient(45deg,transparent 15px,#eee 0) left;
            background-size:50% 100%;
            background-repeat:no-repeat;
        }
        
    ③ 四个边角
    .box{
        width: 200px;
        height: 100px;
        background:linear-gradient(135deg,transparent 15px,#eee 0) top left,
                   linear-gradient(-135deg,transparent 15px,#eee 0) top right,
                   linear-gradient(-45deg,transparent 15px,#eee 0) bottom right,
                   linear-gradient(45deg,transparent 15px,#eee 0) bottom left;
        background-size:50% 50%;
        background-repeat:no-repeat;
    }
   ```
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
