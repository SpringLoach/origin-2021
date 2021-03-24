# 集合  
> 集合是一组无序且**唯一**（即不能重复）的项组成的。
> 
> 实际操作中，当属性为整数时，有[自动排序的现象](https://blog.csdn.net/ccnacyq/article/details/109172104)？  

**创建集合类**  
> JavaScript 的对象不允许一个键指向两个不同的属性，也保证了集合里的元素都是唯一的。  
```
class Set {
    constructor() {
        this.items = {};
    } 
} 
```  
**检查某元素是否存在**  
```
has(element) {
    return Object.prototype.hasOwnProperty.call(this.items,element);
}
```  
**向集合添加一个新元素**  
> 如果属性值已存在，不操作。  
```
add(element) {
    if (!this.has(element)) {             
        this.items[element] = element;    // 同时作为键和值保存
        return true;
    }
    return false;
}
```  
**从集合移除一个元素**  
```
delete(element) {
    if (this.has(element)) {
        delete this.items[element];
        return true;
    }
    return false;
}
```  
**清空集合**  
```
clear() {
    this.items = {};
}
```  
**返回集合中有多少元素**  
> `for-in` 语句将迭代 items对象的所有属性，包括对象的原型所包含的额外属性。  
```
size() {
    let count = 0;
    for(let key in this.items) {    
         if(this.items.hasOwnProperty(key)) {    // 检查他们是否是对象自身的属性。
            count++;
        }
    }
    return count;
}
```   
**返回一个包含集合中所有值（元素）的数组**  
```
values() {
     let values = [];
     for(let key in this.items) {
         if(this.items.hasOwnProperty(key)) {
             values.push(key);
         }
     }
     return values;
}
```

