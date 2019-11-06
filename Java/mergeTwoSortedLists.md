## Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4/


 Definition for singly-linked list.
 public class ListNode {
      int val;
      ListNode next;
      ListNode(int x) { val = x; }
 } 
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode first = new ListNode(0);
        ListNode node = first;
        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                node.next = l1;
                l1 = l1.next;
            }
            else {
                node.next = l2;
                l2 = l2.next;
            }
           node = node.next;
        }
       if (l1 != null) {
            node.next = l1;
        } 
        if (l2 != null) {
            node.next = l2;
        }
        return first.next;
    }
}
