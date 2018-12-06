#java NOTE

* java 自定义集合排序
```java
  lists.sort(new Comparator<T>() {
             @Override
             public int compare(T_cms_navlink o1, T_cms_navlink o2) {
                 return o2.getOrdernum().intValue()-o1.getOrdernum().intValue();
             }
         });

```
