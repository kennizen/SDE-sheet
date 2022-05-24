Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Example 2:

Input: nums = []
Output: []
Example 3:

Input: nums = [0]
Output: []
 

Constraints:

0 <= nums.length <= 3000
-105 <= nums[i] <= 105

ALGO - TC: O(n^2), SC: O(1)
# same as 4 sum

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        
        if(nums.size() < 3) return ans;
        
        for(int i = 0; i<n; i++){
            int left = i+1;
            int right = n-1;
            
            while(left < right){
                int sum = nums[i] + nums[left] + nums[right];
                
                if(sum < 0) left++;
                else if(sum > 0) right--;
                else{
                    vector<int> v(3,0);
                    v[0] = nums[i];
                    v[1] = nums[left];
                    v[2] = nums[right];
                    ans.push_back(v);

                    while(left < right && nums[left] == v[1]) ++left;
                    while(left < right && nums[right] == v[2]) --right;
                }
            }
            while(i+1 < n && nums[i+1] == nums[i]) ++i;
        }
        
        return ans;
    }
};