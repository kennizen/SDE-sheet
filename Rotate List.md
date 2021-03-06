Given the head of a linked list, rotate the list to the right by k places.

 

Example 1:


Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
Example 2:


Input: head = [0,1,2], k = 4
Output: [2,0,1]
 

Constraints:

The number of nodes in the list is in the range [0, 500].
-100 <= Node.val <= 100
0 <= k <= 2 * 109

ALGO - TC: O(n + n - (n%k)), SC: O(1)
# find len of list then if k > len then k = k % len
# then traverse for k = len - k
# point head to that nodes next
# point that node to null

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(head == NULL || head->next == NULL || k == 0) return head;
        int count = 1;
        
        ListNode *tmp = head;
        
        while(tmp->next != NULL){
            count++;
            tmp = tmp->next;
        }
        
        tmp->next = head;
        k = k % count;
        k = count - k;
        
        while(k){
            tmp = tmp->next;
            k--;
        }
        
        head = tmp->next;
        tmp->next = NULL;
        return head;
    }
};