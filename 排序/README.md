## 排序

排序算是数据结构里最基本的算法了吧~~最近针对性的复习了下，做了下总结~

### 时间复杂度O(n²) -- 选择排序、冒泡排序、插入排序

### 选择排序

选择排序原理很简单，就是循环遍历未排序的部分，然后选出最小（大）的一项放在已排序部分的末端。

![image](https://github.com/yukiyuki1900/Data-Structures-and-Algorithms/blob/master/%E6%8E%92%E5%BA%8F/selectionSort.gif)

```
    //选择排序
    var arr = [2, 1, 4, 6, 3, 5];

    for(var i = 0 , len = arr.length ; i < len ; i ++) {
        var index = i
        for(var j = i+1 ; j < len ; j ++) {
            if(arr[i] > arr[j]) {
                index = j;
            }
        }
        var tmp = arr[i];
        arr[i] = arr[index];
        arr[index] = tmp;
    }
```

空间复杂度是O(1)


### 冒泡排序

冒泡排序的步骤是：

    1. 遍历每一个左右相邻的元素，如果第一个比第二个大（小），就交换它们的位置，这样最后一个一定是最大（小）值
    2. 对剩下部分（除最后一个元素）重复第一个步骤，直到没有可以对比的元素为止

![image](https://github.com/yukiyuki1900/Data-Structures-and-Algorithms/blob/master/%E6%8E%92%E5%BA%8F/bubbleSort.gif)

```
    //冒泡排序
    var arr = [4, 2, 1, 6, 5, 3];

    for(var i = 0 , len = arr.length ; i < len-1 ; i ++) {
        var flag = false;
        for(var j = 0 ; j < len-i-1 ; j ++) {
            if(arr[j] > arr[j+1]) {
                var flag = true;
                var tmp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = tmp;
            }
        }

        if(!flag) {
            break;
        }
        
    }
```

空间复杂度是O(1)


### 插入排序

算法步骤是：把第一项元素看做是有序列，把第二项到最后一个元素看成是无序的列，然后遍历无序列，将元素插入到有序列的合适的位置中。

![image](https://github.com/yukiyuki1900/Data-Structures-and-Algorithms/blob/master/%E6%8E%92%E5%BA%8F/insertionSort.gif)

```
    //插入排序
    var arr = [4, 2, 1, 6, 5, 3];

    for(var i = 1 , len = arr.length ; i < len ; i ++) {
        var index = i - 1;
        var tmp = arr[i];

        while(index >= 0 && arr[index] > tmp) {
            arr[index+1] = arr[index];
            index --;
        }

        arr[index+1] = tmp;
    }
```

空间复杂度是O(1)

**选择排序**、**冒泡排序**和**插入排序** 时间复杂度都是O(n²)，但是在最优状态下时间复杂度是O(n)。


### 时间复杂度O(nlogn) -- 快速排序、归并排序、希尔排序、堆排序

### 快速排序

快排是一个很经典，在实际运用中也很常用的一个排序算法，它的原理是使用分而治之和递归的方法对元素进行排序

算法步骤是：

    1. 先选出一个基准值，然后将所有的元素与这个基准值做比较，小于基准值的放在左边，大于基准值的放在右边
    2. 分别对左边和右边两列执行步骤1和步骤2的操作

```
    //快速排序
    function quickSort(arr, low, high) {
        low = low || 0;
        high = high || arr.length-1;

        if(low >= high) {
            return;
        }

        var loc = part(arr, low, high);
        quickSort(arr, low, loc-1);
        quickSort(arr, loc+1, high);
    }

    function part(arr, low, high) { // 根据基准值将未排序的数组分两个区
        var pivot = arr[low];  //将第一个值设为基准值

        while(low < high) {
            while(arr[high] > pivot && low < high) {  //找到比pivot小的值，放到左边
                high --;
            }
            arr[low] = arr[high];

            while(arr[low] <= pivot && low < high) {  //找到比pivot大的值，放在右边
                low ++;
            }
            arr[high] = arr[low];

        }
        arr[low] = pivot;   //这样pivot左边都是小于或等于pivot的值，右边都是大于pivot的值

        return low;
    }

    var arr = [4, 2, 1, 6, 5, 3];
    quickSort(arr);
```

除此之外，我看还看到有通过js自带的函数来实现的，不过需要浪费额外的空间

```
    //快速排序2
    function quickSort2(arr) {
        if(arr.length <= 1 ) {
            return arr;
        }
        var pivot = arr[0];
        var left = [];
        var right = [];

        for(var i = 1 , len = arr.length ; i < len ; i ++) {
            if(arr[i] <= pivot) {
                left.push(arr[i]);
            }else if(arr[i] > pivot) {
                right.push(arr[i])
            }
        }

        return quickSort2(left).concat(pivot, quickSort2(right));
    }

    var arr = [4, 2, 1, 6, 5, 3];
    var arr2 = quickSort2(arr);
```

如果数据量比较大的话，第二种方法所消耗的内存也会比较大。


### 归并排序


