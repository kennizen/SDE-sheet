Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

 

Example 1:

Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
Example 2:

Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
Example 3:

Input: s = ""
Output: 0
 

Constraints:

0 <= s.length <= 3 * 104
s[i] is '(', or ')'.

ALGO - TC: O(n), SC: O(n)
# using stack to store the index 

class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        st.push(-1);
        int n = s.length();
        int maxi = 0;
        
        for(int i = 0; i<n; i++){
            if(s[i] == '('){
                st.push(i);
            }
            else{
                st.pop();
                if(st.empty()){
                    st.push(i);
                }
                else{
                    maxi = max(maxi, i - st.top());
                }
            }
        }
        
        return maxi;
    }
};

# optimal 
ALGO - TC: O(n), SC: O(1)
# traverse from left to right and then right to left

class Solution {
public:
    int longestValidParentheses(string s) {
        int n = s.length();
        int maxi = 0;
        int l = 0, r = 0;
        
        for(int i = 0; i<n; i++){
            if(s[i] == '(') l++;
            else r++;
            
            if(l == r){
                maxi = max(maxi, 2*r);
            }
            else if(r >= l){
                l = r = 0;
            }
        }
        
        l = r = 0;
        
        for(int i = n-1; i>=0; i--){
            if(s[i] == ')') r++;
            else l++;
            
            if(l == r){
                maxi = max(maxi, 2*l);
            }
            else if(l >= r){
                l = r = 0;
            }
        }
        
        return maxi;
    }
};