Given an integer array nums, return the number of reverse pairs in the array.

A reverse pair is a pair (i, j) where 0 <= i < j < nums.length and nums[i] > 2 * nums[j].

 

Example 1:

Input: nums = [1,3,2,3,1]
Output: 2
Example 2:

Input: nums = [2,4,3,5,1]
Output: 3
 

Constraints:

1 <= nums.length <= 5 * 104
-231 <= nums[i] <= 231 - 1

ALGO - merge sort modified

TC: O(nlogn), SC: O(n)

# follow the merge sort approach
# in the step where we get the two sorted arrays we compare the ith term of the left array with the jth term of the right array and increment j until (ith term <= 2 * jth term)
# then we add j to count and increment i

class Solution {
    int count = 0;
public:
    void countReversePairs(vector<int> left, vector<int> right){
        int i = 0, j = 0;
        
        while(i < left.size()){
            while(j < right.size() && left[i] > (2* (long)right[j])) j++;
            count += j;
            i++;
        }
    }
    
    void merge(vector<int> &arr, int n, int s, int m, int e){
        vector<int> left;
        vector<int> right;

        for(int i = s; i<=m; i++) left.push_back(arr[i]);
        for(int i = m+1; i<=e; i++) right.push_back(arr[i]);

        int i = 0, j = 0, k = s;
        
        countReversePairs(left,right); // main step

        while(i < left.size() && j < right.size()){
            if(left[i] <= right[j]){
                arr[k++] = left[i++];
            }else{
                arr[k++] = right[j++];
            }
        }

        while(i < left.size()) arr[k++] = left[i++];
        while(j < right.size()) arr[k++] = right[j++];
    }

    void mergeSort(vector<int> &arr, int n, int s, int e){
        if(s >= e) return;
        int m = s + (e-s)/2;
        mergeSort(arr, n, s, m);
        mergeSort(arr, n, m+1, e);
        merge(arr, n, s, m, e);
    }
    
    int reversePairs(vector<int>& nums) {
        mergeSort(nums, nums.size(), 0, nums.size()-1);
        return count;
    }
};