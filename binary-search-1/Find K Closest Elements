# 658. Find K Closest Elements

Given a sorted array, two integers `k` and `x`, find the `k` closest elements to `x` in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

**Example 1:**  


```text
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

**Example 2:**  


```text
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

**Note:**

1. The value k is positive and will always be smaller than the length of the sorted array.
2. Length of the given array is positive and will not exceed 104
3. Absolute value of elements in the array and x will not exceed 104

这里输出要按顺序，所以可以记录arr里的距离x 的位置，再把这个范围里的数按照顺序加入到res里，这样可以保证题目要求的顺序。在binarySearch里返回的是第一个大于target的index。除此之外还要比较x-arr\[start\]和arr\[end\]-x的大小。

```text
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> res = new ArrayList<>();
        if (arr == null || arr.length == 0) {
            return res;
        }
        int index = binarySearch(arr, x);
        int start = index - 1;
        int end = index;
        for (int i = 0; i < k; i++) {
            if (start < 0) {
                end++;
            } else if (end >= arr.length) {
                start--;
            } else {
                if (x - arr[start] <= arr[end] - x) {
                    start--;
                } else {
                    end++;
                }
            }
        }
        for (int i = start + 1; i < end; i++) {
            res.add(arr[i]);
        }
        return res;
    }
    public int binarySearch(int[] arr, int target) {
        int start = 0;
        int end = arr.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (arr[mid] == target) {
                start = mid;
            } else if (arr[mid] > target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (arr[start] >= target) {
            return start;
        }
        if (arr[end] >= target) {
            return end;
        }
        return arr.length;
    }
}
```

