Absolutely.
Let’s 
build Linked
Lists in C for
GATE CSE from 
absolute zero →
implementation 
→ pointers/memory → 
operations →
complexity → 
tricky GATE cases →
PYQ-style questions.
🔗 Linked List
Complete GATE 

1. understand
2. the big picture

A linked list is 
a dynamic linear 
data structure 
where elements 
are stored in 
separate memory 
locations and 
connected using pointers.

Think of a train:

[COACH 1] →
[COACH 2] → [COACH 3] → NULL

Each coach knows:

1. Its own data
2. Where the next coach is

In C:

Node
┌──────────────┬──────────────┐
│    data      │  next        │
│      10      │      ────────┼──→ next node
└──────────────┴──────────────┘

⸻

1. Why do we need
2.  Linked Lists?

Consider an array:

int a[5] =
{10,
20,30,40,50};

Memory conceptually:

1000 → 10

1004 → 

1008 →
30

1012 → 40

1016 → 50

Elements are stored contiguously.

If you want to insert 25 between 20 and 30:

10 20 30 40 50
      ↓
10 20 25 30 40 50

Array
elements
may need 
to be shifted.

Linked list 
avoids this by connecting nodes through pointers:

10 → 20 → 30 → 40 → 50

Insert 25:

10 → 20 → 25 → 30 → 40 → 50

We don’t need to physically shift all elements.

⸻

2. The Node — MOST IMPORTANT

A linked list is made from nodes.

In C:

struct Node {
    int data;
    struct Node *next;
};

Let’s break this down carefully.

struct Node

We are defining a structure called Node.

struct Node {

Inside it:

int data;

stores the actual value.

And:

struct Node *next;

stores the address of another Node.

Therefore:

struct Node
       ↓
┌───────────────┐
│ data          │
├───────────────┤
│ next          │ ──────→ another Node
└───────────────┘

⸻

3. Why is next a pointer?

Because we don’t want to store the entire next node.

We only want its address.

Suppose:

Node A is at address 1000
Node B is at address 5000

Then:

A
┌──────┬──────┐
│  10  │ 5000 │
└──────┴──────┘
          │
          ↓
        B
       5000
┌──────┬──────┐
│  20  │ 7000 │
└──────┴──────┘

So:

A->next

contains:

5000

⸻

4. head — The Gateway to the List

This is another extremely important GATE concept.

Suppose:

10 → 20 → 30 → NULL

How do we find the first node?

We maintain a pointer:

struct Node *head;

head stores the address of the first node.

head
 ↓
[10 | •] → [20 | •] → [30 | NULL]

For example:

head = 1000

means:

1000
 ↓
[10 | 2000]
       ↓
     [20 | 3000]
             ↓
           [30 | NULL]

Important distinction

head is not a node.

It is a pointer to a node.

⸻

5. Creating a Node using malloc

Usually:

struct Node *newNode;
newNode = (struct Node *)malloc(sizeof(struct Node));

The important idea:

malloc()

requests memory dynamically.

Suppose memory address 5000 is allocated:

newNode
   ↓
 5000
   ↓
┌─────────────┐
│ data        │
│ next        │
└─────────────┘

Then:

newNode->data = 10;
newNode->next = NULL;

Now:

newNode
   ↓
[10 | NULL]

⸻

6. What exactly does -> mean?

Suppose:

struct Node *p;

p is a pointer to a structure.

Then:

p->data

means:

(*p).data

These are equivalent:

p->data

and

(*p).data

But:

*p.data

is different because of operator precedence.

GATE trap ⚠️

Remember:

p->data == (*p).data

⸻

7. Creating a complete linked list

Example:

#include <stdio.h>
#include <stdlib.h>
struct Node {
    int data;
    struct Node *next;
};
int main() {
    struct Node *head;
    head = malloc(sizeof(struct Node));
    head->data = 10;
    head->next = NULL;
    return 0;
}

We have:

head
 ↓
┌───────────┐
│ 10 | NULL │
└───────────┘

⸻

8. Creating multiple nodes

struct Node *head;
struct Node *second;
struct Node *third;
head = malloc(sizeof(struct Node));
second = malloc(sizeof(struct Node));
third = malloc(sizeof(struct Node));

Now assign:

head->data = 10;
second->data = 20;
third->data = 30;
head->next = second;
second->next = third;
third->next = NULL;

Result:

head
 ↓
┌────┬──────┐
│ 10 │  •───┼────┐
└────┴──────┘    ↓
              ┌────┬──────┐
              │ 20 │  •───┼────┐
              └────┴──────┘    ↓
                           ┌────┬──────┐
                           │ 30 │ NULL │
                           └────┴──────┘

⸻

9. Traversing a Linked List

Suppose:

10 → 20 → 30 → NULL

We want to print all elements.

struct Node *temp = head;
while (temp != NULL) {
    printf("%d ", temp->data);
    temp = temp->next;
}

Output:

10 20 30

What happens internally?

Initially:

temp
 ↓
10 → 20 → 30 → NULL

After:

temp = temp->next;

we get:

