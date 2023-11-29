# Table of contents
- [Sorting algorithms](#sorting-algorithms)
    - [Insertion sort](#insertion-sort)
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
Insertion sort sorts in place. Space complexity is therefroe $\Theta(1)$.


# Template for algortihms

## Name
### When to use
### Inputs/outputs
### Pseudocode/explanation
### Runtime
### Other info
