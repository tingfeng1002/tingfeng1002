# BM
## 来源于思路
BF和RK的对比思路是使用模式串和子串逐一进行对比，如果子串不匹配进行下一个子串，再从模式串第一个字符开始匹配，<br/>
可以简化的思路是**当模式串和子串的某个字符不匹配时候，直接跳过到该字符后面** 比如模式串中不包含c ,那么可以直接跳过到c 后面

## 坏字符和好后缀
每次遇到坏字符后把坏字符在模式串中的位置记录为xi 如果不存在xi=-1 ,坏字符在模式串中对应的位置的字符串记录为si 移动的位置是 si-xi
<br/> 但是遇到主串与子串特殊的话 为负数 就需要好后缀规则

### 好后缀规则
在坏字符后面已经匹配的字符称好后缀，记做 {u}，我们使用好后缀在模式串中匹配，如果找到了另一个与好后缀匹配的子串{u*},那么我们将模式串滑动到子串与好后缀上下对齐的位置

### 模式串中对应坏字符出现的位置
每次遍历查询不方便 我们可以使用hash 已经其他方式提前记录出现的位置，比如字符都可以使用ascii 码标记，所以可以使用assci 对应的数组存储所有字符出现的位置，最大是256 ，我们只需要记录最大
```java
package test;

class Test {
    
    int [] ASCII = new int[256];
}
```


## 实现
```java
package test;
public class Test {
    
    public int bm (char [] a, int n,char [] b,int m){
        int i =0;
        while (i< n-m){
            int j ;
            for (j<m-1;j<=0;--j){
                if (a[i+j] != b[j]){
                    break;
                }
            }
            if (j<0){
                return i;
            }
            x = calc(b[j],b);
            i= i+ j- x;
            
        }
    }
}
```

