# 算法设计与技巧  

## 二分搜索————分而治之
```
function binarySearch(array, value, compareFn = defaultCompare) {
    const sortedArray = quickSort(array);    // 先排序
    const low = 0;
    const high = sortedArray.length - 1;
    
    return binarySearchRecursive(array, value, low, high, compareFn);
}

function binarySearchRecursive(array, value, low, high, compareFn = defaultCompare) {
    if (low <= high) {  // 基线条件
        const mid = Math.floor((low + high) / 2);
        const element = array[mid];
        
        if(compareFn(element, value) == 1) {
            return binarySearchRecursive(array, value, mid + 1, high, compareFn);
        } else if (compareFn(element, value) == 2) {
            return binarySearchRecursive(array, value, low, mid - 1, compareFn);
        } else {
            return mid;
        }
    }
    return false;
}
```

## 最少硬币找零问题————动态规划  
> 总额 = 第一张纸币（用 for 遍历所有种类） + 剩余总额  
> 
> 需将面额数组以正序排列，最后一个输出结果即所求解。  
> tip: 将 ④ 删去，并将面额数组以倒序排列，可得所有找零结果。  
```
function minCoinChange(coins, amount) {  // 面额数组，找零的总额
    const cache = [];
    const makeChange = (value) => {  // 函数声明
        if (!value) {
            return [];
        }
        if (cache[value]) {    
            return cache[value];
        }
        let min = [];
        let newMin;
        let newAmount;
        for (let i = 0; i < coins.length; i++) {
            const coin = coins[i];
            newAmount = value - coin;
            if (newAmount >= 0) {
                newMin = makeChange(newAmount);
            }
            if (
              newAmount >= 0 &&
              (newMin.length + 1 < min.length || !min.length) &&  // ④
              (newMin.length || !newAmount)
            ) {
                min = [coin].concat(newMin);
                console.log('new Min' + min + ' for ' + value);
            }
        }
        return (cache[value] = min);
    };
    return makeChange(amount);  // 执行函数
}
```  
> ① value 为本轮需要凑到的总额；  
> ② netAmount 则是为了达成 ① 所需凑到的总额（新目标）；  
> ③ coin 为本次( for )使用的零钱。 

## 背包问题————动态规划    
> 给定一个能携带重量 W 的背包，以及一组有价值和重量的物品，找出一个最佳解决方案，使得装入背包的物品总重量不超过 W 的同时总价值最大。  
> 
> 动态规划只能解决 0-1 版本，即每种物品只有一个。  
```
function knapSack(capacity, weights, value, n) {
    const kS = [];
    for (let i = 0; i <= n; i++) {
        kS[i] = [];
    }
    
    for (let i = 0; i <= n; i++) {
        for (let w = 0; w <= capacity; w++) {
            if (i === 0 || w === 0) {
                kS[i][w] = 0;
            } else if (weights[i - 1] <= w) {
                const a = values[i -1] + kS[i -1][w - weights[i -1 ]];
                const b = kS[i - 1][w];
                kS[i][w] = a > b ? a : b;
            } else {
                kS[i][w] = kS[i - 1][w];
            }
        }
    }
    findValues(n, capacity, kS, weights, values);
    console.log(`总价值:  ${kS[n][capacity]}`);
}

// 列出实际物品
function findValues(n, capacity, kS, weights, values) {
    let i = n;
    let k = capacity;
    console.log('构成解的物品： ');
    while (i > 0 && k > 0) {
        if (kS[i][k] !== kS[i - 1][k]) {  // 判断物品 i 有没有加入方案
            console.log(`物品 ${i} 可以是解的一部分 w,v: ${weights[i - 1]}, ${values[i - 1]}`);
            i--;
            k -= weights[i - 1];  // 剩余重量
        } else {
            i--;
        }
    }
}
```
**举个栗子**  
> 对应重量和价值的参数要以数组形式传入。
```
const values = [3,4,5],
      weights = [2,3,4],
      capacity = 5,
      n = values.length;
knapSack(capacity, weights, values, n);
```

## 最少硬币找零问题————贪心算法  
> 贪心算法期盼通过每个阶段的局部最优选择，从而达到全局的最优。  
> 
> 从最大面额的硬币开始
```
function minCoinChange(coins, amount) {
    const change = [];
    let total = 0;
    for (let i = coins.length - 1; i >= 0; i--) {
        const coin = coins[i];
        while (total + coin <= amount) {
            document.write(coin); //
            change.push(coin);
            total += coin;
        }
    }
    return change;
}
```


