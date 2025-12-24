# LC 1 两数之和

## 1. Basic Information

- __question__: 两数之和
- __topic__: hash
- __level__:  easy
- __time-cost__: null
- __completed-date__: 12-25-2025
- __completed-times__: 1
- __status__: 尝试失败，查看思路和题解后完成

## 2. Question

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。
你可以按任意顺序返回答案。

示例 1：
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
示例 2：
输入：nums = [3,2,4], target = 6
输出：[1,2]
示例 3：
输入：nums = [3,3], target = 6
输出：[0,1]

提示：
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
只会存在一个有效答案

## 3. Solution

构造一个HashMap作为历史记录，同时跟踪元素和下标（因为题目要求返回下标而非元素本身），遍历原数组，寻找当前元素与目标数的差值，因为只存在一个解因此可以直接遍历。

## 4. Code Implementation
我的答案（错误）：

    class Solution {
        public int[] findTarget(int target,  int[] nums) {
            Map<int, int> record = new HashMap();
            int index = 0;
            for(int i : nums){
                record.put(index, i);
                i++;
            }
            
            for(int i : nums){
                int want = target - i;
                // 止步于此，意识到思路错误，查找HashMap里的value时间复杂度为O(n)，同时存在其他问题
            }
        }    
    }

- 分歧问题详见conclusion

标准答案：

    public int[] twoSum(int[] nums, int target) {
      int[] res = new int[2];
      if(nums == null || nums.length == 0){
          return res;
      }
      Map<Integer, Integer> map = new HashMap<>();
      for(int i = 0; i < nums.length; i++){
          int temp = target - nums[i];   // 遍历当前元素，并在map中寻找是否有匹配的key
          if(map.containsKey(temp)){
              res[1] = i;
              res[0] = map.get(temp);
              break;
          }
          map.put(nums[i], i);    // 如果没找到匹配对，就把访问过的元素和下标加入到map中
      }
      return res;
  }

## 5. Conclusion
- 在本题中，我最初意识到可以用 HashMap 将时间复杂度从 O(n²) 优化到 O(n)，方向是正确的，但一开始错误地将 map 设计为 key=下标，value=元素，导致需要按 value 查找，无法发挥 HashMap O(1) 查找的优势，并引入了区分“重复元素”和“重复使用同一元素”等额外复杂逻辑。
进一步分析后我意识到，题目要求返回的是下标，因此正确的设计应为 key=元素值，value=下标，并在遍历数组的过程中动态记录已访问的元素。这样可以直接通过 containsKey(target - nums[i]) 在 O(1) 时间内查找补数，同时自然地处理重复元素（如 2 + 2 = 4）。此外，HashSet 不适用于本题，因为它无法提供元素对应的下标信息。
