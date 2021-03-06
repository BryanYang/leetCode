### 只出现一次的数字 Single Number 

#### 题目

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例：

```javascript
输入: [2,2,1]
输出: 1

输入: [4,1,2,1,2]
输出: 4
```

标签： `位运算` `哈希表`

#### 解答

思路1：没有想到比较简单的方法一步做出来。建立map表，循环数组，如果map中存在，就将该值删去，如果没有就把该值作为map的一个属性，赋值true，最后通过`Object.keys(map)[0]`取出里面的唯一属性。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
  var map = {},len = nums.length, cur;
  for(var i = 0; i < len; i++){
    cur = nums[i];
    if(map[cur] != null){
      delete map[cur];
    }else{
      map[cur] = true;
    }
  }
  return +Object.keys(map)[0];
};
```

提交通过。查看其它解答，几乎都是在使用`^`异或符号来解答，简单是简单，但是js中貌似没有这个运算符吧，搞不懂。


排序，然后一个for循环，如果 i !== i-1 && i !== i+1, 那么肯定是它
但是排序的时间复杂度有

答案是使用位运算。对于这道题，可使用异或运算 \oplus⊕。异或运算有以下三个性质。

任何数和 00 做异或运算，结果仍然是原来的数，即 a ^ 0 == a。
任何数和其自身做异或运算，结果是 00，即 a ^ a == 0。
异或运算满足交换律和结合律，即 a^b^a = a^a^b

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/single-number/solution/zhi-chu-xian-yi-ci-de-shu-zi-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
