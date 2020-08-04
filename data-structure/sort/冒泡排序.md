# 冒泡排序

### 1. 基本思想

冒泡排序是一种交换排序。通过两两比较相邻记录的关键字，如果反序则交换，直到没有反序的记录为止。

### 2.举例分析

冒泡排序的处理过程为：对序列的相邻两个关键字 array[j] 和 array[j+1]，若逆序（array[j] > array[j+1]），则交换，使得关键字值小的记录左移，关键字值大的记录右移。第一趟冒泡排序会找出序列中关键字值最大的记录，第二趟排序会找出关键字值第二大的记录，… … 则对于有 n 个记录的序列，最多经过 n-1 趟冒泡排序，就可使该序列有序。

以序列 12, 23, 33, 8, 99, 0 为例。有 6 个记录，最多需要 5 趟排序。
- 第一趟排序后：12, 23, 8, 33, 0, 99
- 第二趟排序后：12, 8, 23, 0, 33, 99
- 第三趟排序后：8, 12, 0, 23, 33, 99
- 第四趟排序后：8, 0, 12, 23, 33, 99
- 第五趟排序后：0, 8, 12, 23, 33, 99

### 3.代码实现

**基础冒泡排序：**

```java
public static void bubbleSort(int[] array){
	for (int i = 0; i < array.length - 1; i++) {
		for (int j = 0; j < array.length - i - 1; j++) {
			if(array[j] > array[j + 1]){// 大的往后放——>升序
				int t = array[j];
				array[j] = array[j + 1];
				array[j + 1] = t;
			}
		}
	}
}
```

**优化：**

定义一个标识变量 flag 来判断一次循环中有没有交换位置，如果在一次循环中没有交换位置，说明此时序列已经有序，排序已经完成，直接跳出循环即可。 这样可以避免内部循环多次判断，提高效率。代码如下：
```java
public static void improvedBubbleSort(int[] array){
	for (int i = 0; i < array.length - 1; i++) {
		// 设定一个标记，若为true，则表示此次循环没有进行交换，
		// 也就是待排序列已经有序，排序已经完成。
		boolean flag = true;
		for (int j = 0; j < array.length - i - 1; j++) {
			if(array[j] > array[j + 1]){// 大的往后移——>升序
				// 用异或运算实现两个数的交换
				array[j] = array[j] ^ array[j + 1];
				array[j + 1] = array[j] ^ array[j + 1];
				array[j] = array[j] ^ array[j + 1];
				flag = false;
			}
		}
		// 没有交换,说明现在已经是有序的，直接跳出循环
		if(flag)
			break;
	}
}

```
