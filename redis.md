# Redis命令的学习
## 一、什么是Redis
redis（Remote Dictionary Server）是key-value的存储系统, 通常被称为数据结构服务器，是个完全开源的且遵守BSD协议，是一个高性能的key-value数据库。

## 二、Key的基本操作

 、key */?/[] --- 列出库中所有的key(会导致阻塞问题，不会出有重复值)

 、scan cursor [match pattern] [count number] --- 根据条件pattern从0开始遍历所有key，知道返回的cursor是0表示遍历结束，这样不会导致阻塞，但是可能会有重复值

 、exsits key --- 检测key是否存在

 、del [key key1 key2 ...] --- 删除一个或者多个key

 、type key --- 返回key的value类型

 、randomkey --- 返回随机的key

 、rename oldkey newkey --- 重命名oldkey （renamenx 同）

 、expire key seconds --- 设置key的超时的秒数

 、pexpire key pseconds --- 设置key的超时的毫秒数

 、ttl key --- 查看key的剩余过期时间（-1：没有设置过过期时间， -2：key已经不存在了）

 、pttl key --- 同上，以毫秒返回生命周期

## 三、不同数据类型下的基本命令
### 1、字符串(string)

 、set key value --- 设置key值为value

 、mset key value --- 设置key及其值（可一次性设置多个key的value）

 、setnx key value --- 同上，其中nx表示not exists，只有key不存在的时候才set

 、msetnx key value --- 当key不存在时可以一次性设置多个key的值

 、get key --- 获取key

 、mget key --- 可以获取多个key的值

 、getset key value --- 获取key的旧值并设置新值

 、incr key --- 对key执行加的操作，并返回新值(key的值必须是int型，若incr不存在的key，则会设置key为1)
 
 、incrby key integer --- 执行指定数加的操作，integer是key指定加的数 

 、decr key --- 与incr相反(若key不存在则设置key为-1)

 、decrby key integer --- 同incrby相反，执行指定数减的操作

 、append key value --- 给key追加value值，并返回新字符串的值
 
 、substr key start end --- 截取key的值，并返回结果，note：原有值不变

 、strlen key --- 返回key的长度

 、setrange key offset value --- 改写key的值，如key值是34，setrange key 0 12，返回的值是124

 、getrange key start end --- 返回start到end之间的key的值的子字符串（key和end包含在内）

 、setbit key offset value --- 设置或清除key中存储的字符串值的偏移量位。offset最大2^32-1

 、getbit key offset --- 返回存储在key的字符串值中偏移量的位值。

 、bitcount key [start end] --- 返回key对应值中，被设置为1的二进制位的个数

 、bitop and/or/xor/not destkey key1 key2 --- 对1个或多个key对应的值进行AND/OR/XOR/NOT操作，并储存在新的key中

#### Note：redis-cli --raw 此命令可查看redis-cli下操作的中文字符

### 2、列表(list)

 、lpush key string --- 在key对应list的头部添加字符串元素，返回1表示成功，0表示key存在且不是list类型

 、rpush key string --- 在key对应的list的尾部添加字符串

 、lpushx key string1 string2 --- 在key对应的list的头部添加多个字符串（同时在尾部添加多个值用rpush）

 、linsert key [before/after] "value1" "new-value" --- 在key对应的list中的value1前/后添加新的值new-value

 、llen key --- 查看key对应list的长度

 、lindex key index --- 查看key对应list中index对应的值

 、lrange key start end --- 查看key对应list中的从start到end中的值

 、ltrim key start end --- 截取key对应list，返回ok表示截取成功

 、lrem key count value --- 删除list中count个与value相同的元素[count为0表示删除所有与value同值的元素，-count表示从右开始count个与value同值的元素]

 、lpop key --- 从key对应的list的头部删除元素

 、rpop key --- 与lpop相反，它从尾部

 、lset key index value --- 重置key对应list中存在的index的值

 、blpop key key1 key2 timeout --- key对应的list存在，从list的左到右删除list中元素并返回该元素，若key不存在，遍历key1，执行所属操作，以此类推，timeout超时时间

 、brpop key key1 key2 timeout --- 同上相似，只是从右到左（都实现了先到先服务的原则）timeout超时时间

 ### 3、集合

 、sadd key member --- 向集合key中添加member

 、smembers key --- 获取集合key中的元素

 、srem key member --- 移除集合key中的member元素

 、spop key --- 从key的尾部删除元素并返回被删除的元素

 、srandmember key --- 随机返回集合key中的元素

 、smove srckey dstkey member --- 从srckey中将member移动到dstkey中

 、scard key --- 查看集合key的大小

 、sismember key member --- 判断集合key中是否存在元素member，存在返回1，不存在或者key不存在返回0

 、sinter key1 key2 ... --- 返回所有给定key的相同的元素

 、sinterstore dstkey key1 key2 ... --- 同sinter，并同时保存交集到dstkey中

 、sunion key1 key2 ... --- 返回所有给定key的并集

 、sunion dstkey key1 key2 ... --- 同sunion，并同时保存并集到dstkey中

 、sdiff key1 key2 ... --- 返回所有给定key的差集

 、sdiffstore dstkey key1 key2 ... --- 同sdiff，并同时保存差集到dstkey中

 ### 4、有序集合

 、zadd key [xx|nx|ch|incr] score member --- 添加元素到集合key，元素在集合中存在则更新对应score[xx:只更新，nx:值添加，incr:如同zincrby]

 、zincrby key increment element --- 增加有序集合key中element的sorce值[increment:是有效的数字]

 、zrange key start end [withscores] --- 返回有序集合key中从start到end之间的元素，withscores：同时返回scores

 、zrevrange key start end 同上，返回结果是按score逆序的,如果需要得分则加上withscores

 、zrangebyscore key min max [withscores] --- 返回给定分数区间的有序集合

 、zcount key min max --- 返回给定区间中score的个数[min:-inf(负无穷)，max:+inf(正无穷)]

 、zcard key --- 返回有序集合key的个数

 、zscore key element --- 返回有序集合中element对应的score(index)

 、zrem key element --- 删除key中element的元素

 、zremrangebyrank key min max --- 删除key中排名在指定范围内的元素

 、zremrangebyscore key min max --- 删除key中score在指定范围内的元素

 、zrank key element --- 返回指定元素在集合中的排名(下标非分数),集合中元素是按score从小到大排序的

 、zrevrank key element --- 同上，但是集合中元素是按score从大到小排序的

 ### 5、散列(hash---哈希)

 、hset key field value --- 设置hash中key的field对应的值为value

 、hsetnx key field value --- 设置hash field为指定值，如果field已经存在，返回0，nx是not exist的意思

 、hmset key field1 value1 field2 value2 --- 设置hash中key对应的多个field的值

 、hget key field --- 获取hash field的值

 、hmget key field1 field2 --- 获取多个hash field对应的值

 、hincrby key field integer --- 给field增加integer个值

 、hexists key field --- 判断key中field是否存在

 、hdel key field --- 删除field

 、hlen key --- 获取key的长度

 、hkeys key --- 获取key中的field

 、hvals key --- 获取key中所有field对应的值

 、hgetall key --- 获取key中所有的field及其对应的值

 ### 6、HyperLogLog的操作

 、pfadd key element [element...] --- 将元素添加到HyperLogLog中

 、pfcount key [key...] --- 返回key中基数的计算值

 、pfmerge destkey key1 key2 ... --- 将多个key1、key2等等合并到destkey中













 













