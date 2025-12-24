# LC 454 四数相加II

## 1. Basic Information

- __question__: 四数相加II
- __topic__: hash
- __level__: medium
- __time-cost__: null
- __completed-date__: 12-23-2025
- __completed-times__: 1
- __status__: 阅读思路和代码后模仿完成

## 2. Question

给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：
0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
 
示例 1：
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
示例 2：
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1

提示：
n == nums1.length
n == nums2.length
n == nums3.length
n == nums4.length
1 <= n <= 200
-228 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 228

## 3. Solution

将四数组视为A+B,C+D的两个“数组”，注意题目只需要计算次数。因此先遍历计算A+B的和与出现次数映射到HashMap。然后遍历C+D作为匹配值寻找总和为0的累计次数。

## 4. Code Implementation

    class Solution {
        public int fourSumCount(int[] numsA, int[] numsB, int[] numsC, int[] numsD) {
            int result = 0;
            Map<Integer, Integer> semi = new HashMap();
            for(int i : numsA){
                for(int j : numsB){
                    int sum = i + j;
                    semi.put(sum, semi.getOrDefault(sum,0)+1);
                }
            }
    
            for(int i : numsC){
                for(int j : numsD){
                    int sum = i + j;
                    int want = - sum;
                    result += semi.getOrDefault(want, 0);
                }
            }
            return result;
        }
    }
   
## 5. Conclusion
- A+B 的次数是对所有 (a, b) 组合的显式聚合统计，而 C+D 的组合次数通过双重循环被逐一枚举。由于遍历 C+D 的过程已经隐式包含其出现频率，因此在每次匹配时只需累加 A+B 的聚合次数即可完成四元组计数。
- HashMap中获取指定key值的value的方法是.get(key)或者.getOrDefault(key, default)，处理没有找到指定key时返回的默认值。
- 题目中并没有保证有解，因此需要考虑key没有找到的情况，需要使用.getOrDefault()方法。
- HashMap中检查是否存在指定key的方法是.containsKey(key)。
