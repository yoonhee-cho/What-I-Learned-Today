# Min Heap(더미, 무더기) Construction

- A heap more specifically a binary heap is a data structure, resembles a binary tree.
- It is a special type of a binary tree satisfies two additional properties

1. Completeness (= all of levels have to be filled up except the last level)

2. Heap Property (where we can distinguish bt min heap & max heap
    -min heap: all parent nodes are smaller than children nodes -> the root node is always the smallest value in the heap -> MIN HEAP duhh
    -max heap: parent nodes are bigger than children nodes -> the root node is maximum value in the heap 

``` *** HEAP IS NOT SORTED 

                8
               /  \
             12    23
            / \    / \
          17  31  30  44
         /  \
       102  18
     
     0   1   2   3   4   5   6    7   8
    [8, 12, 23, 17, 31, 30, 44, 102, 18 ]

     currentNodeIdx -> i
     child One -> 2*i + 1 -> 0 + 1 = 1
     child Two -> 2*i + 2 -> 0 + 2 = 2
                             2*3+1 = 7 ?????

     parentNode -> floor((i-1)/2)
```

## Methods


1. Insert & Sift Up - continuously swap the inserted node with the parent node until it finds the correct position
 -   0   1   2   3   4   5   6   7   8
 -  [8, 12, 23, 17, 31, 30, 44, 102, 18, 9] : append 9 at the end -> find '9' parent by using fomula floor((i-1)/2) and then swap -> [8, 12, 23, 17, 9, 30, 44, 102, 18, 31]
 
2. Remove & Sift Down 
- since the heap is not sorted, the value we can extract with confidence is the root node.
- replace root node with the last leaf node
- now, the min heap property is not satisfied so we use sift down, keep swapping until it finds the correct position
- instead of comparing the node with the parent node, you have to compare the node with the two children nodes -> find the smalleset value and swap 
```
                 8                 
               /   \
             9       23
           /   \    /  \
         17    12  30  44
        / \    /
     102  18  31                    
```
- [8, 9, 23, 17, 12, 30, 44, 102, 18, 31]
- [31, 9, 23, 17, 12, 30, 44, 102, 18, 8] in place swap and then pop off 8
- [31, 9, 23, 17, 12, 30, 44, 102, 18]

- currNodeIdx = 0 / currNode first left child idx = 2 * 0 +1 = 1 / currNode's first right child idx = 2*0+2 = 2
- [9, 31, 23, 17, 12, 30, 44, 102, 18]
- i = 1 / left child = 2*1+1 = 3 / right child = 2*1+2 = 4
- [9, 12, 23, 17, 31, 30, 44, 102, 18]

3. Build Heap : build a heap out of arr that is not at all a heap, not sorted, in place using sift down method

```
                 30                 
               /    \
             102     23
           /   \    /  \
         17    18  9   44
        / \    
      12  31 

[30, 102, 23, 17, 18, 9, 44, 12, 31]                     
```
- call sift down method all the parent nodes starting from the last parent node (17)
- swap (17) & (12) 
-                ^             ^
- [30, 102, 23, 12, 18, 9, 44, 17, 31]                     

