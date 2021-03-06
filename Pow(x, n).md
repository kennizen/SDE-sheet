Implement pow(x, n), which calculates x raised to the power n (i.e., xn).

 

Example 1:

Input: x = 2.00000, n = 10
Output: 1024.00000
Example 2:

Input: x = 2.10000, n = 3
Output: 9.26100
Example 3:

Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
 

Constraints:

-100.0 < x < 100.0
-231 <= n <= 231-1
-104 <= xn <= 104

intuition - 
# if power(n) is odd then ans = ans * num, power = power-1
# if power(n) is even then num = num * num, power = power/2

class Solution {
public:
    double myPow(double x, int n) {
        double ans = 1;
        long nn = n;
        
        if(nn < 0) nn *= -1;
        
        while(nn){
            if(nn % 2 != 0){
                ans *= x;
                nn--;
            }
            else{
                x *= x;
                nn /= 2;
            }
        }
        
        if(n < 0) return 1.0/ans;
        return ans;
    }
};