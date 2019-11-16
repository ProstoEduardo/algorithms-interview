+ [Binary Search](#binary-search)
+ [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)

## Binary Search

https://leetcode.com/problems/binary-search/

Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.

Example 1:
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```
Example 2:
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```
```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0;
        int r =nums.length - 1;
        int middle;
        while (l <= r) {
            middle = l + (r - l) / 2;
            if (nums[middle] == target){
                return middle;}
            if (target < nums[middle]){
                r = middle - 1;}
            else {l = middle + 1;}
        }
    return -1;
    }
}
```
## Search in Rotated Sorted Array

https://leetcode.com/problems/search-in-rotated-sorted-array/

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
Example 2:
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```
```java
class Solution {
 public int search(int[] nums, int target) {
        int l = 0;
		int r = nums.length - 1;
		int mid;
		while(l <= r) {
			mid = (r + l) / 2;
			if(nums[mid] == target) {
				return mid;
			}
			if(nums[mid] >= nums[l]) {
				if(target <= nums[mid] && target >= nums[l]) {
					r = mid - 1;
				} else {
					l = mid + 1;
				}
			} else if(nums[mid] < nums[l]) {
				if(target >= nums[mid] && target <= nums[r]) {
					l = mid + 1;
				} else {
					r = mid - 1;
				}
			}
		}
		return -1;
    }
}
```
