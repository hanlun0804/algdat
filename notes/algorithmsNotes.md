# Table of contents
- [Sorting algorithms](#sorting-algorithms)
    - [Insertion sort](#insertion-sort)
- []
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

## ENQUEUE
### When to use
### Inputs/outputs
### Pseudocode/explanation
### Runtime









# Template for algortihms

## Name
### When to use
### Inputs/outputs
### Pseudocode/explanation
### Runtime
### Other info

