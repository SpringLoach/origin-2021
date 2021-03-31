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


