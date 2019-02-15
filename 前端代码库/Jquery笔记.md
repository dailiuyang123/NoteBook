#Jquery 笔记

* jquery 遍历
```javascript
 $("li").each(function(){
        alert($(this).text())
      });
```

* jquery 获取标签文本
```javascript
$(this).text();
```
  
  
* jquery 获取 h5 dom元素内 value属性的值
    ```javascript
    $("#ID").val();
    ```
 

  
  
 ## jquery 获取 元素内的值
 
 
 *jquery 获取下拉框 'SELECT' 选择的值
 ```html
                               <select id="LinkType">
                                  <option selected="selected" >请选择</option>
                                  <option value="1" >HR系统</option>
                                  <option value="2" >办公系统</option>
                                  <option value="3" >财务系统</option>
                                  <option value="4" >技术/运维系统</option>
                                  <option value="5" >大数据系统</option>
                                  <option value="6">业务系统</option>
                              </select> 
                               
                        $("#LinkType").on('change',function(){
                        		 
                        	var v=$("#LinkType").val();
                        	console.log(v);
                        		
                        	});    
```
 ### jquery 之 Ajax 
 <table style="width: 600px" border="1" cellspacing="2" cellpadding="2">
 <tbody>
 <tr>
 <td valign="top" width="90">参数名</td>
 <td valign="top" width="83">类型</td>
 <td valign="top" width="419">描述</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>url</strong></td>
 <td valign="top" width="83">String</td>
 <td valign="top" width="419">(默认: 当前页地址) 发送请求的地址。</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>type</strong></td>
 <td valign="top" width="83">String</td>
 <td valign="top" width="419">(默认: "GET") 请求方式 ("POST" 或 "GET")， 默认为 "GET"。注意：其它 HTTP 请求方法，如 PUT 和 DELETE 也可以使用，但仅部分浏览器支持。</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>timeout</strong></td>
 <td valign="top" width="83">Number</td>
 <td valign="top" width="419">设置请求超时时间（毫秒）。此设置将覆盖全局设置。</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>async</strong></td>
 <td valign="top" width="83">Boolean</td>
 <td valign="top" width="419">(默认: true) 默认设置下，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为 false。注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行。</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>beforeSend</strong></td>
 <td valign="top" width="83">Function</td>
 <td valign="top" width="419">发送请求前可修改 XMLHttpRequest 对象的函数，如添加自定义 HTTP 头。XMLHttpRequest 对象是唯一的参数。<br>
 <pre>function (XMLHttpRequest) {
 
          this; // the options for this ajax request
          }</pre>
 </td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>cache</strong></td>
 <td valign="top" width="83">Boolean</td>
 <td valign="top" width="419">(默认: true) jQuery 1.2 新功能，设置为 false 将不会从浏览器缓存中加载请求信息。</td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>complete</strong></td>
 <td valign="top" width="83">Function</td>
 <td valign="top" width="419">请求完成后回调函数 (请求成功或失败时均调用)。参数： XMLHttpRequest 对象，成功信息字符串。<br>
 <pre>function (XMLHttpRequest, textStatus) {
 
          this; // the options for this ajax request
          }</pre>
 </td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>contentType</strong></td>
 <td valign="top" width="83">String</td>
 <td valign="top" width="419">(默认: "application/x-www-form-urlencoded") 发送信息至服务器时内容编码类型。默认值适合大多数应用场合。</td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>data</strong></td>
 <td valign="top" width="83">Object,<br>String</td>
 <td valign="top" width="419">发送到服务器的数据。将自动转换为请求字符串格式。GET 请求中将附加在 URL 后。查看 processData 选项说明以禁止此自动转换。必须为 Key/Value 格式。如果为数组，jQuery 将自动为不同值对应同一个名称。如 {foo:["bar1", "bar2"]} 转换为 '&amp;foo=bar1&amp;foo=bar2'。</td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>dataType</strong></td>
 <td valign="top" width="83">String</td>
 <td valign="top" width="419">
 <p>预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息返回 responseXML 或 responseText，并作为回调函数参数传递，可用值:</p>
 <p>"xml": 返回 XML 文档，可用 jQuery 处理。</p>
 <p>"html": 返回纯文本 HTML 信息；包含 script 元素。</p>
 <p>"script": 返回纯文本 JavaScript 代码。不会自动缓存结果。</p>
 <p>"json": 返回 JSON 数据 。</p>
 <p>"jsonp":&nbsp;<a href="http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/" target="_blank">JSONP</a>&nbsp;格式。使用&nbsp;<a href="http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/" target="_blank">JSONP</a>&nbsp;形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。</p>
 
 </td>
 
 </tr>
 <tr>
 <td valign="top" width="90"><strong>error</strong></td>
 <td valign="top" width="83">Function</td>
 <td valign="top" width="419">(默认: 自动判断 (xml 或 html)) 请求失败时将调用此方法。这个方法有三个参数：XMLHttpRequest 对象，错误信息，（可能）捕获的错误对象。<br>
 <pre>function (XMLHttpRequest, textStatus, errorThrown) {
 
          // 通常情况下textStatus和errorThown只有其中一个有值 
          this; // the options for this ajax request
          }</pre>
 </td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>global</strong></td>
 <td valign="top" width="83">Boolean</td>
 <td valign="top" width="419">(默认: true) 是否触发全局 AJAX 事件。设置为 false 将不会触发全局 AJAX 事件，如 ajaxStart 或 ajaxStop 。可用于控制不同的Ajax事件</td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>ifModified</strong></td>
 <td valign="top" width="83">Boolean</td>
 <td valign="top" width="419">(默认: false) 仅在服务器数据改变时获取新数据。使用 HTTP 包 Last-Modified 头信息判断。</td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>processData</strong></td>
 <td valign="top" width="83">Boolean</td>
 <td valign="top" width="419">(默认: true) 默认情况下，发送的数据将被转换为对象(技术上讲并非字符串) 以配合默认内容类型 "application/x-www-form-urlencoded"。如果要发送 DOM 树信息或其它不希望转换的信息，请设置为 false。</td>
 </tr>
 <tr>
 <td valign="top" width="90"><strong>success</strong></td>
 <td valign="top" width="83">Function</td>
 <td valign="top" width="419">请求成功后回调函数。这个方法有两个参数：服务器返回数据，返回状态<br>
 <pre>function (data, textStatus) {
 
          // data could be xmlDoc, jsonObj, html, text, etc...
          this; // the options for this ajax request
          }</pre>
 </td>
 </tr>
 </tbody>
 </table>
 
  
## javascript 笔记
  
*  js内通过 EL表达式 获取集合对象，直接是一个数组对象。不需要 Json 进行对象转换。


* js 遍历 整个对象获取整个对象 Key的集合。
```javascript
//遍历map 返回keyset
     function getKeySet(data) {
         var list=new Array();
         var i=0;
         for(var k in data ){//遍历packJson 对象的每个key/value对,k为key
             list[i]=k;
             i++;
         }
         return list;
     }
```
 
 * js 声明对象的方式 两种方式
 ```javascript
   var navlink=new Object();
   var navlink={};
```
 

 * js 判断 对象是否为空 的两种方式
 ```java
var b = (JSON.stringify(data) == "{}");
jquery的 isEmptyObject(obj)方法 
```
 * js将 数字类型转为 String类型的方法：
 ````javascript
     var a=123; //数字类型
     String(a); //字符串类型
````
* js 合并两个数组：
```javascript
   var a=[1,4,5,6];
   var b=[2,4,6];
   a.concat(b);   // a 合并 b 数组

```
* js 向数组追加元素：
```javascript
   var a =[1,3,5];
   a.push(2);
```

* js 实现路由跳转
```javascript
   // 实现路由跳转   
   window.location.href= URL;
```









    