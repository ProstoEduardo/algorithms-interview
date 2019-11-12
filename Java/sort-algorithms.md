+ [Sort an Array](#sort-an-array)
## Sort an Array

Given an array of integers nums, sort the array in ascending order.

Example 1:
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```
Example 2:
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

```java
class Solution {
    public List<Integer> sortArray(int[] nums) {
       List<Integer> list = new ArrayList<Integer>();
        int t;
        for( int i = 0; i < nums.length; i++){
            for( int j = i + 1; j < nums.length; j++){
            if(nums[i] > nums[j]){
                t = nums[i];
                nums[i] = nums[j];
                nums[j] = t;
            }
            }
        }
        for( int i = 0; i < nums.length; i++){
            list.add(nums[i]);
        }
        return list;
    }
}
```
