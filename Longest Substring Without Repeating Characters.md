Given a string s, find the length of the longest substring without repeating characters.

 

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 

Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.

ALGO - TC: O(n), SC: O(n)
# better than sliding window approach
# instead of jumping l one at a time jump to last index + 1 of the repeating character
# take a map of char and there last seen position
# take l and r pointer
# traverse with r if s[r] present in map then check if the last index of that character is greater than or equal to l if yes update l
# update new len, insert s[r], increment r

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char,int> umap;
        
        int l = 0, r = 0;
        int n = s.length();
        int len = 0;
        
        while(r < n){
            if(umap.find(s[r]) != umap.end()){
                if(umap[s[r]] >= l){
                    l = umap[s[r]] + 1;
                }
            }
            
            len = max(len, (r-l)+1);
            umap[s[r]] = r;
            r++;
        }
        
        return len;
    }
};