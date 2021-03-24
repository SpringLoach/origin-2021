## 字典  
> 在字典中，用\[键，值]对的形式来存储数据。
> 
> 字典也称作**映射**、**符号表**、或**关联数组**。  

### 创建字典类  
骨架
```
class Dictionary {
    constructor(toStrFn = defaultToString) {
        this.toStrFn = toStrFn;
        this.table = {};
    }
}
```  
defaultToString 函数  
> 用于保证将原始键字符串化。  
```
function defaultToString(item) {
    if (item === null) {
        return 'NULL';
    } else if (item === undefined) {
        return 'UNDEFINED';
    } else if (typeof item === 'string' || item instanceof String) {
        return `${item}`;  // 直接返回
    }
    return item.toString();
}
```  
ValuePair 类
> 将用于充当 table 的属性值，保存了原始键和原始值，改变了默认to..方法。  
```
class ValuePair {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }
    toString() {
        return `[#${this.key}: ${this.value}]`;
    }
}
```
**检查一个键是否存在于字典中**  
```
hasKey(key) {
    return this.table[this.toStrFn(key)] != null;
}
```  
**在字典中添加新元素**  
> 如果 key 已经存在，那么已存在的 value 会被新的值覆盖。  
```
set(key, value) {
    if (key != null && value != null) {
        const tableKey = this.toStrFn(key);  // 用字符串化的键作键
        this.table[tableKey] = new ValuePair(key, value);
        return true;
    }
    return false;
}
```  
**从字典中移除一个值**  
```
remove(key) {
    if (this.hasKey(key)) {
        delete this.table[this.toStrFn(key)];
        return true;
    }
    return false;
}
```  
**从字典中检索一个值**  
> 若先验证是否存在，会消耗更多。  
```
get(key) {
    const valuePair = this.table[this.toStrFn(key)];
    return valuePair == null? undefined : valuePair.value;
}
```
**以数组形式返回字典中的所有\[原始键，值]对**  
> `Object.values(obj)` 返回对象自身的所有 **可枚举属性值** 的数组。  
```
keyValues() {
    return Object.values(this.table);
}
```
**以数组形式返回字典中的所有原始键**  
> `map` 对数组中的每个元素运行给定函数，返回 **每次函数调用的结果** 组成的新数组。  
```
keys() {
    return this.keyValues().map(valuePair => valuePair.key);
}
```  
**以数组形式返回字典中的所有值**  
```
values() {
    return this.keyValues().map(valuePair => valuePair.value);
}
```  
**迭代字典中所有的键值对**  
> 该方法可以在回调函数返回 `false` 时被中止（和 Array类的 every方法类似）。  
> 
> 这个 callbackFn 需要自己设置吧。。
```
forEach(callbackFn) {
    const valuesPairs = this.keyValues();
    for (let i = 0; i < valuesPairs.length; i++) {
        const result = callbackFn(valuePairs[i].key,valuePairs[i].value);
        if (result === false) {
            break;
        }
    }
}
```  
**字典所包含的\[键,值]对数量**  
> `Object.keys(obj)` 返回对象的所有 **可枚举属性** 的字符串数组。  
```
size() {
    return Object.keys(this.table).length;
}
```  
**检验字典是否为空**  
```
 isEmpty() {
    return this.size() === 0;
}
```  
**清空字典**  
```
clear() {
    this.table = {};
}
```  
**创建 toString 方法**  
```
toString() {
    if (this.isEmpty()) {
        return '';
    }
    const valuePairs = this.keyValues();  // 转化为数组
    let objString = `${valuePairs[0].toString()}`;
    for (let i = 1; i < valuePairs.length; i++) {
        objString = `${objString},${valuePairs[i].toString()}`;
    }
    return objString;
}
```  

## 散列表  
> 散列算法的作用是尽可能**快**地在数据结构中找到一个值。  

### 创建散列表  

骨架  
```
class HashTable {
    constructor(toStrFn = defaultToString) {
        this.toStrFn = toStrFn;
        this.table = {};
    }
}
```
创建散列方法  
> lose lose散列函数：简单地将每个键值中的每个字母的 ASCII 值相加。
```
loseloseHashCode(key) {
    if (typeof ley === 'number') {
        return key;
    }
    const tableKey = this.toStrFn(key);  // 转化为字符串
    let hash =0;
    for (let i = 0; i < tableKey.length; i++) {
        hash += tableKey.charCodeAt(i);
    }
    return hash % 37;  
}
```  
调用散列方法  
```
hashCode(key) {
    return this.loseloseHashCode(key);
}
```

**向散列表增加（更新）一个的项**  
> 创建了一个 ValuePair 实例。  
```
put(key,value) {
    if (key != null && value != null) {
        const position = this.hashCode(key);  // 用处理后的键作键
        this.table[position] = new ValuePair(key, value);
        return true;
    }
    return false;
}
```  
**从散列表中获取一个值**  
> 与字典不同的是，散列表中的键使用 hash 转化而非字符串化。  
```
get(key) {
    const valuePair = this.table[this.hashCode(key)];
    return valuePair == null? undefined : valuePair.value;
}
```
**从散列表中移除某项**  
```
remove(key) {
    const valuePair = this.table[this.hashCode(key)];
    if (valuePair != null) {
        delete this.table[this.hashCode(key)];
        return true;
    }
    return false;
}
```  







