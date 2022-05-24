Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

Example 1:

Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
Example 2:

Input: numRows = 1
Output: [[1]]
 

Constraints:

1 <= numRows <= 30


class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        
        vector<vector<int>> res(numRows);
        
        for(int i = 0; i<numRows; i++){
            res[i].resize(i + 1);
            res[i][0] = res[i][i] = 1;
            
            for(int j = 1; j<i; j++) {
                res[i][j] = res[i-1][j] + res[i-1][j-1];
            } 
        }
        
        return res;
    }
};

2nd type given row no. and col no. tell digit

formula is - row-1 C col-1 or [(row-1)!/(row-1)! * (row-col)!]

3rd type given row print whole row

row = 5;

intuition is - nCr use this,
               4C0, 4C1, 4C2, 4C3, 4C4
               trick is multiply col no. in the denominator for the next nCr
               with the previous value.