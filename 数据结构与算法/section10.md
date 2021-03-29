# 图  
> 图是一组由**边**连接的**节点**（或**顶点**）。  

## 邻接表  
> 可以使用一种叫做邻接表的动态数据结构来表示图。邻接表由图中每个顶点的相邻顶点列表所组成。   
> ![邻接表](邻接表.jpg)  

**声明骨架**  
> 默认为无向图。  
```
class Graph {
    constructor(isDirected = false) {
        this.isDirected = isDirected;
        this.vertices = [];  // 顶点列表 
        this.adjList = new Dictionary();  // 储存邻接表
    }
}
```

**添加一个新的顶点**  
> 添加到顶点列表，并在字典中新增一项。  
```
addVertex(v) {
    if (!this.vertices.includes(v)) {
        this.vertices.push(v);
        this.adjList.set(v, []);
    }
}
```
**添加顶点之间的边**  
> 若图中无相应点，将自动创建。
```
addEdge(v,w) {
    if (!this.adjList.get(v)) {
        this.addVertex(v);
    }
    if (!this.adjList.get(w)) {
        this.addVertex(w);
    }
    this.adjList.get(v).push(w);
    if (!this.isDirected) {
        this.adjList.get(w).push(v);
    }
}
```
**返回顶点列表**  
```
getVertices() {
    return this.vertices;
}
```  
**返回邻接表**  
```
getAdjList() {
    return this.adjList;
}
```  
**创建 toString 方法**  
> 迭代顶点列表，并在每一个元素处迭代相应邻接表。  
```
toString() {
    let s = '';
    for (let i = 0; i < this.vertices.length; i++) {
        s += `${this.vertices[i]} -> `;
        const neighbors = this.adjList.get(this.vertices[i]);
        for (let j = 0; j < neighbors.length; j++) {
            s += `${neighbors[j]} `;
        }
        s += '\n';
    }
    return s;
}
```
> **关于换行**
> - `n` 适用于控制台  
> - `<br/>` 适用于 do...write();  

## 图的遍历  
> 有两种方法可以对图进行遍历：广度优先搜索和深度优先搜索。  

**算法**|**数据结构**|**描述**
:-:|:-:|:-:
广度优先搜索|队列|将顶点存入队列，最先入队列的顶点先被探索
深度优先搜索|栈|将顶点存入栈，顶点是沿着路径被探索的，存在新的相邻顶点就去访问  

**标记顶点**  
> 有助于在广度优先和深度优先算法中标记顶点。  
```
const Colors = {  // 枚举器
    WHITE: 0,  // 未访问
    GREY: 1,   // 访问了，但未探索
    BLACK: 2   // 访问且探索
};  
```  
**初始化顶点标记**  
> 将所有顶点标记为未访问（白色）。  
```
const initializeColor = vertices => {
    const color = {};
    for (let i = 0; i < vertices.length; i++) {
        color[vertices[i]] = Colors.WHITE;
    }
    return color;
};
```

## 广度优先探索  
> 先宽后深地访问顶点，就像一次访问图的一层。  

**算法思路**  
- 创建队列，将起始顶点 v 入列。
- 将顶点 u 出列，取邻点存入变量，顶点 u 变灰。
- 将 *白色邻点* 变灰入列，顶点 u 变黑，(如果队列不为空)重复 ② ③。
  
**算法实现**  
```
const breadthFirstSearch = (graph, startVertex, callback) => {
    const vertices = graph.getVertices();
    const adjList = graph.getAdjList();
    const color = initializeColor(vertices);
    const queue = new Queue();
    queue.enqueue(startVertex);
    
    while (!queue.isEmpty()) {
        const u = queue.dequeue();  // 每次的出列项
        const neighbors = adjList.get(u);
        color[u] = Colors.GREY;
        for (let i = 0; i < neighbors.length; i++) {
            const w = neighbors[i];
            if (color[w] === Colors.WHITE) {
                color[w] = Colors.GREY;
                queue.enqueue(w);
            }
        }
        color[u] = Colors.BLACK;
        
        if (callback) {
            callback(u);
        }
    }
};
```  

> 回调函数参考
> （其中 z 是顶点列表；结果将会输出被访问顶点的顺序）
> ```
> const mF = (value) => console.log('探索完成：' + value);
> breadthFirstSearch(x, z[0], mF);
> ```

### 用 BFS 寻找最短路径。
> 给出 **源顶点** 和 **每个顶点** 之间最短路径的距离（ 以边的数量计 ）。  

**改进的广度优先方法**  
> 在算法实现的基础上，加上了两个对象，用于记录每个点与源顶点的距离，以及每个点的前溯点。  
```
const BFS = (graph, startVertex) => {
    const vertices = graph.getVertices();
    const adjList = graph.getAdjList();
    const color = initializeColor(vertices);
    const queue = new Queue();
    const distances = {};
    const predecessors = {};
    queue.enqueue(startVertex);
    
    for (let i = 0; i < vertices.length; i++) {  // 初始化
        distances[vertices[i]] = 0;
        predecessors[vertices[i]] = null;
    }
    
    while (!queue.isEmpty()) {
        const u = queue.dequeue();
        const neighbors = adjList.get(u);
        color[u] = Colors.GREY;
        for (let i = 0; i < neighbors.length; i++) {
            const w = neighbors[i];
            if (color[w] === Colors.WHITE) {
                color[w] = Colors.GREY;
                distances[w] = distances[u] + 1;
                predecessors[w] = u;
                queue.enqueue(w);
            }
        }
        color[u] = Colors.BLACK;
    }
    return {
        distances,
        predecessors
    };
};
```  
**构建原溯点到其它顶点的路径**  
> 通过建立栈的方式，使最后存入的源起点最先出栈。  
```
const startVertex = z[0];

for (i = 1; i < z.length; i++) {
    const toVertex = z[i];
    const path = new Stack();
    for (
      let v = toVertex;  // 被遍历的其中一个顶点
      v !== startVertex;
      v = BFS(x, z[0]).predecessors[v]  // 赋值为自身前溯点
      ) { 
        path.push(v);
    }
    path.push(startVertex);
    let s = path.pop();
    while (!path.isEmpty()) {
        s += ' - ' + path.pop();
    }
    console.log(s);
}
```

