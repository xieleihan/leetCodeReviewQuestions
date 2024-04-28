

# leetCodeReviewQuestions

自己刷题记录仓库
1. **两数之和**

   ```javascript
   
   /**
    * @param {number[]} nums
    * @param {number} target
    * @return {number[]}
    */
   var twoSum = function(nums, target) {
       var l = nums.length; // 取到数据的长度
       var a=[]; // 新建一个变量接受数据
       // 两层for循环遍历
       for (var i = 0; i < l; ++i) {
           for (var j = i + 1; j < l; ++j) {
               if (nums[i] + nums[j] === target) {
                   a.push(i, j);
                   return a; // 在找到结果后立即返回
               }
           }
       }
       return a;
   }
   ```
2. **接雨水**
   ```javascript
   /**
    * @param {number[]} height
    * @return {number}
    */
   var trap = function(height) {
       var x = height.length;
       if (x == 0) {
           return 0;
       }
       
       var leftMax = [];
       var rightMax = [];
       
       leftMax[0] = height[0];
       rightMax[x - 1] = height[x - 1];
       
       // 计算左右边界最大值
       for (var i = 1; i < x; ++i) {
           leftMax[i] = Math.max(leftMax[i - 1], height[i]);
           rightMax[x - i - 1] = Math.max(rightMax[x - i], height[x - i - 1]);
       }
       
       var sum = 0;
       for (var i = 0; i < x; ++i) {
           sum += Math.min(leftMax[i], rightMax[i]) - height[i];
       }
       
       return sum;
   };
   ```
3. **三数之和**
   ```javascript
   /**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    nums.sort((a, b) => a - b); // 将数组排序
    const result = [];

    const length = nums.length;
    for (let i = 0; i < length - 2; i++) {
        // 避免重复的第一个数
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }
        
        for (let j = i + 1; j < length - 1; j++) {
            // 避免重复的第二个数
            if (j > i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }

            for (let k = j + 1; k < length; k++) {
                // 避免重复的第三个数
                if (k > j + 1 && nums[k] === nums[k - 1]) {
                    continue;
                }

                if (nums[i] + nums[j] + nums[k] === 0) {
                    result.push([nums[i], nums[j], nums[k]]);
                }
            }
        }
    }

    return result;
};
```


# 框架
   ```javascript
   ```

   
