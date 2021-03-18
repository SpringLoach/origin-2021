## 队列数据结构  
> 队列是遵循 **先进先出(FIFO)** 原则的一组有序的项。队列在尾部添加新元素，从头部移除元素。  
> 
> 生活中一个例子就是排队去打饭，当然了，大家又乖又饿，既不会插队，也不会中途跑掉。  

**创建队列**  
> 其中 count 将用于添加尾部元素；lowestCount 用于动态地删除头部元素。
```
class Queue {
    constructor() {
        this.count = 0;         
        this.lowestCount = 0;   
        this.items = {};
    }
}  
```  
**判断队列是否为空**   
```
isEmpty() {
    return this.count - this.lowestCount === 0;
}
```   
**向队列添加元素**  
```
enqueue(element) {
    this.items[this.count] = element;
    this.count++;
}
```  
**从队列移除元素**  
>  比起数组，对象在获取元素时能更高效。 
>  
> pop 删除最后的数组元素； delete 可用于删除指定对象元素。
> 有元素时，才进行移除操作。
```
dequeue() {
    if (this.isEmpty()) {
        return undefined;
    }
    const result = this.items[this.lowestCount];
    delete this.items[this.lowestCount];
    this.lowestCount++;
    return result;
}
```  
**查看队列头部元素**  
```
peek() {
    if (this.isEmpty()) {
        return undefined;
    }
    return this.items[this.lowestCount];
}
```  
**获取队列长度**  
> 等于入栈数减出栈数。
```
size() {
    return this.count - this.lowestCount;
}
```  
**清空队列**  
> 简单点的方法就是直接初始化，当然也可以不断调用 dequeue 方法。
```
clear() {
    this.items ={};
    this.count = 0;
    this.lowestCount  = 0;
}
```  
**创建 toString 方法**  
> 需要从**索引值**为 lowestCount 的位置开始迭代队列。
```
toString() {
    if (this.isEmpty()) {
        return '';
    }
    let str = `${this.items[this.lowestCount]}`;
    for (let i = this.lowestCount + 1; i< this.count; i++) {  // 加入一个参数进行循环操作。
        str = `${str},${this.items[i]}`;
    }
    return str;
}
```  

## 双端队列数据结构  
> 双端队列是一种允许我们同时从前端和后端添加和移除元素的特殊队列。
> 
> 同时遵循 **先进先出** 和 **后进先出** 原则，可以说是一种把队列和栈相结合的数据结构。  

**创建 Deque 类**  
> 它有队列的所有方法，还能像栈一样移除（ 或返回 ）后端的第一个元素，实现方法相同。
```
class Deque {
    constructor() {
        this.count = 0;         
        this.lowestCount = 0;   
        this.items = {};
    }
}  
```  
**向前端添加元素**  
> 之前未实现过的方法。 
>  
> 第一种情况主要为了处理未曾操作过的空队列。  
> 第三种情况表示未曾在开头弹出过元素，或 lowestCount 索引不够用。
```
addFront(element) {
    if (this.count - this.lowestCount === 0) {
        this.items[this.count] = element;
        this.count++;
    } else if (this.lowestCount > 0) {
        this.lowestCount--;
        this.items[this.lowestCount] = element;
    } else {
        for (let i = this.count; i > 0; i--) {
            this.items[i] = this.items[i-1];
        }
            this.count++;
            this.lowestCount = 0;
            this.items[0] = element;
    }
}
```


 

