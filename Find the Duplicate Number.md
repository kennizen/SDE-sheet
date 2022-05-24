Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

Example 1:

Input: nums = [1,3,4,2,2]
Output: 2
Example 2:

Input: nums = [3,1,3,4,2]
Output: 3
 
Constraints:

1 <= n <= 105
nums.length == n + 1
1 <= nums[i] <= n
All the integers in nums appear only once except for precisely one integer which appears two or more times.
 
Follow up:

How can we prove that at least one duplicate number must exist in nums?
Can you solve the problem in linear runtime complexity?

ALGO - TC: O(n), SC: O(1)
# linked list tortoise method.
# fast ans slow pointer
# fist loop till fast == slow
# then fast = first then again loop till fast == slow
# return fast or slow, this is the duplicate

class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int fast = nums[0];
        int slow = nums[0];
        
        while(1){
            slow = nums[slow];
            fast = nums[nums[fast]];
            if(slow == fast) break;
        }
        
        fast = nums[0];
        
        while(slow != fast){
            slow = nums[slow];
            fast = nums[fast];
        }
        
        return slow;
    }
};

class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int i = 0;
		
        while(1){
            if(nums[i] != i+1){
                if(nums[i] == nums[nums[i]])
                    return nums[i];
                if(nums[i] < i)
                    return nums[i];
                swap(nums[i], nums[nums[i]]);
            }
            else
                i++;
        }
    }
};

Approach 3: Negative Marking
Note: This approach temporarily modifies individual elements and thus does not satisfy the problem constraints. However, this approach is intuitive and utilizes a technique that is useful to know. Furthermore, the underlying concept lends itself to solving similar problems. As such, you can further practice this technique on other problems such as 41. First Missing Positive.

Intuition

There are n + 1n+1 positive numbers in the array (numsnums) (all in the range [1, n][1,n]). Since the array only contains positive integers, we can track each number (numnum) that has been seen before by flipping the sign of the number located at index |num|∣num∣, where ||∣∣ denotes absolute value.

For example, if the input array is [1, 3, 3, 2][1,3,3,2], then for 11, flip the number at index 11, making the array [1,-3,3,2][1,−3,3,2]. Next, for -3−3 flip the number at index 33, making the array [1,-3,3,-2][1,−3,3,−2]. Finally, when we reach the second 33, we'll notice that nums[3]nums[3] is already negative, indicating that 33 has been seen before and hence is the duplicate number.

Algorithm

Iterate over the array, evaluating each element (let's call the current element curcur).

Since we use negative marking, we must ensure that the current element (curcur) is positive (i.e. if curcur is negative, then use its absolute value).

Check if nums[cur]nums[cur] is negative.

If it is, then we have already performed this operation for the same number, and hence curcur is the duplicate number. Store curcur as the duplicate and exit the loop.

Otherwise, flip the sign of nums[cur]nums[cur] (i.e. make it negative). Move to the next element and repeat step 3.

Once we've identified the duplicate, we could just return the duplicate number. However, even though we were not able to meet the problem constraints, we can show that we are mindful of the constraints by restoring the array. This is done by changing all negative numbers to positive.