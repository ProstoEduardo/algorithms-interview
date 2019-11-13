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
#### Bubble Sort
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
#### MergeSort

```java
public int[] sortArray(int[] nums) {
        mergeSort(nums, 0, nums.length - 1);
        return nums;
    }
    
    public static void mergeSort(int[] a, int left, int right){
        if(left >= right)
            return;
        int mid = (left + right)/2;
        mergeSort(a, left, mid);
        mergeSort(a, mid + 1, right);
        merge(a, left, mid, right);
    }
    
    public static void merge(int[] a, int left, int mid, int right){
        int r1 = mid + 1;
        int[] tmp = new int[a.length];
        int index = left;
        int c = left;
        
        while(left <= mid && r1 <= right){
            if(a[left] <= a[r1]){
                tmp[index] = a[left];
                index++;
                left++;
            }
            else{
                tmp[index] = a[r1];
                index++;
                r1++;
            }
        }
        while(left <= mid){
            tmp[index] = a[left];
            index++;
            left++;
        }
        while(r1 <= right){
            tmp[index] = a[r1];
            index++;
            r1++;
        }
        while(c <= right){
            a[c] = tmp[c];
            c++;
        }
    }
 ```
#### QuickSort

```java
public int[] sortArray(int[] nums) {
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }
    public static void quickSort(int[] a, int left, int right){
        int i = left;
        int j = right;
        int key, tmp;
        if(left > right)
            return;
        key = a[left];
        
        while(i < j){
            while(key <= a[j] && i < j){
                j--;
            }
            while(key >= a[i] && i < j){
                i++;
            }
            if(i < j){
                tmp = a[j];
                a[j] = a[i];
                a[i] = tmp;
            }
        }
        a[left] = a[i];
        a[i] = key;
        
        quickSort(a, left, j-1);
        quickSort(a, j+1, right);
    }
```
