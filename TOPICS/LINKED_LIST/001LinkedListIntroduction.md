### LINKED LIST - 
```bash
> a linear data structure in computer science where elements are not stored in contiguous (adjacent) memory locations
```

### Suppose you have 5 number 10 20 30 40 50
> In  an ARRAY
> Address looks like this -> 
> Address: 100  104  108  112  116
         ↓    ↓    ↓    ↓    ↓
        10   20   30   40   50

> The elements are stored contiguously.
> Accesing element like A[3] is 40 easy and fast.

> but imagine if you have to insert 25 between 20 and 30.
> 10   20   25  30   40   50

> it will take much time because of the shifting process
> 30 -> 40 -> 50 

O(N) work!


### 1. The Linked List Idea

> Instead of forcing elements to sit next to each other in memory, we store each element in a separate node.

[DATA | ADDRESS] ------> [DATA | ADDRESS] -------> [DATA | ADDRES] ------> [DATA | ADDRESS]

[10 | 1001 ] ------> [20 | 1002 ] -------> [30 | 10003 ] ------> [40 | NULL]

SINGLY LINKED LIST

-------------------------------------------

SYNTAX

struct Node {
    int data;
    struct Node* next;
};


Node
 ├── data
 └── next

next is a pointer.

It stores the address of another node.


--------------------------------

so we need some way to find where is the first node.

struct Node* head;



