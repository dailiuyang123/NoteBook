#JSP CODE 

* js文件内无法解析 EL表达式        解决方案
 
 ``
  /<script type="text/javascript">
      var ctx = "${ctx}";
  </script>/
  在jsp页面内 获取EL 表达式的值，然后将值设为 全局变量即可
 ``
* jsp 