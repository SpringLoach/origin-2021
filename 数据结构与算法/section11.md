# 排序算法  

## 冒泡排序  
> **冒泡排序** 比较所有相邻的两个项，如果第一个比第二个大，则交换它们。  
> 
> 从运行时间的角度来看，冒泡排序是最差的一个。  

```
function bubbleSort(array, compareFn = defaultCompare) {
    const {length} = array;
    for (let i = 0; i < length; i++) {    // 轮数和数组长度一致
        for (let j = 0; j < length -1; j++) {  // 比较 length -1 次
            if (compareFn(array[j],array[j+1]) == 2) {
                swap(array, j , j+1);
            }
        }
    }
    return array;
}
```
需要用到的方法  
```
function defaultCompare(a,b) {
    if (a < b) {
        return '1';
    } else if (a > b) {
        return '2';
    }
}

function swap(array, a, b) {
    const temp = array[a];
    array[a] = array[b];
    array[b] = temp;
}
```

创建一个选定长度的倒序数组
> 跟这个算法没有直接关系，但说不定能用上呢
```
function createNonSortedArray(size) {
    const array = [];
    for (let i = size; i > 0; i--) {
        array.push(i);
    }
    return array;
}
```
**改进后的冒泡排序**  
> 由于第 n 轮将捋清倒数 n+1 个元素的关系。
> 
> 只需要从内循环减去外循环中跑过的次数，就可以避免内循环中所有不必要的比较。
```
function modifiedBubbleSort(array, compareFn = defaultCompare) {
    const {length} = array;
    for (let i = 0; i < length; i++) {
        for (let j = 0; j < length -1 - i; j++) {
            if (compareFn(array[j],array[j+1]) == 2) {
                swap(array, j , j+1);
            }
        }
    }
    return array;
}
```

## 选择排序  
> 选择排序是一种原址比较排序算法。思路是找到最小值放置在第一位，剩下的值里继续找最小值放在第二位，以此类推。  
```
function selectionSort(array, compareFn = defaultCompare) {
    const { length } = array;
    let indexMin;
    for (let i = 0; i < length - 1; i++) {  // 共进行 length - 1 轮，最后的位置不用
        indexMin = i;
        for (let j = i; j < length; j++) {  // 比较 length - i 位数
            if (compareFn(array[indexMin], array[j]) == 2) {
                indexMin = j;
            }
        }
        if (i !== indexMin) {  // 找出最小值后交换到 i 的位置
            swap(array, i, indexMin);
        }
    }
    return array;
};
```
