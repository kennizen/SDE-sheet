Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

 

Example 1:

Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
Example 2:

Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
Example 3:

Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
 

Constraints:

1 <= s.length, t.length <= 200
s and t only contain lowercase letters and '#' characters.
 

Follow up: Can you solve it in O(n) time and O(1) space?

ALGO - TC: O(n), SC: O(n)
# using stack

class Solution {
public:
    bool backspaceCompare(string s, string t) {
        stack<char> st;
        
        for(int i = 0; i<s.length(); i++){
            if(s[i] == '#' && !st.empty()){
                st.pop();
            }
            else if(s[i] != '#'){
                st.push(s[i]);
            }
        }
        
        s = "";
        
        while(!st.empty()){
            s += st.top();
            st.pop();
        }
        
        for(int i = 0; i<t.length(); i++){
            if(t[i] == '#' && !st.empty()){
                st.pop();
            }
            else if(t[i] != '#'){
                st.push(t[i]);
            }
        }
        
        t = "";
        
        while(!st.empty()){
            t += st.top();
            st.pop();
        }
        
        return s == t;
    }
};

ALGO - TC: O(n), SC: O(1)
# using two pointer by modifying the given strings
# traverse the string with a pointer k that points to the index that is to be filled after getting a # 

class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int k=0,p=0;

        for(int i=0; i<s.size(); i++)
        {
            if(s[i] == '#') {
                k--;
                k = max(0,k);
            }
            else {
                s[k] = s[i];
                k++;
           }
        }
        
        for(int i=0;i<t.size();i++)
        {
            if(t[i] == '#'){
                p--;
                p = max(0,p);
            }
            else {
                t[p] = t[i];
                p++;
            }
        }
        
        if(k != p) return false;
        else {
            for(int i=0; i<k; i++){
                if(s[i] != t[i]) return false;
            }
        }
        return true;
    }
};