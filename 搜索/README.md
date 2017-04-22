## 搜索

### 二分搜索 -- O(log n)

二分搜索是在一个一个**有序的序列**里，先取序列中间的元素与需要查找的元素进行对比，如果需要查找的元素等于中间元素，则返回；如果小于中间元素，则在小于中间元素的那一半序列中继续选择中间的元素进行对比；如果大于中间元素，则在大于中间元素的那一半序列中继续选择中间元素进行对比；如果直到最后步骤的数组为空，则找不到。

```
    var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

    var binary_search = function (arr, key, start, end) {
        if(start > end) {
            return -1;
        }

        var mid = parseInt((start + end)/2);

        if(arr[mid] === key) {
            return mid;
        }

        if(arr[mid] > key) {
            return binary_search(arr, key, start, mid-1);
        }

        if(arr[mid] < key) {
            return binary_search(arr, key, mid+1, end);
        }
    }

    var result = binary_search(arr, 8, 0, arr.length);

```

因为每次都会把搜索区域折半，所以时间复杂度是O(log n)


### 参考材料
* [二分搜索算法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E7%B4%A2%E7%AE%97%E6%B3%95)