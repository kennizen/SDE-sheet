Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 

Constraints:

1 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 104

intuition - sort the intervals

class Solution {
private:
    pair<int,int> mergeIt(pair<int,int> v1, vector<int> v2){
        pair<int,int> p;
        p.first = v1.first;
        p.second = max(v1.second,v2[1]);
        return p;
    }
public:
    vector<vector<int>> merge(vector<vector<int>>& in) {
        
        int n = in.size();
        vector<vector<int>> ans;
        
        sort(in.begin(),in.end());
        
        pair<int,int> p;
        
        p.first = in[0][0];
        p.second = in[0][1];
        
        for(int i = 0; i<n; i++){
            if(in[i][0] <= p.second)
                p = mergeIt(p, in[i]);
            else{
                vector<int> v(2);
                v[0] = p.first;
                v[1] = p.second;

                ans.push_back(v);

                p.first = in[i][0];
                p.second = in[i][1];
            }
        }
        
        vector<int> v(2);
        v[0] = p.first;
        v[1] = p.second;
        
        ans.push_back(v);
        
        return ans;
    }
};