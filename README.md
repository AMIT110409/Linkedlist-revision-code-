# Linkedlist-revision-code-
linked_list  key question 


Here's a concise Linked List revision sheet covering the key concepts, types, and commonly asked problems:

1. Key Concepts
Linked List: A data structure where each element (node) contains a value and a reference (or pointer) to the next node in the list.

Node Structure:
python

class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
Head: The starting node of the linked list.

Null Reference: The last node’s next points to None, indicating the end of the list.

2. Types of Linked Lists
Singly Linked List: Nodes have a single pointer to the next node.

Doubly Linked List: Nodes have two pointers—one pointing to the next node and another pointing to the previous node.

Circular Linked List: The last node points back to the head, creating a circular structure.

3. Basic Operations
Insertion:

Insert at the beginning:
python

def insert_at_beginning(head, value):
    new_node = Node(value)
    new_node.next = head
    return new_node  # New head
Insert at the end:
python

def insert_at_end(head, value):
    new_node = Node(value)
    if not head:
        return new_node
    temp = head
    while temp.next:
        temp = temp.next
    temp.next = new_node
    return head
    
Deletion:

Delete a node by value:
python

def delete_node(head, value):
    if head and head.value == value:
        return head.next  # New head
    temp = head
    while temp and temp.next:
        if temp.next.value == value:
            temp.next = temp.next.next
            break
        temp = temp.next
    return head
    
Traversal:

Print all nodes:
python

def print_list(head):
    while head:
        print(head.value, end=" -> ")
        head = head.next
    print("None")
4. Important Problems
1. Reverse a Linked List
Iterative Approach:

python
def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev  # New head
Recursive Approach:

python

def reverse_list_recursive(head):
    if not head or not head.next:
        return head
    rest = reverse_list_recursive(head.next)
    head.next.next = head
    head.next = None
    return rest
    
2. Detect Cycle in a Linked List (Floyd’s Cycle Detection Algorithm)
python


def has_cycle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True  # Cycle found
    return False
    
3. Merge Two Sorted Linked Lists
python

def merge_sorted_lists(l1, l2):
    dummy = Node(-1)
    current = dummy
    while l1 and l2:
        if l1.value < l2.value:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    current.next = l1 or l2
    return dummy.next
    
4. Find Middle of a Linked List
Using Two Pointers:
python


def find_middle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow  # Middle node
5. Remove N-th Node from End
python


def remove_nth_from_end(head, n):
    dummy = Node(0)
    dummy.next = head
    slow, fast = dummy, dummy
    for _ in range(n + 1):
        fast = fast.next
    while fast:
        slow = slow.next
        fast = fast.next
    slow.next = slow.next.next
    return dummy.next
    
6. Intersection of Two Linked Lists
Two Pointer Approach:
python

def get_intersection_node(headA, headB):
    if not headA or not headB:
        return None
    a, b = headA, headB
    while a != b:
        a = a.next if a else headB
        b = b.next if b else headA
    return a  # Intersection node or None
5. Advanced Problems
1. Flatten a Multilevel Doubly Linked List
python
Copy code
def flatten(head):
    if not head:
        return head
    stack = []
    current = head
    while current:
        if current.child:
            if current.next:
                stack.append(current.next)
            current.next = current.child
            current.child.prev = current
            current.child = None
        if not current.next and stack:
            next_node = stack.pop()
            current.next = next_node
            next_node.prev = current
        current = current.next
    return head
2. Add Two Numbers (Linked Lists)
python


def add_two_numbers(l1, l2):
    dummy = Node(0)
    current = dummy
    carry = 0
    while l1 or l2 or carry:
        v1 = l1.val if l1 else 0
        v2 = l2.val if l2 else 0
        sum_val = v1 + v2 + carry
        carry = sum_val // 10
        current.next = Node(sum_val % 10)
        current = current.next
        if l1:
            l1 = l1.next
        if l2:
            l2 = l2.next
    return dummy.next
    
6. Complexity Analysis
Time Complexity:

Insertion/Deletion at head: O(1)
Insertion/Deletion at tail: O(N)
Traversal/Search: O(N)
Reverse Linked List: O(N)
Merge Two Linked Lists: O(N)
Space Complexity:

Iterative solutions: O(1)
Recursive solutions: O(N) (due to call stack)
