# 二叉堆  
> 二叉堆是一种特殊的二叉树，有以下两个特性。  

- 结构特性：它是一棵**完全二叉树**，表示树的每一层都有左侧和右侧子节点（除了最后一层的叶节点），并且**最后一层的叶节点尽可能都是左侧子节点**。
- 堆特性：二叉堆不是最小堆就是最大堆。最大堆允许你快速导出树的最大值。**所有的节点都大于等于每个它的子节点**。

## 创建最小堆类    
**骨架**  
```
class MinHeap {
    constructor(compareFn = defaultCompare) {
        this.compareFn = compareFn;
        this.heap = [];
    }
}
```  
**比较函数**   
```
function defaultCompare(a,b) {
    if (a < b) {
        return '1';
    } else if (a > b) {
        return '2';
    }
}
```  
**访问某节点的左/右子节点/父节点的索引值**  
```
getLeftIndex(index) {
    return 2 * index + 1;
}
getRightIndex(index) {
    return 2 * index + 2;
}
getParentIndex(index) {
    if (index === 0) {
        return undefined;
    }
    return Math.floor((index - 1) / 2);
}
 ```
### 向堆中插入值  
> 先将值插入数组的最后一个位置，再上移。  
```
insert(value) {
    if (value != null) {
        this.heap.push(value);
        this.siftUp(this.heap.length - 1);
        return true;
    }
    return false;
}
```  
**上移操作**  
> 将这个值和它的父节点进行交换，直到父节点小于这个插入的值。
```
siftUp(index) {
    let parent = this.getParentIndex(index);
    while(
        index > 0 && 
        this.compareFn(this.heap[index], this.heap[parent]) == 1
      ){
         this.swap(this.heap, parent, index);  // 元素（值）交换
        index = parent;
        parent = this.getParentIndex(index);
    }
}
    
swap(array, a, b) {
    const temp = array[a];
    array[a] = array[b];
    array[b] = temp;
}
```

### 从堆中找到最小值  
```
findMinimum() {
    return this.isEmpty() ? undefined : this.heap[0];
}

size() {
    return this.heap.length;
}
isEmpty() {
    return this.size() === 0;
}
```

### 导出堆中的最小值  
> 移除数组的第一个元素后，将最后的元素移至根部并进行下移。  
```
extract() {
    if (this.isEmpty()) {
        return undefined;
    }
    if (this.size() === 1) {
        return this.heap.shift();
    }
    const removeValue = this.heap.shift();
    this.heap.unshift(this.heap.pop()); // 验证
    this.siftDown(0);
    return removeValue;
}
```
**下移操作（堆化）**  
> 将这个值和它的左/右子点中的较小者进行交换，直到底部。  
```
siftDown(index) {
    let element = index;
    const left = this.getLeftIndex(index);
    const right = this.getRightIndex(index);
    const size = this.size();
    if (
        left < size && 
        this.compareFn(this.heap[element], this.heap[left]) == 2
      ) {
        element = left;
    }
    if (
        right < size && 
        this.compareFn(this.heap[element], this.heap[right]) == 2
      ) {
        element = right;
    }
    if (index !== element) {
        this.swap(this.heap, index, element);
        this.siftDown(element);
    }
}
```  

## 创建最大堆类  
> 拓展最小堆类，并在需要时进行方向的比较即可。  
```
class MaxHeap extends MinHeap {
    constructor(compareFn = defaultCompare) {
        super(compareFn);
        this.compareFn = this.reverseCompare(compareFn);
    }
    reverseCompare(compareFn) {
        return (a,b) => compareFn(b,a);
    }
        // 最后
}
```


