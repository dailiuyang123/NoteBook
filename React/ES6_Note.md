# ES6 Note

* 基础语法：


##### 对象新增方法 
  
  ```javascript
   1. Object.is()
   2. Object.assign()
   3. Object.getOwnPropertyDescriptors()
   4. __proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf()
   5. Object.keys()，Object.values()，Object.entries()
   6. Object.fromEntries()
``` 
  * Object.is() 它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。
    ```javascript
       Object.is('foo', 'foo')
       // true
       Object.is({}, {})
       // false 
       
    ```
  * Object.assign() Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）
    ```javascript
        const target = { a: 1, b: 1 };
        
        const source1 = { b: 2, c: 2 };
        const source2 = { c: 3 };
        
        Object.assign(target, source1, source2);
        target // {a:1, b:2, c:3}
        
        // 除此之外。此方法还可用于 对象值拷贝(浅拷贝)(js 有引用拷贝的问题！)
        Object.assign({},obj);
        Object.assign([],arry);
    
    ```
    
  * Object.keys()  返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名 
    ```javascript
      var obj = { foo: 'bar', baz: 42 };
      Object.keys(obj)
      // ["foo", "baz"]

    ```
  * Object.values() 返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。
    ```javascript
    const obj = { foo: 'bar', baz: 42 };
    Object.values(obj)
    // ["bar", 42]

    返回数组的成员顺序，与本章的《属性的遍历》部分介绍的排列规则一致。
    
    const obj = { 100: 'a', 2: 'b', 7: 'c' };
    Object.values(obj)
    // ["b", "c", "a"]
    上面代码中，属性名为数值的属性，是按照数值大小，从小到大遍历的，因此返回的顺序是b、c、a。
        
    ```
    
  *  Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。
    
    ```javascript
        const obj = { foo: 'bar', baz: 42 };
        Object.entries(obj)
        // [ ["foo", "bar"], ["baz", 42] ]    
        //除了返回值不一样，该方法的行为与Object.values基本一致。
        
         Object.entries方法的另一个用处是，将对象转为真正的Map结构。
         const obj = { foo: 'bar', baz: 42 };
         const map = new Map(Object.entries(obj));
         map // Map { foo: "bar", baz: 42 }
    ```
  * Object.fromEntries()方法是Object.entries()的逆操作，用于将一个键值对数组转为对象。
     ```javascript
        Object.fromEntries([
          ['foo', 'bar'],
          ['baz', 42]
        ])
        // { foo: "bar", baz: 42 }
        该方法的主要目的，是将键值对的数据结构还原为对象，因此特别适合将 Map 结构转为对象。
        // 例一
        const entries = new Map([
          ['foo', 'bar'],
          ['baz', 42]
        ]);
        
        Object.fromEntries(entries)
        // { foo: "bar", baz: 42 }
        
        // 例二
        const map = new Map().set('foo', true).set('bar', false);
        Object.fromEntries(map)
        // { foo: true, bar: false }

     ```
     
  ##### Set 和 Map 数据结构
     
  * ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。 
    
    ```javascript
        Set本身是一个构造函数，用来生成 Set 数据结构。
            
        const s = new Set();
        
        [2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
        
        for (let i of s) {
          console.log(i);
        }
        // 2 3 5 4
    
        Set函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化
        
        // 例一
        const set = new Set([1, 2, 3, 4, 4]);
        [...set]
        // [1, 2, 3, 4]
        
        // 例二
        const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
        items.size // 5
        
        // 例三
        const set = new Set(document.querySelectorAll('div'));
        set.size // 56
        
        // 类似于
        const set = new Set();
        document
         .querySelectorAll('div')
         .forEach(div => set.add(div));
        set.size // 56
        
    ```
  * Set 实例的属性和方法
    ```javascript
       Set.prototype.constructor：构造函数，默认就是Set函数。
       Set.prototype.size：返回Set实例的成员总数。
        
    ```