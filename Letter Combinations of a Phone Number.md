Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.



 

Example 1:

Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
Example 2:

Input: digits = ""
Output: []
Example 3:

Input: digits = "2"
Output: ["a","b","c"]
 

Constraints:

0 <= digits.length <= 4
digits[i] is a digit in the range ['2', '9'].

ALGO - TC: O()

class Solution {
private:
    void solve(vector<string>& v, string ar[], string op, string digits, int k)
    {
        if(k >= digits.length())
        {
            v.push_back(op);
            return;
        }
        
        int index = digits[k] - '0' - 2;
        
        for(int i = 0; i<ar[index].length(); i++)
        {
            op.push_back(ar[index][i]);
            solve(v,ar,op,digits,k+1);
            op.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits) {
        int n = digits.length();
        
        vector<string> v;
        
        if(n == 0)
            return v;
        
        string ar[] = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        
        string op = "";
        
        solve(v, ar, op, digits, 0);
        
        return v;
    }
};