Given an array of n integers nums, a 132 pattern is a subsequence of three integers nums[i], nums[j] and nums[k] such that i < j < k and nums[i] < nums[k] < nums[j].

Return true if there is a 132 pattern in nums, otherwise, return false.

 

Example 1:

Input: nums = [1,2,3,4]
Output: false
Explanation: There is no 132 pattern in the sequence.
Example 2:

Input: nums = [3,1,4,2]
Output: true
Explanation: There is a 132 pattern in the sequence: [1, 4, 2].
Example 3:

Input: nums = [-1,3,2,0]
Output: true
Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].

Constraints:

n == nums.length
1 <= n <= 2 * 105
-109 <= nums[i] <= 109

ALGO - TC: O(n), SC: O(n)
# we need a monotonically decreasing stack with every element on the stack with a value and the minimum before that value.
# we need i < j < k but nums[i] < nums[k] < nums[j] so we need to find nums[k]
# minimum will hold nums[i], stack top will hold nums[j]

class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        stack<pair<int,int>> st;
        int n = nums.size();
        int mini = nums[0];
        
        for(int i = 1; i<n; i++){
            while(!st.empty() && nums[i] >= st.top().first){
                st.pop();
            }
            if(!st.empty() && nums[i] > st.top().second){
                return true;
            }
            st.push({nums[i], mini});
            mini = min(mini, nums[i]);
        }
        
        return false;
    }
};