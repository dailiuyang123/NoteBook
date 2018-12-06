#JSP CODE 

* js文件内无法解析 EL表达式        解决方案
```html
  <script type="text/javascript">
      var ctx = "${ctx}";
  </script>
  //在jsp页面内 获取EL 表达式的值，然后将值设为 全局变量即可
```
* jsp 中 回显 select下拉选择框 el 三元运算符 如何选中与不选中
 ```jsp
                                                    <select id="LinkType">
                                                       <option   ${data.linkType == null?'selected="selected"':''} >请选择</option>
                                                       <option value="1" ${data.linkType == 1?'selected="selected"':''} >HR系统</option>
                                                       <option value="3" ${data.linkType == 3?'selected="selected"':''}>办公系统</option>
                                                       <option value="4" ${data.linkType == 4?'selected="selected"':''}>财务系统</option>
                                                       <option value="2" ${data.linkType == 2?'selected="selected"':''}>技术/运维系统</option>
                                                       <option value="6" ${data.linkType == 6?'selected="selected"':''}>大数据系统</option>
                                                       <option value="5" ${data.linkType == 5?'selected="selected"':''}>业务系统</option>
                                                   </select>

```

* JSP页面 获取后台 重定向方式：(redirect)  传参方式： request.setAttribute("key",value)的对象或者属性值.

```java
   JAVA 后台：
       // 返回课程包装类的数据--用于页面显示
       request.setAttribute("courseDto", courseDto);     
```

```jsp
   <div class="static-item">
   	<div class="meta">难度级别</div>
   	<div class="meta-value">${courseDto.course.courseGrade }</div>
   </div> 
```

* JSP 



