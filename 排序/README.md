## 排序

排序算是数据结构里最基本的算法了吧~~最近针对性的复习了下，做了下总结~

### 时间复杂度O(n²) -- 选择排序、冒泡排序、插入排序

#### 选择排序

选择排序原理很简单，就是循环遍历未排序的部分，然后选出最小（大）的一项放在已排序部分的末端。

![image]()

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


#### 冒泡排序

冒泡排序的步骤是：

    1. 遍历每一个左右相邻的元素，如果第一个比第二个大（小），就交换它们的位置，这样最后一个一定是最大（小）值
    2. 对剩下部分（除最后一个元素）重复第一个步骤，直到没有可以对比的元素为止

![image]()

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


#### 插入排序

算法步骤是：把第一项元素看做是有序列，把第二项到最后一个元素看成是无序的列，然后遍历无序列，将元素插入到有序列的合适的位置中。

![image]()

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