        temp
         ↓
10 → 20 → 30 → NULL

Next iteration:

10 → 20 → 30 → NULL
      ↑
     temp

Then:

10 → 20 → 30 → NULL
           ↑
          temp

Then:

temp = NULL

Loop ends.

GATE formula

For a list of n nodes:

Traversal = O(n)

⸻

10. Insertion

This is one of the most important linked-list topics for GATE.

There are three common cases:

1. Insert at beginning
2. Insert at end
3. Insert after/before a particular node

⸻

11. Insert at Beginning

Original:

10 → 20 → 30 → NULL
↑
head

Want:

5 → 10 → 20 → 30 → NULL

Code:

newNode->next = head;
head = newNode;

Step 1

newNode->next = head;
newNode
   ↓
  [5] ─────→ [10] → [20] → [30]
               ↑
              head

Step 2

head = newNode;
head
 ↓
[5] → [10] → [20] → [30] → NULL

Complexity

O(1)

This is a very important GATE fact.

⸻

12. Insert at End

Suppose:

10 → 20 → 30 → NULL

To insert 40:

First reach the last node:

temp = head;
while (temp->next != NULL) {
    temp = temp->next;
}

Then:

temp->next = newNode;
newNode->next = NULL;

Result:

10 → 20 → 30 → 40 → NULL

Complexity without tail pointer

O(n)

Why?

Because we have to traverse the list.

⸻

13. Insert after a particular node

Suppose:

10 → 20 → 30 → NULL

Want 25 after 20.

Let:

temp → 20

Then:

newNode->next = temp->next;
temp->next = newNode;

First:

newNode->next = temp->next;
25 → 30

Then:

temp->next = newNode;

Result:

10 → 20 → 25 → 30 → NULL

Critical pointer-order rule ⚠️

Do not blindly reverse these statements:

temp->next = newNode;
newNode->next = temp->next;

Because after the first statement:

temp->next

is already newNode.

You can lose the connection to the old next node.

⸻

14. Deletion

Three common cases:

Beginning

10 → 20 → 30

Delete 10.

temp = head;
head = head->next;
free(temp);

Result:

20 → 30

Complexity:

O(1)

⸻

15. Delete after a particular node

Suppose:

10 → 20 → 30 → 40

Delete 30.

Let:

temp → 20

We need:

10 → 20 → 40

Code:

temp2 = temp->next;
temp->next = temp2->next;
free(temp2);

Visual:

temp
 ↓
20 → 30 → 40
     ↑
   temp2

After:

temp->next = temp2->next;

we get:

20 ─────────→ 40
30
↑
temp2

Then:

free(temp2);

⸻

16. free() — Important C concept

When we delete a node:

free(temp);

we release the dynamically allocated memory.

It is not enough to simply remove the pointer connection.

For example:

head = head->next;

removes the node from the list logically, but the old node’s allocated memory is still occupied.

That can create a memory leak.

⸻

17. Searching

struct Node *temp = head;
while (temp != NULL) {
    if (temp->data == key)
        return 1;
    temp = temp->next;
}
return 0;

Complexity:

Best case  = O(1)
Worst case = O(n)

⸻

18. Counting Nodes

int count = 0;
struct Node *temp = head;
while (temp != NULL) {
    count++;
    temp = temp->next;
}

Complexity:

O(n)

⸻

19. Reverse a Linked List ⭐⭐⭐

This is extremely important for GATE.

Original:

10 → 20 → 30 → NULL

Reverse:

30 → 20 → 10 → NULL

The standard iterative algorithm uses three pointers:

prev
curr
next

Initially:

prev = NULL
curr = head

Then:

while (curr != NULL) {
    next = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
}
head = prev;

⸻

20. Understand reversal visually

Original:

NULL
prev
curr
 ↓
10 → 20 → 30 → NULL

Step 1

Save next:

next = curr->next;
prev    curr    next
 ↓       ↓       ↓
NULL    10 →    20 → 30

Reverse link:

curr->next = prev;

Now:

NULL ← 10    20 → 30
       ↑
      curr

Move pointers:

prev = curr;
curr = next;

Now:

prev
 ↓
10    curr
       ↓
       20 → 30

Repeat.

Eventually:

prev
 ↓
30 → 20 → 10 → NULL
curr = NULL

Finally:

head = prev;

Result:

head
 ↓
30 → 20 → 10 → NULL

Complexity

Time  = O(n)
Space = O(1)

⸻

21. Types of Linked Lists

You should know these for GATE.

Singly Linked List

10 → 20 → 30 → NULL

Each node has:

data + next

⸻

Doubly Linked List

NULL ← 10 ⇄ 20 ⇄ 30 → NULL

Node:

struct Node {
    int data;
    struct Node *prev;
    struct Node *next;
};

Each node knows:

previous node
next node

Advantages:

* Can traverse forward
* Can traverse backward
* Easier deletion when node pointer is available

Disadvantage:

Extra memory for prev pointer

⸻

22. Circular Linked List

Instead of:

10 → 20 → 30 → NULL

we have:

10 → 20 → 30
↑         ↓
└─────────┘

Last node points back to first node:

last->next = head;

There is no NULL at the end.

Major GATE trap ⚠️

For circular linked lists:

while (temp != NULL)

can cause an infinite loop.

Instead, traversal often uses:

do {
    printf("%d ", temp->data);
    temp = temp->next;
} while (temp != head);

⸻

23. Circular Doubly Linked List

Combination:

10 ⇄ 20 ⇄ 30
↑           ↓
└───────────┘

Properties:

head->prev = tail
tail->next = head

⸻

24. Linked List vs Array — GATE Perspective

Property	Array	Linked List
Memory	Contiguous	Non-contiguous
Random access	O(1)	O(n)
Search	O(n)	O(n)
Insert beginning	O(n)	O(1)
Delete beginning	O(n)	O(1)
Insert after known node	O(n) generally	O(1)
Dynamic size	Limited/fixed concept	Dynamic
Extra pointer memory	No	Yes
Cache locality	Good	Usually poorer

Most important distinction:

Array:

a[i]

can directly calculate address:

base + i × sizeof(element)

Therefore:

O(1)

Linked list:

head → node1 → node2 → node3 → ...

To reach node 100:

node1
 ↓
node2
 ↓
node3
 ↓
...
 ↓
node100

Therefore:

O(n)

⸻

25. Stack using Linked List

A linked list can implement a stack.

TOP
 ↓
30
 ↓
20
 ↓
10
 ↓
NULL

Push:

new node → old top
top = new node

Therefore:

Push = O(1)
Pop  = O(1)

⸻

26. Queue using Linked List

Maintain:

front
rear
front                     rear
 ↓                          ↓
10 → 20 → 30 → NULL

Enqueue at rear:

O(1)

Dequeue from front:

O(1)

provided we maintain both pointers.

⸻

27. Important Pointer Concepts for GATE

You must be comfortable with:

struct Node *p;

This means:

p is a pointer to a Node.

Suppose:

p = head;

Then both point to the same node:

head ──┐
       ↓
      [10]
       ↑
p ─────┘

If:

p = p->next;

only p moves.

head
 ↓
10 → 20 → 30
      ↑
      p

head remains unchanged.

⸻

28. p = p->next vs p->next = ...

This is a huge GATE distinction.

Case 1

p = p->next;

You’re moving the pointer.

p
 ↓
10 → 20 → 30
after:
10 → 20 → 30
      ↑
      p

Case 2

p->next = ...

You’re modifying the linked-list connection.

Example:

p->next = NULL;

If:

10 → 20 → 30
     ↑
     p

then:

10 → 20 → NULL

The 30 node becomes disconnected.

⸻

29. Very Important GATE Pointer Question

Suppose:

struct Node *p = head;

Then:

p = p->next;

Does head change?

Answer:

No.

Because:

head → Node A
p    → Node A

After:

p = p->next;

only:

p → Node B

while:

head → Node A

remains.

⸻

30. Pointer-to-pointer — Advanced GATE

You may encounter:

struct Node **p;

This means:

p is a pointer to a pointer to a Node.

Visual:

p
 ↓
head
 ↓
Node

This becomes useful when a function needs to modify the actual head.

Example:

void insertBeginning(struct Node **head, int x)
{
    struct Node *newNode =
        malloc(sizeof(struct Node));
    newNode->data = x;
    newNode->next = *head;
    *head = newNode;
}

Call:

insertBeginning(&head, 10);

Why &head?

Because the function needs to modify the original pointer head.

⸻

31. Recursion + Linked List

GATE may combine linked lists with recursion.

Example:

void print(struct Node *p)
{
    if (p == NULL)
        return;
    print(p->next);
    printf("%d ", p->data);
}

For:

10 → 20 → 30 → NULL

Output:

30 20 10

Why?

Calls happen:

print(10)
  ↓
print(20)
  ↓
print(30)
  ↓
print(NULL)

Then recursion returns:

30
20
10

Key concept

print(p->next);
printf("%d", p->data);

means reverse order.

Whereas:

printf("%d", p->data);
print(p->next);

means forward order.

⸻

32. Time Complexity Cheat Sheet

Operation	Singly LL
Access kth element	O(n)
Search	O(n)
Insert beginning	O(1)
Delete beginning	O(1)
Insert after known node	O(1)
Delete after known node	O(1)
Insert at end, no tail	O(n)
Insert at end, tail maintained	O(1)
Reverse	O(n)
Traverse	O(n)

But remember:

O(1) insertion after a known node doesn’t mean finding that node is O(1).

If you first have to search for it:

Search = O(n)
Insertion = O(1)
Total = O(n)

⸻

33. Space Complexity

Suppose we have n nodes.

Each node stores:

data
+
pointer

Therefore auxiliary storage for the list itself is:

O(n)

For iterative reversal:

O(1) auxiliary space

For recursive reversal:

O(n) stack space

This distinction is important.

⸻

34. GATE-Level Trick: Lost Node

Consider:

p->next = p->next->next;

Suppose:

10 → 20 → 30 → 40
     ↑
     p

After:

p->next = p->next->next;

we get:

10 → 20 → 40
     ↑
     p

Node 30 is disconnected.

If it was dynamically allocated and not freed:

memory leak

⸻

35. GATE-Level Trick: free()

Suppose:

free(p);

After this, p becomes a dangling pointer if you continue using it.

Conceptually:

p
 ↓
[freed memory]

Accessing:

p->data

after free(p) gives undefined behavior.

A common safer pattern is:

free(p);
p = NULL;

⸻

36. Floyd’s Cycle Detection ⭐⭐⭐

Very important algorithm.

Suppose:

10 → 20 → 30 → 40
          ↑     ↓
          └─────┘

There is a cycle.

Use two pointers:

slow
fast

Initially:

slow = head;
fast = head;

Then:

while (fast != NULL && fast->next != NULL) {
    slow = slow->next;
    fast = fast->next->next;
    if (slow == fast)
        return 1;
}

Why does it work?

Imagine two runners on a circular track:

slow → 1 step
fast → 2 steps

Eventually the faster one catches the slower one.

Complexity:

Time  = O(n)
Space = O(1)

⸻

37. Finding Middle Node

Another classic.

Use:

slow = head;
fast = head;

Then:

while (fast != NULL && fast->next != NULL) {
    slow = slow->next;
    fast = fast->next->next;
}

When fast reaches the end:

slow
 ↓
middle

For:

10 → 20 → 30 → 40 → 50

slow ends at:

30

Complexity:

O(n)

Space:

O(1)

⸻

38. Nth Node from End

Another important pattern.

Use two pointers:

first
second

Move first ahead by n nodes.

Then move both together.

When:

first = NULL

second points to the nth node from the end.

Example:

10 → 20 → 30 → 40 → 50

Find 2nd from end:

40

⸻

39. GATE Mental Model

Whenever you see linked-list code, don’t immediately calculate complexity.

First draw the nodes.

For example:

p = p->next->next;

Draw:

p
↓
10 → 20 → 30 → 40

After:

10 → 20 → 30 → 40
          ↑
          p

Then calculate what happened.

This single habit will solve many GATE linked-list questions.

⸻

40. Your GATE Linked List Mastery Checklist

You should master these in this order:

Level 1 — Fundamentals

* [ ]	Structure
* [ ]	Node
* [ ]	Pointer
* [ ]	head
* [ ]	NULL
* [ ]	malloc
* [ ]	free
* [ ]	->
* [ ]	(*p).data

Level 2 — Basic operations

* [ ]	Traversal
* [ ]	Searching
* [ ]	Counting
* [ ]	Insert beginning
* [ ]	Insert end
* [ ]	Insert middle
* [ ]	Delete beginning
* [ ]	Delete end
* [ ]	Delete middle

Level 3 — Types

* [ ]	Singly linked list
* [ ]	Doubly linked list
* [ ]	Circular linked list
* [ ]	Circular doubly linked list

Level 4 — Algorithms

* [ ]	Reverse
* [ ]	Find middle
* [ ]	Detect cycle
* [ ]	Remove cycle
* [ ]	Nth node from end
* [ ]	Merge two sorted lists
* [ ]	Remove duplicates
* [ ]	Palindrome linked list

Level 5 — GATE traps

* [ ]	Pointer movement
* [ ]	Pointer modification
* [ ]	Aliasing
* [ ]	p->next
* [ ]	p->next->next
* [ ]	p = p->next
* [ ]	free()
* [ ]	Dangling pointer
* [ ]	Memory leak
* [ ]	Recursion
* [ ]	Pointer-to-pointer
* [ ]	Complexity analysis

⸻

🧠 The 10 things you MUST remember for GATE

1. head = pointer to first node
2. next = address of next node
3. last node's next = NULL
   (except circular lists)
4. Linked list does NOT provide O(1) random access
5. Insert at beginning = O(1)
6. Delete at beginning = O(1)
7. Insert after a KNOWN node = O(1)
8. Traversal/search = O(n)
9. Reverse iterative = O(n) time, O(1) auxiliary space
10. slow + fast pointers solve many linked-list problems

⸻

🎯 GATE PYQ-style practice

Try these without looking at the answers.

Q1

Given:

head → 10 → 20 → 30 → NULL

What is the value of p->data?

struct Node *p = head;
p = p->next;
p = p->next;

⸻

Q2

Given:

10 → 20 → 30 → 40 → NULL

What does this do?

p = head;
p->next = p->next->next;

Draw the resulting list.

⸻

Q3

What is the complexity?

p = head;
while(p != NULL) {
    printf("%d", p->data);
    p = p->next;
}

⸻

Q4

What is the output?

void f(struct Node *p)
{
    if(p == NULL)
        return;
    printf("%d ", p->data);
    f(p->next);
}

For:

10 → 20 → 30 → NULL

⸻

Q5 ⭐

What is the output?

void f(struct Node *p)
{
    if(p == NULL)
        return;
    f(p->next);
    printf("%d ", p->data);
}

⸻

Q6 ⭐

For a singly linked list with n nodes, what is the time complexity of finding the k-th node from the beginning?

⸻

Q7 ⭐⭐

For:

10 → 20 → 30 → 40 → 50

using:

slow = head;
fast = head;
while(fast != NULL && fast->next != NULL)
{
    slow = slow->next;
    fast = fast->next->next;
}

Which node does slow point to when the loop terminates?

⸻

Q8 ⭐⭐⭐

What is the time and auxiliary-space complexity of iterative linked-list reversal?

⸻

Q9 ⭐⭐⭐

Why does this code potentially create an infinite loop for a circular linked list?

while(p != NULL)
{
    p = p->next;
}

⸻

Q10 — Pointer trap

Suppose:

head → A → B → C → NULL

and:

p = head;
p = p->next;

Does head now point to B?

Explain why.

⸻

🔥 Recommended GATE study sequence

Don’t try to memorize all linked-list algorithms at once. Use:

STRUCT
  ↓
NODE
  ↓
POINTER
  ↓
HEAD
  ↓
malloc/free
  ↓
TRAVERSAL
  ↓
INSERTION
  ↓
DELETION
  ↓
DOUBLY/CIRCULAR
  ↓
REVERSE
  ↓
SLOW/FAST POINTER
  ↓
RECURSION
  ↓
POINTER TRACING
  ↓
GATE PYQs

Most important: for GATE, linked lists are less about writing a huge program and more about being able to trace pointer changes exactly. Draw the nodes and arrows whenever you encounter unfamiliar C code.
