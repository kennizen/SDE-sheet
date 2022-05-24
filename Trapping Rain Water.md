Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

 

Example 1:


Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
Example 2:

Input: height = [4,2,0,3,2,5]
Output: 9
 

Constraints:

n == height.length
1 <= n <= 2 * 104
0 <= height[i] <= 105

Approach - 1
ALGO - TC: O(n), SC: O(n)
# using preffix max array and suffix max array
# for every index finding the left most max and right most max then min of them - the current height

class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        int pre = height[0];
        int suf = height[n-1];
        int ans = 0;
        
        vector<int> preMax(n, 0);
        vector<int> sufMax(n, 0);
        
        for(int i = 0; i<n; i++){
            pre = max(height[i], pre);
            preMax[i] = pre;
        }
        
        for(int i = n-1; i>=0; i--){
            suf = max(height[i], suf);
            sufMax[i] = suf;
        }
        
        for(int i = 0; i<n; i++){
            ans += min(preMax[i], sufMax[i]) - height[i];
        }
        
        return ans;
    }
};

Optimal 
ALGO - TC: O(n), SC: O(1)
# two pointer approach
# making sure of the left and the right max by comparing the two heights at i and j and keeping track of the leftmax and rightmax

class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        int ans = 0;
        int leftmax = 0, rightmax = 0;
        int i = 0, j = n-1;
        
        while(i <= j){
            if(height[i] <= height[j]){
                if(height[i] > leftmax) 
                    leftmax = height[i];
                else 
                    ans += leftmax - height[i];
                i++;
            }
            else{
                if(height[j] > rightmax) 
                    rightmax = height[j];
                else 
                    ans += rightmax - height[j];
                j--;
            }
        }
        
        return ans;
    }
};