![leetCodeReviewQuestions](https://socialify.git.ci/xieleihan/leetCodeReviewQuestions/image?description=1&font=Source%20Code%20Pro&forks=1&issues=1&language=1&logo=https%3A%2F%2Favatars.githubusercontent.com%2Fu%2F57227318%3Fs%3D400%26u%3D0042e26f16ac9b24babe9cc6d8f659ba4167f457%26v%3D4&name=1&owner=1&pattern=Floating%20Cogs&pulls=1&stargazers=1&theme=Light)

# leetCodeReviewQuestions

自己刷题记录仓库
> 不按顺序

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

  - 下面这个不是很好,测试用例有个超过时间限制

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
  - 改进版:*上面它的时间复杂度是O(n^3)，因为它使用了三重循环来遍历所有可能的组合。这种解法对于较大规模的输入会导致超出时间限制。一种优化思路是通过减少循环的次数来降低时间复杂度。可以通过使用双指针的方法来替代其中的一到两个循环。以下是一个优化后的解法*
  ```javascript
  /**
   * @param {number[]} nums
   * @return {number[][]}
   */
  var threeSum = function(nums) {
      nums.sort((a, b) => a - b);
      const result = [];
  
      const length = nums.length;
      for (let i = 0; i < length - 2; i++) {
          if (i > 0 && nums[i] === nums[i - 1]) {
              continue;
          }
          
          let left = i + 1;
          let right = length - 1;
  
          while (left < right) {
              const sum = nums[i] + nums[left] + nums[right];
              if (sum === 0) {
                  result.push([nums[i], nums[left], nums[right]]);
                  
                  // 去重
                  while (left < right && nums[left] === nums[left + 1]) {
                      left++;
                  }
                  while (left < right && nums[right] === nums[right - 1]) {
                      right--;
                  }
                  
                  // 移动指针
                  left++;
                  right--;
              } else if (sum < 0) {
                  left++;
              } else {
                  right--;
              }
          }
      }
  
      return result;
  };
  ```

4. **最接近三数之和**

	```javascript
	/**
	 * @param {number[]} nums
	 * @param {number} target
	 * @return {number}
	 */
	var threeSumClosest = function(nums, target) {
	    nums.sort((a,b)=>a - b);
	    var l = nums.length;
	    // 定义一个最接近的值,后续修改
	    var res = nums[0] + nums[1] + nums[2];
	
	    for(var i =0 ;i<l-2;i++){
	        var leftPointer = i+1;
	        var rightPointer = l-1;
	
	        // 左指针向右,右向左 逼近
	        while(leftPointer < rightPointer){
	            const sum = nums[i] + nums[leftPointer] + nums[rightPointer];
	            // 由于我们的一个题目的要求是要最接近值,所以,可以用绝对值的方式来判断是最合适的
	            if(Math.abs(sum-target) < Math.abs(res-target)){
	                res = sum;
	            }
	            // 理想情况,达到预期,直接return出去
	            if(sum == target){
	                return sum;
	            }
	            // 不然的话做出判断,指针走,再循环
	            else if (sum < target){
	                leftPointer++;
	            }else{
	                rightPointer--;
	            }
	        }
	    }
	    // 结果弹出
	    return res;
	};
	```

5. **四数之和**

	```JavaScript
	/**
	* @param {number[]} nums
	* @param {number} target
	* @return {number[][]}
	*/
	var fourSum = function (nums, target) {
		// 跟三数之和是差不多的
		/**  
		 * 第一步:我们还是对数组进行排序,方便我们的双指针
		 * 因为什么呢,遇到这种多数计算的,双指针可以更好的实现
		 * 相比我之前的暴力解法,这种方式很好
		 */
		nums.sort((a, b) => a - b);
		var res = new Array();
		var l = nums.length;
		// 外层遍历数组,固定第一个数
		for (var i = 0; i < l - 3; i++) {
		    // 如果当前的数与上一个数相等,则跳过
		    if (i > 0 && nums[i] == nums[i - 1]) {
		        continue;
		    }
		    // 二层循环,用于固定第二个数
		    for (var j = i + 1; j < l - 2; j++) {
		        // 跟上一个数相等的话直接跳过
		        if (j > i + 1 && nums[j] == nums[j - 1]) {
		            continue;
		        }
		
		        // 定义左右Pointer
		        var leftPointer = j + 1;
		        var rightPointer = l - 1;
		
		        // 遍历剩下的数组,找另外两个数
		        while (leftPointer < rightPointer) {
		            // const sum = nums[0]+nums[1]+nums[2]+nums[3]+nums[4];
		            // 设置当前四个数的和
		            const sum = nums[i] + nums[j] + nums[leftPointer] + nums[rightPointer];
		
		            // 如果等于target
		            if (sum == target) {
		                // 进入数组
		                res.push([nums[i], nums[j], nums[leftPointer], nums[rightPointer]])
		
		                // 跳过重复的左pointer
		                while (leftPointer < rightPointer && nums[leftPointer] == nums[leftPointer + 1]) {
		                    leftPointer++;
		                }
		                // 跳过重复的右pointer
		                while (leftPointer < rightPointer && nums[rightPointer] == nums[rightPointer - 1]) {
		                    rightPointer--;
		                }
		
		                // 移动左右pointer
		                leftPointer++;
		                rightPointer--;
		            } else if (sum < target) {
		                // sum小于target,左pointer右移
		                leftPointer++;
		            }
		            else {
		                // 否则,右pointer左移
		                rightPointer--;
		            }
		        }
		    }
		}
		
		return res;
	};
	```

		



# 框架
   ```javascript
   ```

   
