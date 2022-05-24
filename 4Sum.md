Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.

 

Example 1:

Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
Example 2:

Input: nums = [2,2,2,2,2], target = 8
Output: [[2,2,2,2]]
 

Constraints:

1 <= nums.length <= 200
-109 <= nums[i] <= 109
-109 <= target <= 109

ALGO - TC: O(n^3), SC: O(1)
# sort the array
# take two pointer i and j, where  i = 0, j = i + 1
# in the linner loop take two more pointers left and right, where left = j+1, right = n-1
# calculate rem = target - left - right
# see if left + right > rem or left + right < rem
# if > right--, if < left++
# if left + right == rem, store the quadruple
# then increment and decrement the left and right skipping the duplicate values
# also increment i and j skipping the duplicate values as we need only unique quadruples 

class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        
        vector<vector<int>> ans;
        
        sort(nums.begin(), nums.end());
        
        int i,j;
        
        for(i = 0; i<n; i++){
            for(j = i+1; j<n; j++){
                int left = j+1;
                int right = n-1;
                int rem = target - nums[i] - nums[j]; 
                
                while(left < right){
                    if(nums[left] + nums[right] < rem){
                        left++;
                    }
                    else if(nums[left] + nums[right] > rem){
                        right--;
                    }
                    else{
                        vector<int> v(4,0);
                        v[0] = nums[i];
                        v[1] = nums[j];
                        v[2] = nums[left];
                        v[3] = nums[right];
                        ans.push_back(v);
                        
                        while(left < right && nums[left] == v[2]) ++left;
                        while(left < right && nums[right] == v[3]) --right;
                    }
                }
                while(j+1 < n && nums[j+1] == nums[j]) ++j;
            }
            while(i+1 < n && nums[i+1] == nums[i]) ++i;
        }
        return ans;
    }
};