# 算法设计与技巧  

## 分而治之————二分搜索
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
