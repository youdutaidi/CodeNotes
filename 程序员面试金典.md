# leetcode 程序员面试金典100题

> 2024.10.2

### 0101判定字符是否唯一

难度级别：简单

实现一个算法，确定一个字符串 `s` 的所有字符是否全都不同。

**示例 1：**

```
输入: s = "leetcode"
输出: false 
```

**示例 2：**

```
输入: s = "abc"
输出: true
```

**限制：**

- `0 <= len(s) <= 100 `
- `s[i]`仅包含小写字母
- 如果你不使用额外的数据结构，会很加分。





#### solution1：使用Python3字符串的内置函数string.count(str,beg,end)

```python
class Solution:
    def isUnique(self, astr: str) -> bool:
        for i in range(0,len(astr)):
            c=astr.count(astr[i],i,len(astr))
            # print(c)
            if c>=2:
                return False

        return True
```



#### solution2: 使用C语言的数组

```c
bool isUnique(char* astr){
    int string[128]={0};
    for(int i=0;i<=strlen(astr);i++)
    {
        string[astr[i]]++;
        if (string[astr[i]]>=2){return false;}
    }
    return true;
}
```

#### 相关知识点：散列表（Hash Table)

散列表，也称哈希表或Hash Table，依赖于数组按照下标随机访问元素的时间复杂度为O(1)的特性。是对数组的一种扩展。



## 0103 URL化

URL化。编写一种方法，将字符串中的空格全部替换为`%20`。假定该字符串尾部有足够的空间存放新增字符，并且知道字符串的“真实”长度。（注：用`Java`实现的话，请使用字符数组实现，以便直接在数组上操作。）

 

**示例 1：**

```
输入："Mr John Smith    ", 13
输出："Mr%20John%20Smith"
```

**示例 2：**

```
输入："               ", 5
输出："%20%20%20%20%20"
```

 

**提示：**

- 字符串长度在 [0, 500000] 范围内。



> 注意审题，length是真实长度，小于计算字符串尾部空格的长度。

解题：

```C
char* replaceSpaces(char* S, int length){
    int rear = strlen(S);
    printf("%d,%d ",rear,length);
    for (int i = length - 1; i >= 0; i--) {
        if (S[i] == ' ') {
            S[--rear] = 0 + '0';
            S[--rear] = 2 + '0';
            S[--rear] = '%';
            printf("%d,%d ",rear,i);
        }
        else {
            S[--rear] = S[i];
        }
    } 
    return S + rear;
}
```

考察的是指针的知识，S+rear是返回指针所指的位置。

Rear的是大于length的

