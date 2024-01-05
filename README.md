
### Question:
Efficiently search for a target value within a pre-sorted 2D matrix, utilizing a binary search strategy that exploits the ordered structure of both rows and columns.

### Solution:
```
public class Solution {
    public static void main(String[] args) {
        int[][] nums = {
                {1,2,3,4},
                {5,6,7,8},
                {9,10,11,12},
                {13,14,15,16}
        };
        int target = 10;
        System.out.println(search(nums,target));
    }

    static boolean search(int[][] nums, int target){
        int rStart = 0;
        int rEnd = nums.length - 1;
        int cStart = 0;
        int cEnd = nums[0].length - 1;
        int cMid = cStart + (cEnd - cStart) / 2;
        while (rStart <= rEnd-2){
            int rMid = rStart + (rEnd - rStart) / 2;

            if(nums[rMid][cMid] == target) return true;

            if(nums[rMid][cMid] < target) rStart = rMid;

            else if (nums[rMid][cMid] > target) rEnd = rMid;
        }
        
        boolean flag = false;
        if(nums[rStart][cMid] == target) return true;
        if(nums[rEnd][cMid] == target) return true;
        if(nums[rStart][cMid] > target){
            flag = binSearch(nums[rStart], cStart, cMid-1, target);
            if(flag) return true;
        }
        if(nums[rStart][cMid] < target){
            flag = binSearch(nums[rStart], cMid+1, cEnd, target);
            if(flag) return true;
        }
        if(nums[rEnd][cMid] > target){
            flag = binSearch(nums[rEnd], cStart, cMid-1, target);
            if(flag) return true;
        }
        if(nums[rEnd][cMid] < target){
            flag = binSearch(nums[rEnd], cMid+1, cEnd, target);
            if(flag) return true;
        }
        return false;
    }

    static boolean binSearch(int[] arr, int start, int end, int target){
        if(start == end){
            if(arr[start] != target) return false;
            return true;
        }
        while (start <= end){
            int mid = start + (end - start) / 2;

            if(arr[mid] == target) return true;

            if(arr[mid] < target) start = mid + 1;

            else end = mid - 1;
        }
        return false;
    }
}

```
