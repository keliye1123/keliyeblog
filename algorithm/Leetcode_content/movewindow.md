# Leetcode 题解
  
  ## 1.处理连续子数组和连续子字符串  
    
3.无重复字符的最长子串  

[力扣](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)  
下面是以移动窗口思想和哈希表所设计的代码  
  
  ```C  
  int lengthOfLongestSubstring(char* s) {
    int dict[128]={0};
    int head = 0,tail = 0,max = 0,temp = 0;

    for (;s[tail];tail++){

        temp = dict[s[tail]];//与if配合判断是否重复出现字符//
        dict[s[tail]] = tail + 1;

        if (temp != 0 && temp > head){
            head = temp ;
        }

        max = max > (tail - head + 1) ? max : (tail - head + 1);
    }

    return max;
}  
```  
1

