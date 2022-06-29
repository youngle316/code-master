## 什么是数组
> 数组就是存放在连续内存空间上的相同类型数据的集合

由于数组在内存空间的地址是连续的，所以当对数组删除或者添加元素的时候，就难免的要移动其他元素的地址。这也是一个耗性能的操作。

尤其是当直接使用数组的 API 时，进行时间复杂度计算的时候，需要将 API 内部时间复杂度计算进去