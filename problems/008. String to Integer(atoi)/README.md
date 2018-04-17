#  8. String to Integer (atoi)

## #1 遍历字符串[AC]

### 思路

本身题目不算难，就是遍历字符串中的每个字符，可以用charAt和计数器一起使用实现遍历字符串。关于正负号，可以先默认为正号，然后通过读取第一个字符是否为'+','-'来改变正负号，这里正负号可以用1或者-1来实现正负号，然后就是读取一个数字，然后乘以10，这样做了。还有，就是要考虑是否越界的问题，我在这里是遍历的过程中就判断，因为我之前试过了，在遍历完再判断，会出现input = 9223372036854775809; 也就是long的最大值也越了。

### 算法

```java
public class Solution {
    public int myAtoi(String str) {
        if(str == null){
            return 0;
        }
        str = str.trim();
        if(str.length() == 0){
            return 0;
        }

        int opt = 1; 
        int start = 1;
        long ans = 0l;
        
        opt = str.charAt(0);
        if(opt == '+'){
            opt = 1;
        }else if(opt == '-'){
            opt = -1;
        }else{
            opt = 1;
            start--;
        }
        int maxint = 0x7fffffff;
        int minint = 0x80000000;
        
        for(int i=start; i<str.length(); i++){
            if(!(str.charAt(start) >= '0' && str.charAt(start) <='9'))
                return 0;
            char tmp = str.charAt(i);
            if(tmp >= '0' && tmp <= '9'){
                ans = ans*10 + (tmp - '0');
                if(ans > maxint){
                    if(opt == -1)
                        return minint;
                    return maxint;
                 }
                 if(ans < minint){
                     if(opt == -1)
                        return maxint;
                    return minint;
                }
            }else{
                break;
            }
        }
        return (int)(opt * ans);
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$