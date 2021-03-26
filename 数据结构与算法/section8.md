## 二叉搜索树   
> 二叉树的节点最多只能有两个子节点。  
> 二叉搜索树（BST）是二叉树的一种，但只允许在左侧节点存储（比父节点）小的值，在右侧节点存储（比父节点）大的值。  

### 创建 BinarySearchTree 类  


基本结构  
> 将声明一个变量以控制此数据结构的第一个节点。  
```
class BinarySearchTree {
    constructor(compareFn = defaultCompare) {
        this.compareFn = compareFn;
        this.root = null;
    }
}
```  

表示每个节点  
```
class Node {
    constructor(key) {
        this.key = key;
        this.left = null;
        this.right = null;
    }
}
```  

比较函数   
```
function defaultCompare(a,b) {
    if (a < b) {
        return '1';
    } else if (a > b) {
        return '2';
    }
}
```  

**向二叉搜索树插入一个键**  
```
insert(key) {
    if (this.root == null) {
        this.root = new Node(key);
    } else {
        this.insertNode(this.root,key);
    }
}

// 参数：当前进行比较的父节点，需要插入的子节点。
insertNode(node, key) {
    if (this.compareFn(key, node.key) == '1') {
        if (node.left == null) {
            node.left = new Node(key);
        } else {
            this.insertNode(node.left, key);
        }
    } else if (this.compareFn(key, node.key) == '2') {
        if (node.right == null) {
            node.right = new Node(key);
        } else {
            this.insertNode(node.right, key);
        }
    }
    return false;
}
```   

### 树的遍历  

**中序遍历（左中右）**  
> 以从最小到最大的顺序访问所有节点。    
```
inOrderTraverse(callback) {
    this.inOrderTraverseNode(this.root, callback);
}

inOrderTraverseNode(node, callback) {
    if (node != null) {
        this.inOrderTraverseNode(node.left,callback);
        callback(node.key);
        this.inOrderTraverseNode(node.right,callback);
    }
}
```  
> 方法接受一个**回调函数**作为参数，回调函数的参数在调用中已经给出。
> ```
> const y = (n) => document.write(n);
> x.inOrderTraverse(y);
> ```  

**先序遍历（中左右）**   
```
preOrderTraverse(callback) {
    this.preOrderTraverseNode(this.root, callback);
}

preOrderTraverseNode(node, callback) {
    if (node != null) {
        callback(node.key);
        this.preOrderTraverseNode(node.left,callback);
        this.preOrderTraverseNode(node.right,callback);
    }
}
```  
**后序遍历（左右中）**   
```
postOrderTraverse(callback) {
    this.postOrderTraverseNode(this.root, callback);
}
postOrderTraverseNode(node, callback) {
    if (node != null) {
        this.postOrderTraverseNode(node.left,callback);
        this.postOrderTraverseNode(node.right,callback);
        callback(node.key);
    }
}
```  

### 搜索树中的值  

**搜索最小值**  
> 最左侧的节点即这棵树中最小的键。
```
min() {
    return this.minNode(this.root);
}

// 我们可以使用它来找到一棵树或其子树中最小的键。
minNode(node) {
    let current = node;
    while (current != null && current.left != null) {
        current = current.left;
    }
    return current;
}
```  
**搜索最大值**  
```
max() {
    return this.maxNode(this.root);
}
maxNode(node) {
    let current = node;
    while (current != null && current.right != null) {
        current = current.right;
    }
    return current;
}
```  
**搜索一个特定的值**  
```
search(key) {
    return this.searchNode(this.root, key);
}

// 第一个参数为当前比较的父节点。
searchNode(node, key) {
    if (node == null) {
        return false;
    }
    if (this.compareFn(key, node.key) == '1') {
        return this.searchNode(node.left, key);
    } else if (this.compareFn(key, node.key) == '2') {
        return this.searchNode(node.right, key);
    } else {
        return true;
    }
}  
```  

### 移除一个节点  
```
remove(key) {
    this.root = this.removeNode(this.root, key);
}

removeNode(node, key) {
    if (node == null) {
        return null;
    }
    if (this.compareFn(key, node.key) == '1') {
        node.left = this.removeNode(node.left, key);
        return node;
    } else if (
            this.compareFn(key, node.key) == '2'
        ) {
        node.right = this.removeNode(node.right, key);
        return node;
    } else {
        // 键等于 node.key
        // 第一种情况：移除一个叶节点
        if (node.left == null && node.right == null) {
            node = null;
            return node;
        }
        // 第二种情况：带一个子节点
        if (node.left == null) {
            node = node.right;
            return node;
        } else if (node.right == null) {
            node = node.left;
            return node;
        }
        // 第三种情况：带两个子节点
        const aux = this.minNode(node.right);
        node.key = aux.key;
        node.right = this.removeNode(node.right, aux.key);
        return node;
    }
}
```









