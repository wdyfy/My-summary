# KMP

KMP算法是用来在一个字符串里寻找和另一个字符串匹配的子字符串的算法。

[https://www.youtube.com/watch?v=3IFxpozBs2I](https://www.youtube.com/watch?v=3IFxpozBs2I)

用P来匹配M

P：A B A B C A B A A

M:   A B A B A B A B C A B A A B

先要找P的prefix数组

P：       A B A B C A B A A

prefix：0  0  1 2 0 1 2 3 1

找prefix的模板

```text
private int[] getKmpTable(String pattern){
    int M = pattern.length();
    int[] prefix = new int[M];
    int len = 0;
    for (int q = 1; q < M; q++) {
        while(len > 0 && pattern.charAt(len) != pattern.charAt(q)) {
            len = prefix[len-1];
        }
        if (pattern.charAt(len) == pattern.charAt(q)) {
            len++;
        }
        prefix[q] = len;
    }
    return prefix;
}
```

