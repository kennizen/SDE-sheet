Given an integer array nums, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return the shortest such subarray and output its length.

 

Example 1:

Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
Example 2:

Input: nums = [1,2,3,4]
Output: 0
Example 3:

Input: nums = [1]
Output: 0
 

Constraints:

1 <= nums.length <= 104
-105 <= nums[i] <= 105
 

Follow up: Can you solve it in O(n) time complexity?

ALGO - TC: O(nlogn), SC: O(n)
# find the left and the right boundarys of the unsorted sub array

class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n = nums.size();
        vector<int> copy = nums;
        
        sort(copy.begin(), copy.end());
        
        int l = -1, r = -1;
        
        for(int i = 0; i<n; i++){
            if(copy[i] != nums[i]){
                l = i;
                break;
            }
        }
        
        for(int j = n-1; j>=0; j--){
            if(copy[j] != nums[j]){
                r = j;
                break;
            }
        }
        
        if(l == -1 && r == -1) return 0;
        return r-l+1;
    }
};

ALGO - TC: O(n), SC: O(1)
# we need to find the unsorted subarray so we do the following
# find the left most index from where the array starts to break the sorted order, once we get the index then from that point we try to find the smallest element till the end
# find the right most index from where the array starts to break the sorted order, once we get the index then from that point we try to find the largest element till the start
# once we get them then we see from left which element is just bigger than smallest, because that is the index where the smallest is supposed to be, we do the same from the right, and we find the left and right bounds

class Solution {
    int findMin(int s, int e, vector<int>& nums){
        int smallest = nums[s];
        for(int i = s; i<=e; i++){
            if(nums[i] < smallest){
                smallest = nums[i];
            }
        }
        return smallest;
    }
    
    int findMax(int s, int e, vector<int>& nums){
        int largest = nums[s];
        for(int i = s; i>=e; i--){
            if(nums[i] > largest){
                largest = nums[i];
            }
        }
        return largest;
    }
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n = nums.size();
        int maxi = INT_MIN;
        int mini = INT_MAX;
        int l = -1, r = -1;
        
        for(int i = 1; i<n; i++){
            if(nums[i] < nums[i-1]){
                mini = findMin(i, n-1, nums);
                break;
            }
        }
        
        for(int i = n-2; i>=0; i--){
            if(nums[i] > nums[i+1]){
                maxi = findMax(i, 0, nums);
                break;
            }
        }
        
        for(int i = 0; i<n; i++){
            if(nums[i] > mini){
                l = i;
                break;
            }
        }
        
        for(int i = n-1; i>=0; i--){
            if(nums[i] < maxi){
                r = i;
                break;
            }
        }
        
        return r-l > 0 ? r-l+1 : 0;
    }
};