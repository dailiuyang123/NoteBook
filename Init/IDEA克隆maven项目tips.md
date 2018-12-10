#    IDEA clone from github && github attention

* IDEA 要从git 上克隆项目时注意

# 如果是 Maven 管理的项目 . 克隆项目时。一定要选择 Maven 管理的形式。 如果选择默认方式构建的话。 所有的依赖都要手动引用。不要那样做！！！

```java
//错误信息摘要：
Error:(26, 23) java: 无法访问com.google.common.base.Predicate
  找不到com.google.common.base.Predicate的类文件
```