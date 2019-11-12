# Linked lists
+ [Design Linked List](#design-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Reverse Linked List](#reverse-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Sort List](#sort-list)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Reorder List](#reorder-list)


## Design Linked List

https://leetcode.com/problems/design-linked-list/

Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

* get(index) : Get the value of the index-th node in the linked list. If the index is invalid, return -1.
* addAtHead(val) : Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
* addAtTail(val) : Append a node of value val to the last element of the linked list.
* addAtIndex(index, val) : Add a node of value val before the index-th node in the linked list. If index equals to the length of linked * list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
* deleteAtIndex(index) : Delete the index-th node in the linked list, if the index is valid.
 

Example:

```
Input: 
["MyLinkedList","addAtHead","addAtTail","addAtIndex","get","deleteAtIndex","get"]
[[],[1],[3],[1,2],[1],[1],[1]]
Output:  
[null,null,null,null,2,null,3]

Explanation:
MyLinkedList linkedList = new MyLinkedList(); // Initialize empty LinkedList
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);  // linked list becomes 1->2->3
linkedList.get(1);            // returns 2
linkedList.deleteAtIndex(1);  // now the linked list is 1->3
linkedList.get(1);            // returns 3
```

```java
class MyLinkedList {

    class ListNode {
        ListNode next;
        int val;

        public ListNode(int x) {
            val = x;
        }
    }
    public int size = 0;
    public ListNode head = null;

    /**
     * Initialize your data structure here.
     */
    public MyLinkedList() {
    }

    /**
     * Get the value of the index-th node in the linked list. If the index is invalid, return -1.
     */
    public int get(int index) {
        int count = 0;
        ListNode currentNode = head;
        while (currentNode != null) {
            if (index == count) {
                return currentNode.val;
            }
            currentNode = currentNode.next;
            count++;
        }
        return -1;
    }

    /**
     * Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
     */
    public void addAtHead(int val) {
        ListNode newNode = new ListNode(val);
        newNode.next = head;
        head = newNode;
        size++;
    }

    /**
     * Append a node of value val to the last element of the linked list.
     */
    public void addAtTail(int val) {
        if (head == null) {
            addAtHead(val);
            return;
        }
        ListNode currentNode = head;
        ListNode newNode = new ListNode(val);
        newNode.next = null;
        while (currentNode.next != null) {
            currentNode = currentNode.next;
        }
        currentNode.next = newNode;
        size++;
    }

    /**
     * Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
     */
    public void addAtIndex(int index, int val) {
        if (index <= 0) {
            addAtHead(val);
            return;
        } else if (index == size) {
            addAtTail(val);
            return;
        }
        int count = 1;
        ListNode currentNode = head;

        while (currentNode != null) {
            if (count == index) {
                ListNode newNode = new ListNode(val);
                newNode.next = currentNode.next;
                currentNode.next = newNode;
                size++;
                return;
            }
            currentNode = currentNode.next;
            count++;
        }
    }

    /**
     * Delete the index-th node in the linked list, if the index is valid.
     */
    public void deleteAtIndex(int index) {
        if (head == null) {
            return;
        }

        if (index == 0) {
            head = head.next;
            size--;
            return;
        }

        ListNode currentNode = head;
        int count = 1;

        while (currentNode.next != null) {
            if (count == index) {
                currentNode.next = currentNode.next.next;
                size--;
                return;
            }

            currentNode = currentNode.next;
            count++;
        }
    }
}
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

Example 1:
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```
Example 2:
```
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
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
    public ListNode middleNode(ListNode head) {
        ListNode newNode = head;
        ListNode node = head;
        while (node != null && node.next != null) {
            newNode = newNode.next;
            node = node.next.next;
        }
        return newNode;
    }
}
```
## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

Given a linked list, remove the n-th node from the end of list and return its head.

Example:
```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode node = new ListNode(0);
        node.next = head;
        ListNode first = node;
        ListNode second = node;
        for (int i = 1; i <= n + 1; i++) {
            first = first.next;

        }
        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        return node.next;
    }
}
```
### Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

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
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                node.next = l1;
                l1 = l1.next;
            } else {
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

https://leetcode.com/problems/reverse-linked-list/

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

https://leetcode.com/problems/palindrome-linked-list/

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
            } else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        if (l1 != null) {
            cur.next = l1;
        }
        if (l2 != null) {
            cur.next = l2;
        }
        return dummy.next;
    }
}
```

## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

Write a program to find the node at which the intersection of two singly linked lists begins.

Example 1:
```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

Example 2:
```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
 ```

Example 3:

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
 ```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        
        ListNode a = headA; 
        ListNode b = headB;
        while(a != b) {
            if(a == null){
                a = headB;
            }
            else { 
	    	a = a.next;
	    }
            if(b == null){
                b = headA;
            }
            else { 
	    b = b.next;
	    }  
        }
        return a;
    }
}
```

## Reorder List

https://leetcode.com/problems/reorder-list/

Given a singly linked list L: L0→L1→…→Ln-1→Ln,

reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
Example 2:
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```

```java
class Solution {
    public void reorderList(ListNode head) {
        while (head != null) {
           head.next = reverseList(head.next);
           head = head.next;
        }
    }
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
}
```
