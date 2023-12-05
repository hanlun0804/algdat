# Table of contents
- [Sorting algorithms](#sorting-algorithms)
    - [Insertion sort](#insertion-sort)
    - [Merge](#merge)
    - [Merge-Sort](#merge-sort)
    - [Partition](#partition)
    - [Quicksort](#quicksort)
    - [Randomized partition](#randomized-partition)
    - [Randomized quicksort](#randomized-quicksort)
    - [Counting sort](#counting-sort)
    - [Radix sort](#radix-sort)
    - [Bucket sort](#bucket-sort)
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
- [Binary search](#binary-search)
    - [Iterative binary search](#iterative-binary-search)
    - [Recursive binary search](#recursive-binary-search)
- [Minimum and maximum](#minimum-and-maximum)
    - [Minimum](#minimum)
    - [Maximum](#maximum)
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

## Merge
### When to use
When you need to merge subarrays in `MERGE-SORT`
### Inputs/outputs
- Input: `A` - array to be sorted, `p` - beginning point of subarray 1, `q` - last element of subarray 1, `r` - end of subarray 2 (start is `q` + 1)

### Pseudocode/explanation
#### Pseudocode
```
MERGE(A,p,q,r)
 1 n_1 = q - p + 1
 2 n_2 = r - q
 3 let L[1,n_1+1] and R[1,n_2+1]
 4 for i = 1 to n_1
 5    L[i] = A[p+i-1]
 6 for j = 1 to n_2
 7    R[j] = A[q+j]
 8 L[n_1+1] = ∞
 9 R[n_2+1] = ∞
10 i = 1
11 j = 1
12 for k = p to r
13    if L[i] <= R[j]
14       A[k] = L[i]
15       i = i + 1
16    else A[k] = R[j]
17       j = j + 1
```
#### Explanation
- You first set $n_1$ to be the length of the subarray 1 and $n_2$ to be length of subarray 2
- Set arrays `L` and `R` to be arrays of length $n_1+1$ and $n_2+1$
- For loop from 1 to $n_1$/$n_2$ adds the element from correct position of `A` to `L` and `R`. `L` and `R` will be sorted.
- Set $\infty$ to be last element of `L` and `R`.
- Set variables `i` and `j` to be 1. These will be used to access elemenets in `L` and `R`.
- For loop from `p` (startpoint for subarray 1) to `r` (endpoint of subarray 2)
    - Checks if current element of `L`is smaller than or equal to current element of `R` (current element follows the index of what `i` or `j` is). If so, element at `A[k]` is set to be `L[i]` and 1 is added to `i`.
    - If not, element at `A[k]` is set to be `R[j]` and 1 is added to `j`.
- $\infty$ is added so all the elements of the other subarray will be chosen if one is empty already.

### Runtime
$\Theta(n)$

## Merge-Sort
### When to use
When you need to sort an array (or list) of elements in ascending order. Merge sort is particularly useful for large datasets and offers good performance with its divide-and-conquer approach.
### Input/output
- Input: A - The array to be sorted, p - Starting index of the segment of A to be sorted, r - Ending index of the segment of A to be sorted.
- Output: The array A sorted between indices p and r.
### Pseudocode/explanation
#### Pseudocode
```
MERGE-SORT(A,p,r)
1 if p < r
2   q = roundDown((q+r)/2)
3   MERGE-SORT(A,p,q)
4   MERGE-SORT(A,q+1,r)
5   MERGE(A,p,q,r)
```
#### Explanation
- Don't need to check if $p<r$. If $p<r$, subarray is 1 or smaller, which is always sorted
- Find middlepoint (rounded down), to split subarray into two new subarrays
- Run `MERGE-SORT` on both subarrays
- Use `MERGE` on array

### Runtime
$O(n \log n)$ (merge sort algorithm divides the array into halves each time (which gives the $\log n$ part) and then merges n elements at each level of recursion (which contributes the $n$ part))

### Other info
- Has space complexity $\Theta(n)$, since it splits `A` into $n$ elements

## Partition
### When to use
When implementing the quicksort algorithm, PARTITION is used to rearrange elements of an array around a pivot element.
### Inputs/outputs
- Input: A - An array, p - Starting index, r - Ending index.
- Output: The partition index, after which elements are rearranged
### Pseudocode/explanation
#### Pseudocode
```
PARTITION(A, p, r)
1 x = A[r]
2 i = p - 1
3 for j = p to r-1
4    if A[j] <= x
5       i = i + 1
6       exchange A[i] with A[j]
7 exchange A[i+1] with A[r]
8 return i + 1

```
#### Explanation
- `x` is set to be the last element that should be sorted of $A$
- `i` is set to be 1 less than the first element that should be sorted of $A$
- Runs through all elements of $A$, other than last element (pivot element)
- If element at current position is smaller or equals to pivot element, `i` is set up by 1, and the element at current position is switched with element at `A[i]`
- When all elements are iterated through, `A[i+1]` and `A[r]` is swapped
- Pivot element is returned
### Runtime
$O(n)$ (more spesifically $O(r-p+1)$)

## Quicksort
### When to use
Quicksort is a highly efficient, recursive, divide-and-conquer sorting algorithm. It's used when an average-case fast sorting algorithm is required.

### Inputs/outputs
- Input: A - An array, p - Starting index, r - Ending index.
- Output: The array A, sorted between indices p and r.

### Pseudocode/explanation
#### Pseudocode
```
QUICKSORT(A, p, r)
1 if p < r
2    q = PARTITION(A, p, r)
3    QUICKSORT(A, p, q-1)
4    QUICKSORT(A, q+1, r)
```
#### Explanation
- If `p < r` (if there is more than one element to be sorted), a pivot point `q` is found using `PARTITION`. 
- `QUICKSORT` is then ran on left and right part of pivot point

### Runtime
- Average case: $O(n\log(n))$
- Worst case: $O(n²)$

### Other info
Sorts in place

## Randomized partition
### When to use
In quicksort, when you want to improve the average-case performance and reduce the likelihood of worst-case scenarios. This function randomizes the selection of the pivot.

### Inputs/outputs
- Input: A - An array, p - Starting index, r - Ending index.
- Output: The index of the pivot after partitioning the array.

### Pseudocode/explanation
#### Pseudocode
```
RANDOMIZED-PARTITION(A, p, r)
1 i = RANDOM(p, r)
2 exchange A[r] with A[i]
3 return PARTITION(A, p, r)
```
#### Explanation
- Selects random number in the range that should be sorted, swaps that with the last element to be sorted and runs `PARTITION`

### Runtime
$O(n)$ (more spesifically $O(r-p+1)$)

## Randomized quicksort
### When to use
In scenarios where an average-case efficient sorting algorithm is required and where there is a risk of encountering worst-case scenarios with regular quicksort due to specific input patterns.
### Inputs/outputs
- Input: A - An array, p - Starting index, r - Ending index.
- Output: The array A, sorted between indices p and r.
### Pseudocode/explanation
#### Pseudocode
```
RANDOMIZED-QUICKSORT(A, p, r)
1 if p < r
2    q = RANDOMIZED-PARTITION(A, p, r)
3    RANDOMIZED-QUICKSORT(A, p, q-1)
4    RANDOMIZED-QUICKSORT(A, q+1, r)
```
#### Explanation
- Runs quicksort, but with random pivot element

### Runtime
-  $O(n \log n)$

### Other info
Sorts in place

## Counting sort
### When to use
When sorting an array of integers $A$ that are within a small range, specified by $k$. Counting sort is efficient for sorting integers that are not too spread out, as it sorts in linear time relative to the number of elements and the range of values.
### Inputs/outputs
- Input: $A$ - array to be sorted, $B$ - return array to store sorted elements, $k$ - upper bound for element in A$
- Output: The sorted array B
### Pseudocode/explanation
#### Pseudocode
```
COUNTING-SORT(A, B, k)
1 let C[0, k] be a new array
2 for i = 0 to k
3    C[i] = 0
4 for j = 1 to A.length
5    C[A[j]] = C[A[j]] + 1
6 // C[i] now contains the number of elements equal to i
7 for i = 1 to k
8    C[i] = C[i] + C[i-1]
9 // C[i] now contains the number of elements less to or equal to i
10 for j = A.length downto 1
11    B[C[A[j]]] = A[j]
12    C[A[j]] = C[A[j]] - 1
```
#### Explanation
- Line 1-3: Initializes an array C of size k+1 with all elements set to 0. This array will hold the count of each element in A.
- Line 4-5: Counts each element in A and increments the corresponding index in C.
Line 6-8: Modifies C such that each element at index i stores the number of elements less than or equal to i.
- Line 10-12: Places each element of A in its correct sorted position in array B by referring to the counts in C, then decrements the count in C for each element placed.
### Runtime
$O(k + n)$
### Other info
- Is stable
- Efficient for small set of integers

## Radix sort
### When to use
When you need to sort an array of numbers (or strings) where the elements have multiple digits or components (like dates or large numbers). Radix sort is particularly effective when the number of digits ($d$) is not large and is used for large datasets where each element has the same number of digits.
### Inputs/outputs
- Input: $A$ - array to be sorted, $d$ - number of digits in the largest number in $A$.
- Output: The sorted array A.
### Pseudocode/explanation
#### Pseudocode
```
RADIX-SORT(A, d)
1 for i = 1 to d
2    use a stable sort to sort array A on digit i
```
#### Explanation
RADIX-SORT sorts the array A by processing it digit by digit. It starts from the least significant digit (LSD) to the most significant digit (MSD). It goes through each digit and uses a stable sorting algorithm on them.
### Runtime
$\theta(d(n+k))$ if the stable sorting algorithm uses $\theta(n+k)$

## Bucket sort
### When to use
When sorting an array $A$ of uniformly distributed floating-point numbers in the range $[0,1)$. Bucket Sort is effective when the input is uniformly distributed over the range because it distributes elements into a number of buckets and then sorts these buckets individually.
### Inputs/outputs
- Input: $A$ - An array of floating-point numbers in the range $[0,1)$.
- Output: The sorted array $A$
### Pseudocode/explanation
#### Pseudocode
```
BUCKET-SORT(A)
1 let B[0, n-1] be a new array
2 n = A.length
3 for i = 0 to n-1
4    make B[i] an empty list
5 for i = 1 to n
6    insert A[i] into list B[roundDown(n*A[i])]
7 for i = 0 to n-1
8    sort list B[i] with insertion sort
9 concatenate the lists B[0], B[1],...,B[n-1] together in order
```
#### Explanation
- Line 1-4: Initialize an array B of n empty lists/buckets (n is the length of array A).

- Line 5-6: Distribute each element in A into a bucket. This is done by calculating the index of the bucket (using roundDown(n*A[i])) for each element, where each bucket corresponds to a range in the array.

- Line 7-8: Sort individual buckets. Each bucket is sorted using a stable sort, typically insertion sort, because individual buckets are expected to be small and insertion sort is efficient for small lists.

- Line 9: Concatenate all buckets in order. This forms the sorted array as elements are grouped and sorted within the correct range in their respective buckets.
### Runtime
- Average case: $O(n + k)$
- Worst case: $O(n^2)$


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

# Binary search
## Iterative Binary Search
### When to use
When you need to find the position of a specific value (`v`) in a sorted array (`A`). This iterative version is straightforward and often preferred due to its simplicity and non-use of additional stack space.

### Inputs/outputs
- Input: `A` - A sorted array, `v` - The value to search for.
- Output: The index of `v` in array `A` if found, `NIL` otherwise.

### Pseudocode/explanation
#### Pseudocode
```
BINARY-SEARCH(A, v):
1 low = 1
2 high = A.length
3 while (low <= high)
4 mid = roundDown((low + high) / 2)
5 if (A[mid] == v)
6 return mid
7 else if (A[mid] < v)
8 low = mid + 1
9 else
10 high = mid - 1
11 return NIL
```
#### Explanation
The function repeatedly divides the range of possible locations for `v` in half. If `v` is equal to the middle element (`A[mid]`), its position is returned. If `v` is larger, the search continues in the upper half. Otherwise, it continues in the lower half. The process repeats until `v` is found or the range is empty.

### Runtime
$O(\log n)$

---

## Recursive Binary Search
### When to use
When you need to perform a binary search and prefer a more elegant, though potentially less space-efficient, recursive approach.

### Inputs/outputs
- Input: `A` - A sorted array, `v` - The value to search for, `low` and `high` - The current search range within the array.
- Output: The index of `v` in array `A` if found, `NIL` otherwise.

### Pseudocode/explanation
#### Pseudocode
```
BINARY-SEARCH(A, v, low, high)
1 if (low <= high)
2 mid = roundDown((low + high) / 2)
3 if v == A[mid]
4 return mid
5 else if (A[mid] < v)
6 BINARY-SEARCH(A, v, mid + 1, high)
7 else
8 BINARY-SEARCH(A, v, low, mid - 1)
9 else return NIL
```
#### Explanation
This recursive version of binary search operates similarly to the iterative version but calls itself recursively instead of using a loop. If `v` equals `A[mid]`, the index is returned. If `v` is greater, it recursively searches the upper half; if lesser, the lower half. The recursion stops when `v` is found or the range is empty.

### Runtime
$O(\log n)$

# Minimum and maximum
## Minimum
### When to use
When you need to find the smallest (minimum) element in an array A. This function is useful in scenarios where identifying the smallest element is required, such as in selection algorithms or when preprocessing data.

### Inputs/outputs
- Input: $A$ - An array of elements
- Output: Smallest element in the  $A$

### Pseudocode/explanation
#### Pseudocode
```
MINIMUM(A)
1 min = A[1]
2 for i = 2 to A.length
3    if min > A[i]
4       min = A[i]
5 return min
```
#### Explanation
- Saves first element as current smallest
- Iterates through the rest of the elements, and if min is bigger than the current element, it gets set as min
### Runtime
 $O(n)$

## Maximum
Very similar to [minimum](#minimum)








# Template for algortihms

## Name
### When to use
### Inputs/outputs
### Pseudocode/explanation
### Runtime
### Other info

