#Jquery 笔记

* jquery 遍历

  ``
      $("li").each(function(){
        alert($(this).text())
      });
  ``
* jquery 获取标签文本
  ``
     $(this).text();
  ``
  
* jquery 获取 h5 dom元素内 value属性的值
 ``
   $("#ID").val();
 ``
  
  
  
  
  
  
  
  
  
  
  
  
 ## jquery 获取 元素内的值
 
 
 *jquery 获取下拉框 'SELECT' 选择的值
 
  ``
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
                               
  ``
  
## javascript 笔记
  
*  js内通过 EL表达式 获取集合对象，直接是一个数组对象。不需要 Json 进行对象转换。


* js 遍历 整个对象获取整个对象 Key的集合。
 ``
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
 ``

  