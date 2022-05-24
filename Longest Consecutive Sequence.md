Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

 

Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
Example 2:

Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
 

Constraints:

0 <= nums.length <= 105
-109 <= nums[i] <= 109

ALGO - TC: O(n), SC: O(n)
# insert all the elements into a hash set
# iterate over the array and look if the previous element for the current element exist in the hashset
# if it exist dont do anything , if it doesnot exist then initialize a count = 1
# check if the next number for the current number exist in the hashSet or not, if it those, increment the num and count
# after the loop update the global count to store the maximum value

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> set;
        
        int n = nums.size();
        int count = 0;
        
        for(int i = 0; i<n; i++){
           set.insert(nums[i]);
        }
        
        for(int i = 0; i<n; i++){
            int curCount = 0;
            if(!set.count(nums[i]-1)){
                int nextNum = nums[i]+1;
                curCount++;
                while(1){
                    if(set.count(nextNum)) curCount++;
                    else break;
                    nextNum++;
                }
            }
            count = max(count, curCount);
        }
        
        return count;
    }
};