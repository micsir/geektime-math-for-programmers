# 02 | 余数：原来取余操作本身就是个哈希函数

### 阅读前问题

- pre-1: 什么地方可以用到余数？

### notes

余数是可以固定在一个范围内

**同余定理**: a % m === b % m, a b 对模 m 同余

#### 应用：

- 百万数据存储

  - 针对若干连续空间 => f(x) = x % size 来指定同余的数放在那个空间

  - 利用随机数 => max => f(x) = (x + max) % size 数据分配更加随机，数据重新洗牌

- hash（哈希，散列）

- 加密

### 阅读中问题

1. 寻址和求余操作的寻址联系，时间关系？