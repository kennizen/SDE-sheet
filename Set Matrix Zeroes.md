Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

 

Example 1:


Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
Example 2:


Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
 

Constraints:

m == matrix.length
n == matrix[0].length
1 <= m, n <= 200
-231 <= matrix[i][j] <= 231 - 1
 

Follow up:

A straightforward solution using O(mn) space is probably a bad idea.
A simple improvement uses O(m + n) space, but still not the best solution.
Could you devise a constant space solution?


class Solution {
private:
    void makeZero(vector<vector<int>>& matrix, int i, int j) {
        // up
        for(int l = i; l>=0; l--){
            matrix[l][j] = 0;
        }
        
        // left
        for(int l = j; l>=0; l--){
            matrix[i][l] = 0;
        }
        
        // down
        for(int l = i; l < matrix.size(); l++){
            matrix[l][j] = 0;
        }
        
        // right
        for(int l = j; l < matrix[0].size(); l++){
            matrix[i][l] = 0;
        }
    }
public:
    void setZeroes(vector<vector<int>>& matrix) {
        vector<pair<int,int>> v;
        
        int row = matrix.size();
        int col = matrix[0].size();
        
        for(int i = 0; i<row; i++){
            for(int j = 0; j<col; j++){
                if(matrix[i][j] == 0){
                    pair<int,int> p;
                    p.first = i;
                    p.second = j;
                    v.push_back(p);
                }
            }
        }
        
        for(int i = 0; i<v.size(); i++)
            makeZero(matrix, v[i].first, v[i].second);
        }
    }
};

optimised

intuition - make a dummy row & col in the matrix itself and check for matrix[i][j] == 0

ALGO - TC: O(nm), SC: O(1)
# make the dummy array the top row and the left most column
# start traversing from the beginning
# if we encounter a 0 other than the first column then set the top and left points of the dummy array as 0
# if the encountered 0 is in the first column then set col0 = false
# after the traversal start traversing from the back and check if for a cell any of the row or col is 0 if yes set the cell to 0
# lastly if for first col, col0 == false, then set that cell to be 0

class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        
        int row = matrix.size();
        int col = matrix[0].size();
        bool col0 = true;
        
        for(int i = 0; i<row; i++){
            if(matrix[i][0] == 0){
                col0 = false;
            }
            for(int j = 1; j<col; j++){
                if(matrix[i][j] == 0){
                   matrix[i][0] = matrix[0][j] = 0;
                }
            }
        }
        
        for(int i = row-1; i>=0; i--){
            for(int j = col-1; j>=1; j--){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                   matrix[i][j] = 0;
                }
            }
            if(!col0){
                matrix[i][0] = 0;
            }
        }
    }
};