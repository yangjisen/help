###  String操作
 *  字符串操作

##

* 设置键值：成功返回true, 否则返回false, 键值不存在则新建, 否则覆盖
```
$redis->set('string', 'hello world!');
```

* 从左往右第五个字符开始替换为另一指定字符串, 成功返回替换后新字符串的长度.
```
$redis->setRange('string',6, '1111');
```


* 截取字符串里指定key对应的value里的第一个到第七个字符.
```
$redis->getRange('string', 0, 6);
```

* 添加键, 返回旧键值：若key不存在则创建键值, 返回false
```
$redis->getSet('ad', 'hi man');
```

* 一次设置多个键值对：成功返回true
```
$redis->mset(['name' => 'jet', 'age' => 18]);
```

* 一次获取多个key的值：返回一个键值对数组, 其中不存在的key值为false.
```
$redis->mget(['name', 'age']);
```

* 创建一个具有时间限制的键值, 过期则删除, 秒为单位, 成功返回true
```
$redis->setex('name', 10, 'jetwu');
```

* 创建一个具有时间限制的键值, 过期则删除, 毫秒为单位, 成功返回true
```
$redis->psetex('name', 10, 'jetwu');
```

* key的值不存在时, 添加key并返回true, key存在返回false.
```
$redis->setnx('name', 'boby');
```

* setnx命令的批量操作.只有在给定所有key都不存在的时候才能设置成功, 只要其中一个key存在, 所有key都无法设置成功.
```
$redis->msetnx(['name' => '11', 'name1' => '22']);
```

* 获取指定key存储的字符串的长度, key不存在返回0, 不为字符串返回false.
```
$redis->strlen('name');
```

* 将指定key存储的数字值增加1.若key不存在会先初始化为0再增加1, 若key存储的不是整数值则返回false.成功返回key新值.
```
$redis->incr('name');
```

* 给指定key存储的数字值增加指定增量值.
```
$redis->incrBy('age', 10);
```

* 给指定key存储的数字值增加指定浮点数增量.
```
$redis->incrByFloat('age', 1.5);
```

* 将指定key存储的数字值减一.
```
$redis->decr('age');
```

* 将指定key存储的数字值减去指定减量值.
```
$redis->decrBy('age', 10);
```

* 为指定key值尾部添加字符, 返回值得长度, 若key不存在则创建
```
$redis->append('name', 'haha');
```

* 获取键值：成功返回String类型键值, 若key不存在或不是String类型则返回false
```
$redis->get('name');
```

