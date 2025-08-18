# 常用方法

### String类

| 方法名                             | 返回值  | 作用                                             |
| ---------------------------------- | ------- | ------------------------------------------------ |
| **增**                             |         |                                                  |
| concat（String）                   | String  | 连接字符串至结尾                                 |
| **改**                             |         |                                                  |
| replace（char old，char new）      | String  | 把字符串中的所有old替换成new                     |
| split（String regex，[int limit]） | String  | 按给定的正则表达式分隔字符串[至limit]            |
| substring（int begin，[int end]）  | String  | 截取字符串，从[begin,end)                        |
| **trim（）**                       | String  | 返回字符串的副本，忽略前导空白和尾部空白         |
| toLowCase<br />toUpperCase         | String  | 转换为小写/大写字符串并返回                      |
| getBytes（String s）               | byte[]  | 将String编码为byte序列，存储至新数组             |
| **查**                             |         |                                                  |
| charAt（int）                      | char    | 返回索引处的字符                                 |
| contains（String）                 | boolean | 判断是否包含String字符串                         |
| length（）                         | int     | 返回字符串长度                                   |
| isEmpty（）                        | boolean | 判断字符串是否为空                               |
| equals（Object）                   | boolean | 默认比较两个对象（地址）是否相等，重写后比较内容 |
| starsWith<br />endsWith（String）  | boolean | 是否以String为前缀/后缀                          |
| indexOf<br />lastIndexOf（String） | int     | 返回首次出现的索引                               |
| matches(String regex)              | boolean | 判断是否匹配正则表达式                           |
| compareTo（String）                | int     | 按字典顺序比较两个字符串，之前则为负数。否则为正 |
|                                    |         |                                                  |

### StringBuffer类

| 方法名                                      | 返回值       | 作用                              |
| ------------------------------------------- | ------------ | --------------------------------- |
| **append（String）**                        | StringBuffer | 尾部追加字符串                    |
| **insert（int，int/String）**               | void         | 向字符串的int位置，插入int/String |
| **delete（int begin，int end）**            | void         | 删除begin->end的字符              |
| **replace(int start, int end, String str)** | void         | 替换start->end为str               |
| **reverse（）**                             | StringBuffer | 反转字符串并返回                  |
| **capacity()**                              | int          | 返回字符串容量                    |



### ArrayList类

| 方法名                            | 返回值  | 作用                                 |
| --------------------------------- | ------- | ------------------------------------ |
| **增**                            |         |                                      |
| add<br />addAll（int，E element） | boolean | 将元素/集合所有元素插入到int位置中   |
| **删**                            |         |                                      |
| remove（E）                       |         | 移除元素E                            |
| clear（）                         |         | 删除 arraylist 中的所有元素          |
| **改**                            |         |                                      |
| toArray（）                       |         | 转换为数组                           |
| toString（）                      |         | 转换为字符串                         |
| subList（）                       |         | 截取部分 arraylist 的元素            |
| **查**                            |         |                                      |
| forEach（action）                 |         | 遍历集合中的每一个元素并执行特定操作 |
| size（）                          | int     | 返回元素数量                         |
| isEmpty（）                       | boolean | 判断是否为空                         |
| contains（）                      |         | 判断元素是否存在                     |
| get（int）                        |         | 获取索引为int的元素                  |
| indexOf<br />lastIndexOf（）      |         | 返回元素索引值                       |
| sort（）**[继承List接口]**        | void    | 对元素排序                           |

### **LinkedList类**

| **方法名**                                    | **返回值**  | **作用**                                                     |
| --------------------------------------------- | ----------- | ------------------------------------------------------------ |
| **add/addAll（[int]，E element）**            | **boolean** | **将元素/集合所有元素插入到[int]位置中，并返回t/f**          |
| **addFirst(E e)**                             | **void**    | **元素添加到头部。**                                         |
| **addLast(E e)**                              | **void**    | **元素添加到尾部。**                                         |
| **offer(E e)<br />offerFirst<br />offerLast** | **boolean** | **向链表末尾添加元素，返回是否成功，成功为 true，失败为 false。（超出容量返回false不抛出异常）** |
| **remove (int)**                              |             | **删除并返回指定int位置的元素**                              |
| **removeFirst() / removeLast()**              |             | **删除并返回 首个/最后 元素。**                              |
| **poll ()**                                   |             | **删除并返回第一个元素。**                                   |
| **clear()**                                   |             | **清空链表**                                                 |
| **get(int index)**                            |             | **返回指定位置的元素**                                       |
| **contains(Object o)**                        |             | **判断是否含有某一元素。**                                   |



### **HashSet类**

- **基于HashMap实现，不允许有重复元素**
- **线程不安全**
- **允许有null值**
- **元素无序**
- **可以使用for-each（）语句迭代集合内元素**

| **方法名**    | **返回值** | **作用** |
| ------------- | ---------- | -------- |
| **add**       |            |          |
| **remove**    |            |          |
| **clear（）** |            |          |
| **contains**  |            |          |
| **size（）**  |            |          |



### **Number&Math类**

| **方法名**                           | **返回值** | **作用**               |
| ------------------------------------ | ---------- | ---------------------- |
| **abs（Number）**                    |            | **返回绝对值**         |
| **max（Number...）**                 |            | **返回最大值**         |
| **min（Number...）**                 |            | **返回最小值**         |
| **pow（int a，int b）**              |            | **返回a的b次方**       |
| **sqrt（）**                         |            | **求参数的算数平方根** |
| **sin / cos / tan / asin / acos...** |            | **三角函数**           |
| **random（）**                       | **double** | **返回随机数**         |
|                                      |            |                        |

# 日期类

### 1. `LocalDate`、`LocalTime` 和 `LocalDateTime`

- **`LocalDate`**：表示不带时区的日期（年-月-日）。
- **`LocalTime`**：表示不带时区的时间（小时-分钟-秒）。
- **`LocalDateTime`**：表示不带时区的日期和时间组合。

### 2. `ZonedDateTime`

表示带有**时区**的日期和时间，适用于需要处理不同时区的应用场景。

### 3. `Duration` 和 `Period`

- **`Duration`**：用于表示两个时间点之间的时间差（如秒、分钟、小时等）。
- **`Period`**：用于表示两个日期之间的日期差（如天、月、年等）

### 4. `DateTimeFormatter`

用于格式化和解析日期时间对象，提供了灵活的格式化选项。
