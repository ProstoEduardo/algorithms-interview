# Linked lists
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Reverse Linked List](#reverse-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Sort List](#sort-list)

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


## Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

Example 1:

```
Input: 1->2
Output: false

```

Example 2:


```
Input: 1->2->2->1
Output: true

```

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
 
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null)
            return true;
        
        //Step 1: Bisect at mid
        ListNode head2 = bisect(head);
        
        //Step 2: Reverse second head
        head2 = reverse(head2);
        
        //Step 3: Check for equality
        return isEqual(head, head2);
    }
    
    private boolean isEqual(ListNode head, ListNode head2) {
        while (head != null) {
            if (head.val != head2.val)
                return false;
            head = head.next;
            head2 = head2.next;
        }
        return true;
    }
    
    private ListNode bisect(ListNode head) {
        ListNode fast = head, slow = head, prev = null;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;
        return slow;
    }
    
    private ListNode reverse(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode root = head;
        while (head != null && head.next != null) {
            ListNode next = head.next, nextNext = next.next;
            next.next = root;
            head.next = nextNext;
            root = next;
        }
        return root;
    }
}
```
## Sort List
https://leetcode.com/problems/sort-list/
Sort a linked list in O(n log n) time using constant space complexity.

Example 1:
```
Input: 4->2->1->3
Output: 1->2->3->4
```
Example 2:
```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
	public ListNode sortList(ListNode head) {
		if (head == null || head.next == null) return head;
		ListNode fast = head.next.next;
		ListNode slow = head;
		while (fast != null && fast.next != null) {
			fast = fast.next.next;
			slow = slow.next;
		}

		ListNode l1 = sortList(slow.next);
		slow.next = null;
		ListNode l2 = sortList(head);
		return merge(l1, l2);
	}

	public ListNode merge(ListNode l1, ListNode l2) {
		ListNode dummy = new ListNode(-1);
		ListNode cur = dummy;

		while (l1 != null && l2 != null) {
			if (l1.val < l2.val) {
				cur.next = l1;
				l1 = l1.next;
			}
			else {
				cur.next = l2;
				l2 = l2.next;
			}
			cur = cur.next;
		}
		cur.next = (l1 == null) ? l2 : l1; 

		return dummy.next;
	}
}
```
