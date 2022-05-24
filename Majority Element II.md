Given an integer array of size n, find all elements that appear more than [n/3] times.

 

Example 1:

Input: nums = [3,2,3]
Output: [3]
Example 2:

Input: nums = [1]
Output: [1]
Example 3:

Input: nums = [1,2]
Output: [1,2]
 

Constraints:

1 <= nums.length <= 5 * 104
-109 <= nums[i] <= 109
 

Follow up: Could you solve the problem in linear time and in O(1) space?


class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        
        vector<int> ans;
        
        int c1 = 0, c2 = 0, n1 = INT_MIN, n2 = INT_MIN;
        
        int n = nums.size();
        
        for(int i = 0; i < n; i++){
            if(n1 == nums[i]) 
                c1++;
            else if(n2 == nums[i]) 
                c2++;
            else if(c1 == 0){
                n1 = nums[i];
                c1++;
            }
            else if(c2 == 0){
                n2 = nums[i];
                c2++;
            }
            else{
                c1--;
                c2--;
            }
        }
        
        c1 = c2 = 0;
        
        for(int i = 0; i<n; i++){
            if(n1 == nums[i]) c1++;
            if(n2 == nums[i]) c2++;
        }
        
        if(c1 > n/3) ans.push_back(n1);
        if(c2 > n/3) ans.push_back(n2);
        
        return ans;
    }
};