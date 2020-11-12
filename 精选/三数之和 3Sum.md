### 三数之和 3Sum

#### 题目

给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？找出所有满足条件且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

示例：

```javascript
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

#### 解答

思路1：这道题的难点在于如何避免重复的结果数组，`[1,2,-3]`和`[-3,1,2]`算一个结果，这就比较难办了。最初考虑的是3层循环，然后每次碰见正确的结果就存两次，一次以数组的形式存入结果集合，另外一次将数组转为字符串形式，方便过滤重复的答案。但是处理方式太粗暴，最后验证的时候会超过时间限制。

思路2：先将数组排序，然后两层循环，内层分作两个数分别从前向后和从后向前循环。期间需要多种情况的判断。

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
  var result = [];
  nums.sort((a, b) => a - b);
  for(var i = 0; i < nums.length-2; i++){
    //当下个数开始大于0的时候，就可以停止循环了
    if(nums[i] > 0) return result;
    if(i > 0 && nums[i] === nums[i-1]) continue;
    for(var j = i+1, k = nums.length-1; j < k;){
      if (nums[i] + nums[j] + nums[k] === 0) {
        result.push([nums[i], nums[j], nums[k]]);
        j++; k--;
        // 遇见重复元素就再往后/前移动一位
        while(j < k && nums[j] === nums[j-1]){ j++ };
        while(j < k && nums[k] === nums[k+1]){ k-- };
      } else if (nums[i] + nums[j] + nums[k] > 0) {
        k--;
      } else {
        j++;
      }
    }
  }
  return result;
};
```

leecode上搜的答案：
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    let ans = [];
    const len = nums.length;
    if(nums == null || len < 3) return ans;
    nums.sort((a, b) => a - b); // 排序
    for (let i = 0; i < len ; i++) {
        if(nums[i] > 0) break; // 如果当前数字大于0，则三数之和一定大于0，所以结束循环
        if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
        let L = i+1;
        let R = len-1;
        while(L < R){
            const sum = nums[i] + nums[L] + nums[R];
            if(sum == 0){
                ans.push([nums[i],nums[L],nums[R]]);
                while (L<R && nums[L] == nums[L+1]) L++; // 去重
                while (L<R && nums[R] == nums[R-1]) R--; // 去重
                L++;
                R--;
            }
            else if (sum < 0) L++;
            else if (sum > 0) R--;
        }
    }        
    return ans;
};

```


作者：guanpengchn
链接：https://leetcode-cn.com/problems/3sum/solution/hua-jie-suan-fa-15-san-shu-zhi-he-by-guanpengchn/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

