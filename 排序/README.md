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

归并排序应该比较好理解，就是遍历两个已排序的序列，选择比较小的一项放入新的序列中，最终得到一个已排序的序列。

也是使用分而治之的方法，对序列进行自上而下的递归，主要步骤如下：

    1. 申请一个空数组，来存放排序后的两个序列
    2. 将两个指针放在两个已排序的序列前端，同时遍历两个序列，遇到较小的元素则将此元素push进步骤1的数组里，直到遍历到序列最后一个元素
    3. 重复步骤1和步骤2，直到最小已排序序列长度为1

![image](https://github.com/yukiyuki1900/Data-Structures-and-Algorithms/blob/master/%E6%8E%92%E5%BA%8F/mergeSort.gif)

```
    //归并排序
    function mergeSort(arr) {
        var len = arr.length;

        if(len <= 1) {
            return arr;
        }

        var mid = parseInt(len/2);
        var larr = arr.slice(0, mid);
        var rarr = arr.slice(mid);

        return merge(mergeSort(larr), mergeSort(rarr));
    }

    function merge(left, right) {
        var result = [];
        var i = 0;
        var j = 0;
        var llen = left.length;
        var rlen = right.length;

        while(i < llen && j < rlen) {
            if(left[i] < right[j]) {
                result.push(left[i]);
                i ++;
            }else {
                result.push(right[j]);
                j ++;
            }
        }

        while(i < llen) {
            result.push(left[i]);
            i ++;
        }

        while(j < rlen) {
            result.push(right[j]);
            j ++;
        }

        return result;
    }

    var arr = [4, 2, 1, 6, 5, 3];
    var arr2 = mergeSort(arr);
```

因为需要申请新的空间，所以归并排序的空间复杂度是O(n);


### 希尔排序

希尔排序其实就是对插入排序的一个优化，插入排序效率比较低，每次数据只能挪动一个位置。希尔排序则是先将序列分为几个区域，元素在区域间排序，使得每次元素能挪动一大步，从而增加排序的效率。

比如有一个数组[10, 2, 9, 6, 5, 3, 7, 8, 1, 11, 4]

首先以步长为5进行排序，此时更直观的看到数组应该是这样的：

```
    10 2 9 6 5
    3  7 8 1 11
    4
```

因为第一次排序步长是5，所以排序是对上面数组纵列进行排序，排完序后数组为：

```
    3  2 8 1 5
    4  7 9 6 11
    10
```

第二次采取步长为3进行排序，更直观的看到数组应该是这样：

```
    3  2 8
    1  5 4
    7  9 6
    11 10
```

排序完后数组为：

```
    1  2  4
    3  5  6
    7  9  8
    11 10
```

把数组还原是：[1, 2, 4, 3, 5, 6, 7, 9, 8, 11, 10]

通过两次遍历，每个元素距离有序的位置已经很靠近了。这个时候，再通过简单的插叙排序，所有元素便成为有序。

如何去选择步长是希尔排序的一个重要的部分，常见的步长选择为n/2

```
    //希尔排序
    function shellSort(arr) {
        var len = arr.length;

        if(len <= 1) {
            return;
        }

        var gap = parseInt(len/2);

        while(gap > 0) {
            for(var i = gap ; i < len ; i ++) {
                var tmp = arr[i];
                for(j = i - gap ; j >= 0 && arr[j] > tmp ; j -= gap) {
                    arr[j+gap] = arr[j];
                }
                arr[j+gap] = tmp;
            }

            gap = parseInt(gap/2);
        }

        return arr;
    }

    var arr = [10, 2, 9, 6, 5, 3, 7, 8, 1, 11, 4];
    shellSort(arr);
```


### 堆排序

堆是类似完全二叉树的一个数据结构，在起始下标为0的数组中：

* 父节点i的左节点的下标是 **2*i+1**
* 父节点i的右节点的下标是 **2*i+2**
* 子节点为i的父节点下标是 **floor((i-1)/2)**

主要算法步骤如下：

    1. 对数组做第一遍遍历，使所有父节点都大于等于子节点
    2. 此时，第一位元素一定是数值最大的节点
    3. 将第一位元素与未排序的最后一个序列的最后一位交换
    4. 对左边未排序序列循环1，2，3步骤，最终得到已排序的升序序列

![image](https://github.com/yukiyuki1900/Data-Structures-and-Algorithms/blob/master/%E6%8E%92%E5%BA%8F/heapSort.gif)

```
```

### 参考材料

* [希尔排序](https://zh.wikipedia.org/wiki/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)
* [堆排序](https://zh.wikipedia.org/wiki/%E5%A0%86%E6%8E%92%E5%BA%8F)
* [十大经典排序算法](https://sort.hust.cc/)
