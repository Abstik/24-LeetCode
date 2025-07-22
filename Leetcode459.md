```
//方法一：KMP算法(主要用途就是字符串的匹配)
func repeatedSubstringPattern(s string) bool {
    n :=len(s)
    if n==0{
        return false
    }
    next:=make([]int,n)
    j:=-1
    next[0]=j
    for i:=1;i<n;i++{
        for j>=0 && s[i]!=s[j+1]{
            j=next[j]
        }
        if s[i]==s[j+1]{
            j++
        }
        next[i]=j
    }
     if next[n-1]!=-1 && n%(n-(next[n-1]+1))==0{  //在这里+1是因为在next数组每个下标都-1了
        return true
    }
    return false
    }
    //构成字符串的最短子字符串：最长前后缀不包括的字符串，且能被字符串长度整除
    //在讨论充分必要性时，分三种情况分析：
    1.当不包括的字符串长度大于文本字符串的一般长度时，肯定不是构成子字符串
    2.当前缀字符串和后缀字符串无重叠时，最长前后缀不包括的字符串能被字符串长度整除，为最短子字符串
    3.当两者有重叠时，看情况，画图先找出两者在最长前后缀相对应的下标，再找出再文本子字符串中对应的相等的下标
    
   最长前后缀长度(假设在next数组中每个下标-1)：
    next[len-1]+1
   如果next[len-1]!=-1，则说明字符串有最长相同的前后缀
   next数组长度:len
   如果len%(len-(next[len-1]+1))==0，则说明该字符串有重复的子字符串
```

[leetcode459.重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern/)

------

```
//方法二：移动匹配
func repeatedSubstringPattern(s string) bool {
    if len(s) == 0 {
        return false
    }
    t := s + s
    return strings.Contains(t[1:len(t)-1], s)
}
//思想：其头去尾看s+s，这个新构建的字符串中如果部分字符串包含了子字符串，则说明该字符串是由重复的子字符串构成的
```

<img src="C:\Users\yyn\AppData\Roaming\Typora\typora-user-images\image-20250722102153308.png" alt="image-20250722102153308" style="zoom: 67%;" />