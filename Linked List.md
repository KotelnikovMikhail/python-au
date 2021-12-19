# Linked lists
 
+ [Reverse Linked List](#reverse-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Sort List](#sort-list)
 
## Reverse Linked List
 
https://leetcode.com/problems/reverse-linked-list/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest

import Linked1 as linlist

class TestReversedLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()
    def test_reverse(self):
        expected = self.get_linked_list_values(self.build_linked_list([5, 4, 3, 2, 1]))
        actual = self.get_linked_list_values(self.solution.reverseList(self.build_linked_list([1, 2, 3, 4, 5])))
        self.assertEqual(expected, actual) 
    def test_reverse_empty(self):
        expected = None
        actual = self.solution.reverseList(None)
        self.assertEqual(expected, actual)  
    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem
    def get_linked_list_values(self, head):
        result = []
        curr = head
        while curr is not None:
            result.append(curr.val)
            curr = curr.next
        return result


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution:
    def reverseList(self, head):
        prev = None
        while(head != None):
            nxt = head.next
            head.next = prev
            prev = head
            head = nxt
        return prev
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## Middle of the Linked List
 
 https://leetcode.com/problems/middle-of-the-linked-list/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest
import Linked2 as linlist

class TestMiddleLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()
    def test_middle_odd(self):
        expected = self.get_linked_list_values(self.build_linked_list([3, 4, 5]))
        actual = self.get_linked_list_values(self.solution.middleNode(self.build_linked_list([1, 2, 3, 4, 5])))
        self.assertEqual(expected, actual)

    def test_middle_even(self):
        expected = self.get_linked_list_values(self.build_linked_list([4, 5, 6]))
        actual = self.get_linked_list_values(self.solution.middleNode(self.build_linked_list([1, 2,3, 4, 5, 6])))
        self.assertEqual(expected, actual)
    def test_middle_empty(self):
        expected = None
        actual = self.solution.middleNode(None)
        self.assertEqual(expected, actual)
    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem
    def get_linked_list_values(self, head):
        result = []
        curr = head
        while curr is not None:
            result.append(curr.val)
            curr = curr.next
        return result


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution:
    def middleNode(self, head):
        mid = total = 0
        midNode = head
        while head:
            total += 1
            if total // 2 > mid:
                mid += 1
                midNode = midNode.next
            head = head.next
        return midNode

class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## Palindrome Linked List
 
https://leetcode.com/problems/palindrome-linked-list/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest
import Linked3 as linlist

class TestPalindromeLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()
    def test_palindrome_false(self):
        expected = False
        actual = self.solution.isPalindrome(self.build_linked_list([1, 2, 3, 4, 5]))
        self.assertEqual(expected, actual)
    def test_palindrome_true(self):
        expected = True
        actual = self.solution.isPalindrome(self.build_linked_list([1, 2, 3, 3, 2, 1]))
        self.assertEqual(expected, actual)
    def test_palindrome_empty(self):
        expected = True
        actual = self.solution.isPalindrome(None)
        self.assertEqual(expected, actual)
    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution(object):
    def isPalindrome(self, head):
        left=right=head
        while right and right.next:
            right = right.next.next
            left = left.next
        node = None
        while left:
            nxt = left.next
            left.next = node
            node = left
            left = nxt
        while node:
            if node.val != head.val:
                return False
            node = node.next
            head = head.next
        return True

class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## Merge Two Sorted Lists
 
https://leetcode.com/problems/merge-two-sorted-lists/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest
import Linked4 as linlist

class TestMergeTwoLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()

    def test_merge_alllarger(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3, 4, 5, 6]))
        actual = self.get_linked_list_values(self.solution.mergeTwoLists(self.build_linked_list([1, 2, 3]), self.build_linked_list([4, 5, 6])))
        self.assertEqual(expected, actual)
    def test_merge_alllesser(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3, 4, 5, 6]))
        actual = self.get_linked_list_values(self.solution.mergeTwoLists(self.build_linked_list([4, 5, 6]), self.build_linked_list([1, 2, 3])))
        self.assertEqual(expected, actual)
    def test_merge(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3, 4, 5, 6]))
        actual = self.get_linked_list_values(self.solution.mergeTwoLists(self.build_linked_list([1, 2, 6]), self.build_linked_list([3, 4, 5])))
        self.assertEqual(expected, actual)

    def test_merge_empty1(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3]))
        actual = self.get_linked_list_values(self.solution.mergeTwoLists(None, self.build_linked_list([1, 2, 3])))
        self.assertEqual(expected, actual)
    def test_merge_empty2(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3]))
        actual = self.get_linked_list_values(self.solution.mergeTwoLists(self.build_linked_list([1, 2, 3]), None))
        self.assertEqual(expected, actual)
    def test_merge_empty_both(self):
        expected = None
        actual = self.solution.mergeTwoLists(None, None)
        self.assertEqual(expected, actual)

    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem
    def get_linked_list_values(self, head):
        result = []
        curr = head
        while curr is not None:
            result.append(curr.val)
            curr = curr.next
        return result


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution:
    def mergeTwoLists(self, list1, list2):
        ptrA = list1
        ptrB = list2
        res = ListNode(0)
        head = res

        while (ptrA != None and ptrB != None):
            if (ptrA.val <= ptrB.val):
                res.next = ListNode(ptrA.val)
                res = res.next
                ptrA = ptrA.next
            else:
                res.next = ListNode(ptrB.val)
                res = res.next
                ptrB = ptrB.next
        while (ptrB):
            res.next = ListNode(ptrB.val)
            res = res.next
            ptrB = ptrB.next
        while (ptrA):
            res.next = ListNode(ptrA.val)
            res = res.next
            ptrA = ptrA.next
        return head.next

