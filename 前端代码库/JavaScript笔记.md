#JavaScript 笔记

#####js 数组,字符串,json互相转换
  * 数组转字符串
  ```javascript
   var arr = [1,2,3,4,'巴德','merge'];
   var str = arr.join(',');
   console.log(str); // 1,2,3,4,巴德,merge
```
 * 字符串转数组
 ```javascript
var str = '1,2,3,4,巴德,merge';
var arr = str.split(',');
console.log(arr);     // ["1", "2", "3", "4", "巴德", "merge"]   数组
console.log(arr[4]);  // 巴德
  
```

*字符串转数组，数组转数组格式化，数组格式化转数组
```javascript
var str = '1,2,3,4,巴德,merge';
var arr = str.split(',');
var strify = JSON.stringify(arr);
console.log(arr);       // ["1", "2", "3", "4", "巴德", "merge"]   数组
console.log(arr[4]);    // 巴德
console.log(strify);    // ["1", "2", "3", "4", "巴德", "merge"]   字符串

var arrParse = JSON.parse(strify);
console.log(arrParse);  // ["1", "2", "3", "4", "巴德", "merge"]   数组
```