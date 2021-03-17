# 栈  
> 栈是一种遵从**后进先出**（ LIFO ）原则的有序集合。新添加或待删除的元素都保存在栈顶，另一端就叫栈底。  
> 
> 应用于浏览器的历史记录（ 返回 ）等。  

## 创建一个基于数组的栈  
```
class Stack {
    constructor() {
        this.items = [];     // 为示例添加一个名为 items 的属性，并初始化为空数组。
   }                         // 方法添加到这之后。
}
```  
**向栈添加元素**  
> 只添加到栈顶，也就是栈的末尾。  
```
push(element){                 // 这里的 push 为方法名，喜欢也可以改成别的。
    this.items.push(element);  // 这里的 push 则调用了数组方法。
}
```
**从栈移除元素**  
> 移除最后添加的元素。  
```
pop(){
    return this.items.pop();   // return 便于查看移除的值
} 
```  
**查看栈顶元素**  
```
peek(){
    return this.items[this.items.length-1];
}
```  
**检查栈是否为空**  
```
isEmpty(){
    return this.items.length === 0;
}
```
**查看栈的长度**  
```
size(){
    return this.items.length;
}
``` 
**清空栈元素**  
```
clear(){
    this.items = [];
}
```

## 创建一个基于对象的栈  
```
class Stack {
    constructor() {
        this.count = 0;    // 用于记录栈的大小等。
        this.items = {};
    }
}
```  
**向栈中插入元素**  
> 对象是一系列**键值对**的集合。
```
push(element){
    this.items[this.count] = element;
    this.count++;
}
```  
**检查栈是否为空**  
```
isEmpty(){
    return this.count === 0;
}
```
**查看栈的长度**  
``` 
size(){
    return this.count;
} 
```  
**从栈中弹出元素**  
```
pop(){
    if (this.isEmpty()){    // 等同于 this.count === 0
        return undefined;   // 比起之前基于数组建栈，这考虑的更周全。
    }
    this.count--;    
    const result = this.items[this.count];    // 创建一个临时变量以便最后返回弹出值
    delete this.items[this.count];
    return result;
}
```  
**查看栈顶的值**  
```
peek(){
    if (this.isEmpty()){
        return undefined;
    }
    return this.items[this.count - 1]
}
```
**清空栈元素**  
```
clear(){
    this.items = {};
    this.count = 0;
}
```  
> 遵循 LIFO 原则来移除所有栈元素。
> ```
> clear(){
>     while (!this.isEmpty()){
>         this.pop();
>     }
> }
> ```
**创建 toString 方法**  
```  
toString() {
    if (this.isEmpty()){
        return '';
    }                                      // 针对空对象
    let x = `${this.items[0]}`;            // 仅1个元素，无逗号； 
    for (let i = 1; i < this.count; i++){  // 多个元素，也不会以逗号开头。
        x = `${x},${this.items[i]}`;
    }
    return x;
}
```

