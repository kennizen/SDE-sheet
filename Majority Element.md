Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

 

Example 1:

Input: nums = [3,2,3]
Output: 3
Example 2:

Input: nums = [2,2,1,1,1,2,2]
Output: 2
 

Constraints:

n == nums.length
1 <= n <= 5 * 104
-231 <= nums[i] <= 231 - 1
 

Follow-up: Could you solve the problem in linear time and in O(1) space?


class Solution {
public:
    int majorityElement(vector<int>& nums) {
        
        int n = nums.size();
        
        unordered_map<int,int> umap;
        
        for(int i = 0; i<n; i++)
        {
            if(umap.find(nums[i]) != umap.end())
                umap[nums[i]]++;
            else
                umap.insert({nums[i],1});
            if(umap[nums[i]] > n/2)
                return nums[i];
        }
        
        return 0;
    }
};

ALGO - Moore voting
TC: O(n), SC: O(1)

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n = nums.size();
        int count = 0, ele;
        
        for(int i = 0; i<n; i++)
        {
            if(count == 0){
                ele = nums[i];
                count++;
            }
            else if(ele == nums[i])
                count++;
            else
                count--;
        }
        return ele;
    }
};