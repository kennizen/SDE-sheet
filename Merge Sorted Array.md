You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

 

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
 

Constraints:

nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-109 <= nums1[i], nums2[j] <= 109

ALGO - GAP method

class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) 
    {
      int j = 0, i = 0;
        
      for(int i = m; i<m+n; i++,j++)
        nums1[i]=nums2[j];
        
      int gap = ceil((m+n)/2);
        
      while(gap >= 1)
      {
        i = 0, j = i+gap;
        while(j < (m+n)) 
        {
            if(nums1[i] > nums1[j]) 
                swap(nums1[i],nums1[j]);
            i++;
            j++;
        }
        if(gap == 1) break;
        gap = gap%2 ? (gap/2)+1 : gap/2;
      }
    }
};

ALGO - TC: O(n), SC: O(1)
# iterate from the last of both the arrays
# fill the last of the first array while comparing with the second array
# it nums1[i] > nums2[j] then nums1[lastpos] = nums1[i] and nums1[i] = nums2[j] 

class Solution {
public:
     void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m-1;
        int j =n-1;
        int tar = n+m-1;
        
        while (j >=0){
            if (i>=0 && nums1[i] > nums2[j]){
                nums1[tar] = nums1[i];
                nums1[i] = nums2[j]; 
                tar -=1;
                i -=1;
            }
            else{
                nums1[tar] = nums2[j];
                tar -=1;
                j -=1;
            }
        }
    }
};

TC - O(mn) SC - O(1)
class Solution {
private:
    void sortIt(vector<int>& nums2){
        int i = 0;
        while(i < nums2.size()){
            if(i + 1 < nums2.size() && nums2[i+1] < nums2[i])
                swap(nums2[i],nums2[i+1]);
            i++;
        }
    }
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int j = 0;
        
        if(m == 0)
            nums1 = nums2;
        else if(n != 0){
            for(int i = 0; i<m; i++){
                if(nums1[i] > nums2[j]){
                    swap(nums1[i],nums2[j]);
                    sortIt(nums2);
                }
            }
            for(int i = m; i< m+n; i++,j++){
                nums1[i] = nums2[j];
            }
        }
    }
};

TC - O(n) SC - O(m+n)
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int> temp;
        int i = 0, j =0;
        
        while(i < m && j < n)
        {
            if(nums1[i] < nums2[j])
            {
                temp.push_back(nums1[i]);
                i++;
            }
            else
            {
                temp.push_back(nums2[j]);
                j++;
            }
        }
        
        while(i < m)
        {
            temp.push_back(nums1[i]);
            i++;
        }
        
        while(j < n)
        {
            temp.push_back(nums2[j]);
            j++;
        }
        
        nums1 = temp; 
    }
};