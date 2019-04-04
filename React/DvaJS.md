# Dva 路由控制

##### dva 概念
 数据的改变发生通常是通过用户交互行为或者浏览器行为（如路由跳转等）触发的，当此类行为会改变数据的时候可以通过 dispatch 发起一个 action，如果是同步行为会直接通过 Reducers 改变 State ，如果是异步行为（副作用）会先触发 Effects 然后流向 Reducers 最终改变 State，所以在 dva 中，数据流向非常清晰简明，并且思路基本跟开源社区保持一致（也是来自于开源社区）。
 
<a href='https://dvajs.com/guide/concepts.html#%E6%95%B0%E6%8D%AE%E6%B5%81%E5%90%91' target='_blank' >官方文档地址</a>

##### dva 组件简介

* dva = 【Models】+【Router】 两部分构成
<p>1.Models</p>
<ul>
 <li>State</li>
 <li>Action</li>
 <li>dispatch 函数</li>
 <li>Effect</li>
 <li>Subscription</li>
</ul>

<p>2.Router</p>
<ul>
 <li>react-router</li>
</ul>

###### dva 组件详解
     
* State 
     
     ![](https://github.com/dailiuyang123/NoteBook/blob/master/pictrue/HTTPS%E9%AA%8C%E8%AF%81.png)
     
     

