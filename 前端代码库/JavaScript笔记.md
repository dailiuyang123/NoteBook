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

* 字符串转数组，数组转数组格式化，数组格式化转数组
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

##### js 【Array API】
  
* push()
   ```javascript
    var arr = [1,2,3]
    console.log(arr.push(4)) // 4
    console.log(arr) // [1,2,3,4]
   ```
* unshift()
  ```javascript
     向数组的开头添加一个或更多元素，并返回新的长度
     var arr = [1,2,3] 
     console.log(arr.unshift(4)) // 4
     console.log(arr) // [4,1,2,3]
  ```
* shift()
  ```javascript
     删除并返回数组的第一个元素
     var arr = [1,2,3] 
     console.log(arr.shift()) // 1
     console.log(arr) // [2,3]
  ```
* pop() 
  ```javascript
     删除并返回数组的最后一个元素
     var arr = [1,2,3] 
     console.log(arr.prop()) // 3
     console.log(arr) // [1,2]
  ``` 
* join()   
  ```javascript
     把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。
     var arr = [1,2,3] 
     arr.join('+') //"1+2+3"
  ```
* toString()
  ```javascript
     该方法可把数组转换为字符串，返回值与没有参数的 join() 方法返回的字符串相同。
     var arr = [1,2,3] 
     arr.toString() // "1,2,3"
  ```
* concat()
  ```javascript
     该方法可以连接两个或更多的数组，并返回结果
     var arr1 = [1,2,3] 
     var arr2 = [4,5,6]
     arr1.concat(arr2) //[1,2,3,4,5,6] 
  ```
* slice(start,end)
  ```javascript
     该方法可从已有的数组中返回选定的元素。(返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。),不传参返回整个数组，传入负值(等价于负值＋数组长度的位置开始)
     
     该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。
     var arr = [1,2,3] 
     arr.slice(1) // [2,3]
     arr.slice(0,2) // [1,2]
     arr.slice() // [1,2，3]
     arr.slice(－1) // [3]
    
  ```
* splice(arg1,arg2,arg3)
  ```javascript 
     参数1 添加／删除 的起始位置
     
     参数2 要删除的项目数量。如果设置为 0，则不会删除项目。
     
     参数3 向数组添加的新项目。(可以添加多个)
     
     1）单纯的删除元素 (这时不用传参数3，用参数1、2控制即可)返回的是一个包含被删除元素的数组,如果参数1为负值，则相当于从参数1+数组长度的位置开始删除。
     
     var arr = [1,2,3,4,5]
     arr.splice(1,2) // ［2，3］
     arr.splice(－2,2) // [4,5] 
     2）单纯的添加元素 (这时参数2要传入0)返回值是一个空数组,如果参数1为负值，则相当于从参数1+数组长度的位置开始添加。
     
     var arr = [1,2,3,4,5]
     arr.splice(1,0,6);  // []
     console.log(arr )  // [1, 6, 2, 3, 4, 5]
     arr.splice(－1,0,6);  // []
     console.log(arr )  // [1,2, 3, 4, 6，5]
     3)  删除元素并添加元素 返回值是包含新被删除元素的一个数组，如果参数1为负值，则相当于从参数1+数组长度的位置开始删除/添加。
     
     var arr = [1,2,3,4,5]
     arr.splice(1,3,6,7,8);  // [2,3,4]
     console.log(arr )  // [1, 6, 7, 8, 5]
     arr.splice(-1,3,6,7,8);  // [5]
     console.log(arr )  // [1, 2,3,4,6,7,8]
     
     
  ```
##### js 定时器
  * 1.倒计定时器：timename=setTimeout("function();",delaytime);
    
  *  2.循环定时器：timename=setInterval("function();",delaytime);


