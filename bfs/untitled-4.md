# 127. Word Ladder

Given two words \(_beginWord_ and _endWord_\), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

**Example 1:**

```text
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```text
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.

```

1.用什么算法: BFS 

2.为什么用这个算法：这道题相当于是简单图，每个边长度相等，求从起点到终点最短路径

3.代码实现要注意的地方：这个和层级遍历类似，所以在第一个循环内要考虑每层的遍历，即要多写个循环，

```text
for (int j = queue.size(); j > 0; j--) {
```

这里j&gt;0而不是j&gt;=0。

4.代码实现可以优化的地方：用Bidirectional BFS， 定义两个queue。

5.时间复杂度：O\(m\*n\), m:word.length\(\), n:wordList长度

6.空间复杂度: O\(n\)

7.相关题目: word Ladder II

```text
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> set = new HashSet<>();
        for (String word : wordList) {
            set.add(word);
        }
        if (!set.contains(endWord)) {
            return 0;
        }
        int count = 0;
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int l = beginWord.length();
        
        while (!queue.isEmpty()) {
            count++;
            for (int j = queue.size(); j > 0; j--) {
                String cur = queue.poll();
                char[] arr = cur.toCharArray();
                for (int i = 0; i < l; i++) {
                    char ch = arr[i];
                    for (char c = 'a'; c < 'z'; c++) {
                        if (c == ch) {
                            continue;
                        }
                        arr[i] = c;
                        String newString = new String(arr);
                        if (newString.equals(endWord)) {
                            return count + 1;
                        } 
                        if (!set.contains(newString)) {
                            continue;
                        }
                        set.remove(newString);
                        queue.add(newString);
                    }
                    arr[i] = ch;
                 }
            } 
        }
        return 0;
    }
}
```

```text
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashSet<String> dict = new HashSet<>();
        for (String str : wordList) {
            dict.add(str);
        }
        
        if (!dict.contains(endWord)) 
            return 0;
        
        HashSet<String> q1 = new HashSet<>();
        HashSet<String> q2 = new HashSet<>();
        
        q1.add(beginWord);
        q2.add(endWord);
        
        int l = beginWord.length();
        int steps = 0;
        
        while (!q1.isEmpty() && !q2.isEmpty()) {
            steps++;
            
            if (q1.size() > q2.size()) {
                HashSet<String> temp = q1;
                q1 = q2;
                q2 = temp;
            }
            
            HashSet<String> q = new HashSet<>();
            for (String w : q1) {
                char[] chs = w.toCharArray();
                for (int i = 0; i < l; i++) {
                    char ch = chs[i];
                    for (char c = 'a'; c <= 'z'; ++c) {
                        chs[i] = c;
                        String t = new String(chs);
                        if (q2.contains(t)) return steps + 1;
                        if (!dict.contains(t)) continue;
                        dict.remove(t);
                        q.add(t);
                    }
                    chs[i] = ch;
                }
            }
            q1 = q;
        }
        return 0;
    }
}
```

