# React Note 

* React 之 import

```javascript
   //每一个模块只加载一次， 每一个JS只执行一次， 如果下次再去加载同目录下同文件，直接从内存中读取。 一个模块就是一个单例，或者说就是一个对象；
  import React, {Component,Fragment} from 'react';

```

* react 之 const 

 ```javascript
 //const定义的变量不可以修改，而且必须初始化 类似java中的静态常量
const modelkey = 'UserManageModel/';

```

* react 之 class
```javascript
class UserManage extends Component {
  //构造方法 constructor( ) 同 java 
  constructor() {
    super();
    this.bind();
    this.state = {
      activeKey: "1",
      authUserData:null,
      userDataSource: [],
      userTargetSource: [],
      userTargetSourceName:[],
      showTargetSource:[],
      onDeptTreeExpand:['00000001'],
      allDeptTreeInfo:[],
      deptId:'',
      deptCheckedKeys:[],
      jobDataSource:[],
      //jobTargetSource: [],
      deptJobInfo:{},
      allCheckedDeptJobInfo:{},
      checkedDeptJobInfo:[],
      autoExpandParent: true,
    }
  }
  
  
}
```

* react 之 export
```javascript

```

* react 之 css 样式调整
```javascript
    //注意 在react 内引用样式，要用双大括号的形式引用。 
   <div style={{float:"left"}}> </div>

```



