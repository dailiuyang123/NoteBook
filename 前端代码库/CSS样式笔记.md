# CSS 笔记


* cursor: pointer; 当鼠标指针移入时，改变指针图标

* 用css 如何改变文本框（input）输入光标的位置? 光标要往后一点
 ```html
   <input style="padding-left:10px;"/>即可， 可以根据自己需要修改 padding-left的值
```
 * 如何点击div跳转链接
 ```html
<div onclick="window.open('http://www.baidu.com')">在新窗口跳转至百度</div>

<div onclick="window.open('http://www.baidu.com','_self')">在当前窗口跳转至百度</div>
``` 
* 超链接类 a 标签 如何设置，使其不跳转
 ```html
标签属性href，使其指向空或不返回任何内容。如：
<a href="javascript:void(0);" >点此无反应javascript:void(0)</a>
<a href="javascript:;" >点此无反应javascript:</a>

标签事件onclick，阻止其默认行为。如：
<a href="" onclick="return false;">return false;</a>
<a href="#" onclick="return false;">return false;</a>
注意：只有一个href="#"是不可以的。

```
 * 点击 回到顶部功能配置
 ```html
首先我们在网页body内最上面添加一个<span id="top" name="top"></span>

我们再到body内，需要出现点击后转到顶部位置添加，<a href="#top">回到顶部</a>

点击回到顶部即可让滚动回到顶部。
```
* js 模拟鼠标点击效果
```javascript
 <ul id="son">
   <li>系统入口</li>
   <li>流程入口</li>
   <li>个人中心</li>
 </ul>
 //实现 默认点击效果
 $("#son").children().each(function(){
            var litel= $(this).text();
            if (litel==date[0]){
                //模拟 鼠标点击事件 
                $(this).click();
            }
        });
```

* HTML <'a '> 标签的 target 属性
```javascript
<a target="value">

_blank	在新窗口中打开被链接文档。
_self	默认。在相同的框架中打开被链接文档。
_parent	在父框架集中打开被链接文档。
_top	在整个窗口中打开被链接文档。
framename	在指定的框架中打开被链接文档。
```




