# Partition Array

## Partition Array

Given an array`nums`of integers and an int`k`, partition the array (i.e move the elements in "nums") such that:

* All elements < _k \_are moved to the \_left_
* All elements >= _k \_are moved to the \_right_

Return the partitioning index, i.e the first index nums\[_i_] >=_k_.

## Example

If nums =`[3,2,2,1]`and`k=2`, a valid answer is`1`.

## Note

快速排序的划分过程

返回左指针就行啦

## Code

```java
public class Solution {
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            while (left <= right && nums[left] < k) {
                left++;
            }
            while (left <= right && nums[right] >= k) {
                right--;
            }
            if (left <= right) {
                int temp = nums[left];
                nums[left++] = nums[right];
                nums[right--] = temp;
            }
        }
        return left;
    }
}
```
