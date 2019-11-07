# Linked lists
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Reverse Linked List](#reverse-linked-list)

### Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4

Output: 1->1->2->3->4->4
```
``` java
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
```
## Reverse Linked List

Reverse a singly linked list.

Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode nextTemp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextTemp;
    }
    return prev;
}
```
Пример для понимания:

1 > 2 > 3 > 4 > 5 > null - our list

Before the while(...) loop: node = 1, head = null

While moving over the list:
```
1 step:                 1 > null; node = 1, head = null, node.next = head, head = node

2 step:             2 > 1 > null; node = 2, head = 1,    node.next = head, head = node

3 step:         3 > 2 > 1 > null; node = 3, head = 2,    node.next = head, head = node

4 step:     4 > 3 > 2 > 1 > null; node = 4, head = 3,    node.next = head, head = node

5 step: 5 > 4 > 3 > 2 > 1 > null; node = 5, head = 4,    node.next = head, head = node
```
Комментарии представляют собой первый шаг алгоритма:
```
public Node reverseList(Node head) {
    Node focusNode = head;          // focusNode = 1
    head = null;                    // no comments...
    while (focusNode != null) {
      Node parent = focusNode;      // parent = 1
      focusNode = focusNode.next;   // focusNode = 2; moving over the list...
      parent.next = head;           // parent.next = null (1 -> null)
      head = parent;                // head = 1
    }
    return head;
}
```
