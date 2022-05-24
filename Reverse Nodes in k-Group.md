Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

 

Example 1:


Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
Example 2:


Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
 

Constraints:

The number of nodes in the list is n.
1 <= k <= n <= 5000
0 <= Node.val <= 1000
 

Follow-up: Can you solve the problem in O(1) extra memory space?

# recursive

class Solution {
    int length(ListNode*head){
        int len = 0;

        while(head != NULL){
            len++;
            head = head->next;
        }

        return len;
    }
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        int len = length(head);

        if(head == NULL){
            return NULL;
        }    

        //reverse firse k nodes
        ListNode *next = NULL;
        ListNode *current = head;
        ListNode *pre = NULL;

        int count = 0; int itr = len;      

        while(count<k && current!=NULL){
            next = current->next;
            current->next = pre;
            pre=current;
            current = next;
            count++;
            itr--;
        }

        //recursion kar lega
        if(next != NULL && itr >= k){
            head->next = reverseKGroup(next,k);
        }
        else{
            head->next = next;
            return pre;
        }

        return pre;
    }
};

# iterative

class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(head == NULL || k == 1) return head;
        int count = 0;
        ListNode* tmp = head;
        
        while(tmp != NULL){
            count++;
            tmp = tmp->next;
        }
        
        ListNode* dummy = new ListNode();
        dummy->next = head;
        
        ListNode* next = dummy;
        ListNode* cur = dummy;
        ListNode* prev = dummy;
        
        while(count >= k){
            cur = prev->next;
            next = cur->next;
            for(int i = 1; i<k; i++){
                cur->next = next->next;
                next->next = prev->next;
                prev->next = next;
                next = cur->next;
            }
            prev = cur;
            count -= k;
        }
        
        return dummy->next;
    }
};