class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## Intersection of Two Linked Lists
 
https://leetcode.com/problems/intersection-of-two-linked-lists/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest
import Linked5 as linlist

class TestSortLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()

    def test_intersection(self):
        a = self.build_linked_list([7, 2, 8])
        expected = self.get_linked_list_first_node(a)
        actual = self.get_linked_list_first_node(self.solution.getIntersectionNode(self.unite_two_linked_lists(self.build_linked_list([2, 9]),a), self.unite_two_linked_lists(self.build_linked_list([6, 8, 0]),a)))
        self.assertEqual(expected, actual)

    def test_intersection_no(self):
        expected = None
        actual = self.get_linked_list_first_node(self.solution.getIntersectionNode(self.build_linked_list([2, 9, 3, 15, 7]), self.build_linked_list([6, 8, 0, 1, 2, 8])))
        self.assertEqual(expected, actual)

    def test_intersection_equal(self):
        a = self.build_linked_list([7, 2, 8])
        expected = self.get_linked_list_first_node(a)
        actual = self.get_linked_list_first_node(self.solution.getIntersectionNode(a, a))
        self.assertEqual(expected, actual)

    def test_intersection_empty(self):
        expected = None
        actual = self.solution.getIntersectionNode(None, None)
        self.assertEqual(expected, actual)

    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem
    def unite_two_linked_lists(self, headA, headB):
        cur=headA
        while cur.next:
            cur=cur.next
        cur.next=headB
        return headA
    def get_linked_list_first_node(self, head):
        if head:
            return head.val
        return None



if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class Solution:
    def getIntersectionNode(self, headA, headB):
        ptrA, ptrB = headA, headB
        if headA == None or headB == None:
            return None
        while (ptrA != ptrB):
            if ptrA == None:
                ptrA = headB
            elif ptrA != None:
                ptrA = ptrA.next
            if ptrB == None:
                ptrB = headA
            elif ptrB != None:
                ptrB = ptrB.next
        return ptrA
```

## Sort List
 
https://leetcode.com/problems/sort-list/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest
import Linked6 as linlist

class TestSortLinkedList(unittest.TestCase):
    def setUp(self):
        self.solution = linlist.Solution()

    def test_reverse(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 2, 3, 4]))
        actual = self.get_linked_list_values(self.solution.sortList(self.build_linked_list([4, 2, 3, 1])))
        self.assertEqual(expected, actual)

    def test_reverse_equal(self):
        expected = self.get_linked_list_values(self.build_linked_list([1, 1, 1, 1]))
        actual = self.get_linked_list_values(self.solution.sortList(self.build_linked_list([1, 1, 1, 1])))
        self.assertEqual(expected, actual)

    def test_reverse_empty(self):
        expected = None
        actual = self.solution.sortList(None)
        self.assertEqual(expected, actual)

    def build_linked_list(self, source):
        prev_link = None
        for i in source[::-1]:
            elem = linlist.ListNode(i, prev_link)
            prev_link = elem
        return elem
    def get_linked_list_values(self, head):
        result = []
        curr = head
        while curr is not None:
            result.append(curr.val)
            curr = curr.next
        return result


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution:

    def sortList(self, head):
        if not head:
            return None

        l = []
        while head:
            l.append(head)
            head = head.next

        l.sort(key=lambda node: node.val)
        head = run = l[0]
        for n in l[1:]:
            run.next = n
            run = run.next
        run.next = None
        return head

class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```