Problem Statement
For a given integer array/list 'ARR' of size 'N', find the total number of 'Inversions' that may exist.
An inversion is defined for a pair of integers in the array/list when the following two conditions are met.
A pair ('ARR[i]', 'ARR[j]') is said to be an inversion when:

1. 'ARR[i] > 'ARR[j]' 
2. 'i' < 'j'

Where 'i' and 'j' denote the indices ranging from [0, 'N').
Input Format :
The first line of input contains an integer 'N', denoting the size of the array.

The second line of input contains 'N' integers separated by a single space, denoting the elements of the array 'ARR'.
Output Format :
Print a single line containing a single integer that denotes the total count of inversions in the input array.
Note:
You are not required to print anything, it has been already taken care of. Just implement the given function.  
Constraints :
1 <= N <= 10^5 
1 <= ARR[i] <= 10^9

Where 'ARR[i]' denotes the array element at 'ith' index.

Time Limit: 1 sec
Sample Input 1 :
3
3 2 1
Sample Output 1 :
3
Explanation Of Sample Output 1:
We have a total of 3 pairs which satisfy the condition of inversion. (3, 2), (2, 1) and (3, 1).
Sample Input 2 :
5
2 5 1 3 4
Sample Output 2 :
4
Explanation Of Sample Output 1:
We have a total of 4 pairs which satisfy the condition of inversion. (2, 1), (5, 1), (5, 3) and (5, 4).

ALGO - merge sort modification
TC: O(nlogn), SC: O(1)
# follow the merge sort approach
# in the merge part if the left side element is greater than the right one than everything on the left will also be greater than that right element thus forming inversions so count them at that position

#include<bits/stdc++.h>

void merge(long long *arr, int n, int s, int m, int e, long long &count){
	vector<int> left;
	vector<int> right;
	
	for(int i = s; i<=m; i++) left.push_back(arr[i]);
	for(int i = m+1; i<=e; i++) right.push_back(arr[i]);
	
	int i = 0, j = 0, k = s;
	
	while(i < left.size() && j < right.size()){
		if(left[i] <= right[j]){
			arr[k++] = left[i++];
		}else{
			arr[k++] = right[j++];
			count += left.size()-i; // main step
		}
	}
	
	while(i < left.size()) arr[k++] = left[i++];
    while(j < right.size()) arr[k++] = right[j++];
}

void mergeSort(long long *arr, int n, int s, int e, long long &count){
	if(s >= e) return;
	int m = s + (e-s)/2;
	mergeSort(arr, n, s, m, count);
	mergeSort(arr, n, m+1, e, count);
	merge(arr, n, s, m, e, count);
}

long long getInversions(long long *arr, int n){
    long long count = 0;
	mergeSort(arr, n, 0, n-1, count);
	return count;
}