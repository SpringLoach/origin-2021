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
    return this.getVertices;
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



