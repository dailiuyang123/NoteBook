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
  
* jquery 
  
  
  
  
  
  
  
  
  
  
  
  
  
  
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
  