Problem Statement
Given an array of integers ‘ARR’ and an integer ‘X’, you are supposed to find the number of subarrays of 'ARR' which have bitwise XOR of the elements equal to 'X'.
Note:
An array ‘B’ is a subarray of an array ‘A’ if ‘B’ that can be obtained by deletion of, several elements(possibly none) from the start of ‘A’ and several elements(possibly none) from the end of ‘A’. 
Input Format :
The first line contains a single integer ‘T’ denoting the number of test cases. The test cases follow.

The first line of each test case contains two integers ‘N’ and ‘X’ separated by a single space, denoting the number of elements in the array and the required subarray XOR respectively.

The second line of each test case contains ‘N’ single space-separated integers denoting the elements of the array.
Output Format :
For each test case, print on a new line the number of subarrays of the given array that have bitwise XOR of the elements equal to ‘X’.

Print the output of each test case in a separate line.
Note :
You don’t need to print anything; It has already been taken care of.
Constraints :
1 <= T <= 10
3 <= N <= 5 * 10 ^ 4
0 <= X <= 10 ^ 9
0 <= ARR[i] <= 10 ^ 9

Where ‘T’ denotes the number of test cases, ‘N’ denotes the number of elements in the array, ‘X’ denotes the required subarray XOR and ARR[i] denotes the 'i-th' element of the given array.

Time Limit: 1 sec
Sample Input 1 :
2
5 8
5 3 8 3 10
3 7
5 2 9
Sample Output 1 :
2
1
Explanation Of Sample Input 1 :
In the first test case, the subarray from index 1 to index 3 i.e. {3,8,3} and the subarray from index 2 to index 2 i.e. {8} have bitwise XOR equal to 8.

In the second test case, the subarray from index 0 to index 1 i.e. {5,2} has bitwise XOR equal to 7.
Sample Input 2 :
2
6 11
10 1 0 3 4 7
5 4
4 3 1 2 4
Sample Output 2 :
3
4

ALGO - TC: O(nlogn), SC: O(n)
# if val from point a to b is xor then from any point x to b is xor then a to x will be y
# therefore we can say y ^ x = xor also y = x ^ xor
# so if we find the no of y's in the current range of i then we will get the count of subarrays with xor as k
# take a map of prefix xor and count
# calculate the xor check if xor == k if yes count++;
# check for the y's in map by checking xor ^ k
# if found add the count to count
# add the current prefix xor to map  

int subarraysXor(vector<int> &arr, int x)
{
    int count = 0;
	int xorr = 0;
	unordered_map<int,int> umap;
	
	for(int i = 0; i<arr.size(); i++){
		xorr ^= arr[i];
		if(xorr == x) count++;
		if(umap.find(xorr ^ x) != umap.end()) count += umap[xorr^x];
		umap[xorr] += 1;
	}
	return count;
}