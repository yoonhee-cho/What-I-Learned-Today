# Insertion Sort

- Assume that first el in the arr is sorted arr's element
- Start comparing the second el with the first el
- If the first el is greater than the second el (not sorted) then, swap the order
- so the first and secon el are now sorted
- compare third el with the second el and if the second el is greater than third el, swap the order. while index > 0 and not sorted, keep swap.
- move on the fourth el do the samething

- the reason why name of the insertion sort is insertion sort is that while comparing the elements, it INSERTs the el to compare in the sorted el and if the order is not sorted, swap keeps happening until it is sorted.

## Solution 
- best : O(n)time - when the arr is sorted swap is not needed| O(1) space
- avg  : O(n^2)time | O(1)space
- worst: O(n^2)time | O(1)space
```
function insertionSort(arr){
    for(let i = 1; i < arr.lengthl i++){
        let j = i
        while( 0 < j && arr[j-1] > arr[j] ){
            let temp = arr[j]
            arr[j] = arr[j-1]
            arr[j-1] = temp
            j -= 1
        }
    }
    return arr
}
```
   <!-- not sorted arr's els
   -----
[6,3,2,1]
 -
 consider 6 is sorted arr's el

compare 6 & 3 -> 6 is greater than 3 -> swap! ->
[3,6,2,1] j is now 0 (out of while loop)

     not sorted arr's els
     ---
[3,6,2,1]
 ---
 sorted arr's els

 compare 6 & 2 -> 6 is greater than 2 -> swap! 
[3,2,6,1]-> j is now 1 -> 3 is greater than 2 -> swap! 
[2,3,6,1]-> j is now 0 (out of while loop)

        not sorted arr's els
        -
 [2,3,6,1]
  -----
  sorted arr's els

 compare 6 & 1 -> 6 is greater than 1 -> swap! 
[2,3,1,6]-> j is now 2 -> 3 is greater than 1 -> swap! 
[2,1,3,6]-> j is now 1 -> 2 is greater than 1 -> swap!
[1,2,3,6]-> j is now 0 (out of while loop) -->