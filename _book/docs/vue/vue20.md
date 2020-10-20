## Vuex状态管理模式   

 state  // 状态      
 mutations  // 提交mutation改变状态   
 store.commit('mutation')   
 
 actions // 提交mutation，可以包含异步操作   
 store.dispatch('action')   
 
 getters  // 类似计算属性


## Vuetify

 v-layout 加wrap，实现的是流式布局   
 v-layout 不加wrap，实现的单行布局   

 跟布局有关的组件，主要只有两个：  
    v-card：跟div一样用   
    v-container > v-layout > v-flex ：跟table>tr>td一样用。   

 组件的属性使用参考 vuetify的示例和源代码。   
 vuetify整体项目示例，参考 vue-material-admin

 v-table有暂无数据默认提示，要修改则需添加   
` <div slot="empty">msg</div>`

    
## Vue搭建H5页面总结    

 + font-family:'黑体'，在CSS中会被编译，iphone识别不出【字体样式直接放至index.html，免编译】
 + div内div设置margin-top，外层div高度未撑起，导致布局错乱【外层div设置透明边线】
 + 屏幕适配@media screen and () and (){} 【注意空格，否则不生效】