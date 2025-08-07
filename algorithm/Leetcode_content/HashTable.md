# Leetcode 题解 - 哈希表  
哈希表使用 O(N) 空间复杂度存储数据，并且以 O(1) 时间复杂度求解问题。  
  
    
## 1. 数组中两个数的和为给定值

1. Two Sum (Easy)

 [力扣](https://leetcode-cn.com/problems/two-sum/description/)  
    下面是我以哈希表的思想用固定大小的数组模拟哈希表所设计的代码。  
    优点：访问速度快、实现成本低、内存可控  
    缺点：输入的数值范围受限、内存可能会浪费、扩展性为零

```C  
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    int* result = (int*)malloc(2 * sizeof(int)); //分配内存存储结果数组
    int* dict = (int*)malloc(2000 * sizeof(int));//分配内存将dict数组作为哈希表

    // 初始化 dict 数组，避免脏数据影响判断
    for (int i = 0; i < 2000; i++) 
    {
        dict[i] = 0;
    }
      
    //遍历输入数组nums
    for (int i = 0; i < numsSize; i++) 
    {
        int complement = target - nums[i];//计算当前元素与目标值的补数
        if (dict[1000 + complement] != 0)//检查补数是否已在哈希表存在
        {
            result[1] = i;//如果存在，将当前索引存入结果数组
            result[0] = dict[1000 + complement] - 1;//将哈希表中存储的索引-1后存入结果数组
            *returnSize = 2;
            return result;
        } 
        else 
        {
            dict[1000 + nums[i]] = i + 1;//如果补数不存在哈希表中，将当前补数和其索引+1存入哈希表
        }
    }
    *returnSize = 0;
    return result;
}  
```
    
疑问1：为什么returnSize要用指针类型而不用整形？  
解答：在C语言中，如果一个整形变量作为参数传入函数中，函数无法修改这个值，所以通过指针修改returnSize所指的值来影响函数外部变量。
  
疑问2：为什么将索引存储在哈希表时要先加一然后存入结果数组后再减一？  
解答：避免索引为零时与哈希表的初始值为零混淆的问题。  
  
  总结：该代码用dict数组的下表存储补数的值，在查找时可以根据下标值直接判断是否存在所需数值，同时用dict数组元素存储索引值，这使数值与索引形成映射关系，让查找更方便。

    
    
    



 
 