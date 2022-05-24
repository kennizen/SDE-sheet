Given the head of a singly linked list, return true if it is a palindrome.

 

Example 1:


Input: head = [1,2,2,1]
Output: true
Example 2:


Input: head = [1,2]
Output: false
 

Constraints:

The number of nodes in the list is in the range [1, 105].
0 <= Node.val <= 9
 

Follow up: Could you do it in O(n) time and O(1) space?

ALGO - TC: O(n), SC: O(1)
# first find the middle of the list
# then reverse the list from the middle
# compare the list by iterating 
# return false or true

class Solution {
private:
    ListNode *reverse(ListNode *head)
    {
        if(head == NULL || head->next == NULL)
            return head;
        ListNode *node = reverse(head->next);
        head->next->next = head;
        head->next = NULL;
        return node;
    }
public:
    bool isPalindrome(ListNode* head) {
        
        ListNode *slow = head;
        ListNode *fast = head;
        
        while(fast != NULL)
        {
            slow = slow->next;
            if(fast->next != NULL)
                fast = fast->next->next;
            else
                fast = fast->next;
        }
        
        ListNode *res = reverse(slow);
        ListNode *nl = res;
        
        fast = head;
        
        while(res != NULL)
        {
            if(fast->val != res->val)
                return false;
            res = res->next;
            fast = fast->next;
        }
        
        reverse(nl);
         
        return true;
    }
};