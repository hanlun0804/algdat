# Table of contents
- [Sorting algorithms](#sorting-algorithms)
    - [Insertion sort](#insertion-sort)
- [Stack functions](#stack-functions)
    - [STACK-EMPTY](#stack-empty)    
    - [PUSH](#push)    
    - [POP](#pop)
- [Queue functions](#queue-functions)
    - [ENQUEUE](#enqueue)
    - [DEQUEUE](#dequeue)
- [List functions](#list-functions)
    - [LIST-SEARCH](#list-search)
    - [LIST-INSERT](#list-insert)
- [Hash functions](#hash-functions)
    - [HASH-INSERT](#hash-insert)
    - [HASH-SEARCH](#hash-search)
    - [CHAINED-HASH-INSERT](#chained-hash-insert)
    - [CHAINED-HASH-SEARCH](#chained-hash-search)
    - [CHAINED-HASH-DELETE](#chained-hash-delete)
- [Direct access table functions](#direct-access-table-functions)
    - [DIRECT-ADDRESS-SEARCH](#direct-address-search)
    - [DIRECT-ADDRESS-INSERT](#direct-address-insert)
    - [DIRECT-ADDRESS-DELETE](#direct-address-delete)
- [Template for algorithms](#template-for-algortihms)

# Sorting algorithms

## Insertion sort
### When to use
- Small datasets
- Datasets that are almost sorted
### Inputs/outputs
- Inputs:
    - Array to be sorted
    - Size of array (optional, can use .size/.length)
- Outputs:
    - Sorted array
### Pseudocode/explanation

#### Pseudocode
```
INSERTION-SORT(A)
1 for j = 2 to A.length
2     key = A[j]
3     // Insert A[j] into the sorted sequence A[1..j-1]
4     i = j-1
5     while i > 0 and A[i] > key
6         A[i+1] = A[i]
7         i = i-1
8         A[i+1] = key
```

#### Explination
- The classic card analogy: 
    - You have 5 cards in your right hand. You take the leftmost card, and put it in your left hand. This will always be sorted, so you don't worry about that. 
    - Then you pick the next leftmost card (index 2 in an array) and you place that in the correctly sorted place in your left hand. Now you have two sorted cards in your left hand. 
    - You repeat this for all 5 cards, and you will have a sorted deck in your left hand.
- Technical explination: 
    - You iterate through each card in the deck, from the second card.  This is because the first card is always sorted by default, as it's a single-element 'subarray'. You then set the key to be the current card, and also save the index of the previous card. 
    - You then go through all the cards you have already sorted, and check if the index of the previous card (i) is greater than or equal to 0, ensuring you don't go out of the array bounds. Also, you check if the previous card is greater than the key (the current card). If these conditions are met, you set the card at i+1 to be the card at i (effectively shifting it "to the right" in the deck). You then decrement i to move one position "to the left" in the deck. This process continues until you find the correct position for the key. Finally, you set the card at i+1 (the correct sorted position) to be key, effectively placing the current card in its correct position in the sorted subarray.

### Runtime
- Best case: $\Theta(n)$
- Average case: $\Theta(n²)$
- Worst case: $\Theta(n²)$

### Other info
Insertion sort sorts in place. Space complexity is therefore $\Theta(1)$.

# Stack functions

## STACK-EMPTY
### When to use
Use when you want to check if stack is empty.
### Inputs/outputs
- Input: Stack to check
- Output: True/false, depening on if it is empty or not
### Pseudocode/explanation

#### Pseudocode
```
STACK-EMPTY(S)
1 if S.top == 0
2   return TRUE
3 else return FALSE
```

#### Explanation
Check if stack is empty by checking if the top of the stack (like a stack of plates), is in position 0. Returns true if this is the case, if not, it returns false

### Runtime
$O(1)$

## PUSH
### When to use
When you want to add item to top of stack
### Inputs/outputs
- Input: `S` - stack, `x` - element to add

### Pseudocode/explanation

#### Pseudocode
```
PUSH(S,x)
1 S.top = S.top + 1
2 S[S.top] = x
```

#### Explanation
Sets `S.top` to be one higher than it is. Adds element `x` to index of `S.top`

### Runtime
$O(1)$

## POP
### When to use
When you want to remove the top item of stack
### Inputs/outputs
- Input: `S` - stack

### Pseudocode/explanation

#### Pseudocode
```
POP(S)
1 if STACK-EMPTY(S)
2   error "underflow"
3 else S.top = S.top - 1
4   return S[S.top + 1]
```

#### Explanation
Checks if stack is empty, throws error. If not, it sets `S.top` to be one less than it currently is, and returns the item on `S[S.top + 1]`. First remove 1 from `S.top`and add one in the return statement because we need it to be one less, and this can't be done after the return statement.

### Runtime
$O(1)$

# Queue functions

## ENQUEUE
### When to use
When you want to add an element to the end of a queue
### Inputs/outputs
- Input: `Q` - queue, `x` - element to add to queue
### Pseudocode/explanation
#### Pseudocode
```
ENQUEUE(Q,x):
1 Q[Q.tail] = x
2 if Q.tail == Q.length
3   Q.tail = 1
4 else Q.tail = Q.tail + 1
```

#### Explanation
- Set `x` to be the last element of `Q` with `Q[Q.tail]`. Check if the tail is currently the end of the array, then set the tail to be 1, as queues uses wraparound. If tail is not at end of array, we add 1 to the tail.
### Runtime
$O(1)$

## DEQUEUE
### When to use
When you want to remove the first element of a queue.
### Inputs/outputs
- Input: `Q` - queue to remove elemnt from
### Pseudocode/explanation
#### Pseudocode
```
DEQUEUE(Q):
1 x = Q[Q.head]
2 if Q.head == Q.length
3   Q.head = 1
4 else Q.head = Q.head + 1
5 return x
```
#### Explanation
Set `x` to be the head of the queue. Checks if this is the last element of the array. If it is, `Q.head` is set to 1, as queues use wraparound. If not, 1 is added to head. Return element we have removed.
### Runtime
$O(1)$


# List functions

## LIST-SEARCH
### When to use
When you want to search for an item (its key value) in a linked list
### Inputs/outputs
- Inputs: `L` - list to search through, `k` - key you want to search for
- Output: Pointer to `k`
### Pseudocode/explanation
#### Pseudocode
```
LIST-SEARCH(L,k)
1 x = L.head
2 while x ≠ NIL and x.key ≠ k
3   x = x.next
4 return x
```
#### Explanation
`L.head` is saved in `x`. Checks that `x` isn't NIL (end of list) or that `x.key` isn't `k` (then we found `k`). Returns `x`. 

### Runtime
$O(1)$



## LIST-INSERT
### When to use
When you want to insert an item at the front of a linked list
### Inputs/outputs
- Input: `L` - List you want to insert item to, `x` - pointer to element we want to insert
### Pseudocode/explanation
#### Pseudocode
```
LIST-INSERT(L,x)
1 x.next = L.head
2 if L.head ≠ NIL
3   L.head.prev = x
4 L.head = x
5 x.prev = NIL
```
#### Explanation
`x.next` is set to `L.head`. This makes sure `x` points to the previously first element. If `L.head` isn't NIL, `L.head.prev` is set to `x`. If `L.head` is NIL, `L` is empty. `L.head` is then set to `x`, and `x.prev` is set to NIL.
### Runtime
$O(1)$

# Hash functions

## HASH-INSERT
### When to use
When inserting a key into a hash table using open addressing and linear probing.

### Inputs/outputs
- Input: `T` - Hash table, `k` - Key to be inserted.
- Output: The index `j` where `k` was inserted.

### Pseudocode/explanation
#### Pseudocode
```
HASH-INSERT(T,k)
1 i = 0
2 repeat
3   j = h(k,i)
4   if T[j] == NIL
5       T[j] = k
6       return j
7   else i = i + 1
8 until i == m 
9 error "hash table overflow"
```
### Runtime
- Average case: $O(1)$
- Worst case: $O(m)$

## HASH-SEARCH
### When to use
When searching for a key in a hash table that uses open addressing.
### Inputs/outputs
- Input: `T` - Hash table, `k` - Key to search for.
- Output: Index of the key if found, NIL otherwise.
### Pseudocode/explanation
#### Pseudocode
```
HASH-SEARCH(T,k)
1 i = 0
2 repeat
3   j = h(k,i)
4   if T[j] == k 
5       return j
6   i = i + 1
7 until T[j] == NIL or i == m
8 return NIL
```
#### Explanation
The function searches for key `k` using the hash function `h(k,i)` and linear probing. If `k` is found at `T[j]`, its index is returned. If a NIL slot is encountered or after `m` attempts without finding `k`, the search returns NIL.
### Runtime
- Average case: $O(1)$
- Worst case: $O(m)$

## CHAINED-HASH-INSERT
### When to use
When inserting an element into a hash table that uses chaining to resolve collisions.
### Inputs/outputs
- Input: T - Hash table, x - Element to be inserted.
### Pseudocode/explanation
#### Pseudocode
```
CHAINED-HASH-INSERT(T,x)
1 insert x at the head of list T[h(x.key)]
```
#### Explanation
This function inserts the element x at the head of the linked list at the index determined by hashing x.key. It's used when collisions in the hash table are resolved by chaining.
### Runtime
- Average case: $O(1)$
- Worst case: $O(n)$



## CHAINED-HASH-SEARCH
### When to use
When searching for an element with a specific key in a hash table using chaining.
### Inputs/outputs
- Input: `T` - Hash table, `k` - Key of the element to search for.
- Output: The element with key `k` if found, NIL otherwise.
### Pseudocode/explanation
#### Pseudocode
```
CHAINED-HASH-SEARCH(T,k)
1 search for an element with key k in list T[h(k)]
```
#### Explanation
Searches for an element with key k in the linked list at the index determined by hashing k. It's suitable for hash tables that use chaining to resolve collisions.
### Runtime
- Average case: $O(1)$
- Worst case: $O(n)$


## CHAINED-HASH-DELETE
### When to use
When you need to delete an element from a hash table that uses chaining for collision resolution.
### Inputs/outputs
- Input: `T` - Hash table, `x` - Element to be deleted.
### Pseudocode/explanation
#### Pseudocode
```
CHAINED-HASH-DELETE(T.x)
1 delete x from the list T[h(x.key)]
```
#### Explanation
Removes the element `x` from the linked list at the index determined by hashing `x.key`. This function is used in hash tables with chaining.
### Runtime
- Average case: $O(1)$
- Worst case: $O(n)$






# Direct access table functions

## DIRECT-ADDRESS-SEARCH
### When to use
When you need to retrieve an element from a direct address table using its key.

### Inputs/outputs
- Input: `T` - Direct address table, `k` - Key of the element to retrieve.
- Output: The element with key `k` if it exists in the table, `NIL` otherwise.

### Pseudocode/explanation
#### Pseudocode
```
DIRECT-ADDRESS-SEARCH(T,k)
1 return T[k]
```
#### Explanation
This function simply returns the element at the slot in the table `T` that corresponds to the key `k`. It's a straightforward lookup operation.

### Runtime
$O(1)$


## DIRECT-ADDRESS-INSERT
### When to use
When you need to insert an element into a direct address table.

### Inputs/outputs
- Input: `T` - Direct address table, `x` - Element to be inserted.
- Output: None (element `x` is inserted in the table `T`).

### Pseudocode/explanation
#### Pseudocode

```
DIRECT-ADDRESS-INSERT(T,x)
1 T[x.key] = x
```
#### Explanation
This function places the element `x` into the slot in table `T` that corresponds to `x.key`. It's a direct mapping from the key to the slot in the table.

### Runtime
$O(1)$

## DIRECT-ADDRESS-DELETE
### When to use
When you need to delete an element from a direct address table, where each possible key has a dedicated slot.
### Inputs/outputs
- Input: T - Direct address table, x - Element to be deleted.
- Output: Modified table with the element removed.
### Pseudocode/explanation
#### Pseudocode
```
DIRECT-ADDRESS-DELETE(T,x)
1 T[x.key] = NIL
```
#### Explanation
Searches for an element with key k in the linked list at the index determined by hashing k. It's suitable for hash tables that use chaining to resolve collisions.
### Runtime
- Average case: $O(1)$
- Worst case: $O(n)$













# Template for algortihms

## Name
### When to use
### Inputs/outputs
### Pseudocode/explanation
### Runtime
### Other info

