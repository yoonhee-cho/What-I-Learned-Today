# Bubble Sort

- Starting from the first element in the arr, keep comparing current element with the next element(so the range of for loop can stop right before the last idx as we need to compare it with the next el). If the current el is greater than the next el, swap the order. At the end, the last element in the arr is the greatest el within the arr.
- That means the last element is sorted so, we don't need to consider the element for the next loop
- In order to run for loop without the sorted elements, we need to make a variable called sortedElIdx and set it equal to arr.length -1 (last idx of the arr) in the beginning, and decreases by 1, everytime the entire for loop iterates

## Solution 
1. Use nested for loop
- best : O(n)time - when the arr is sorted swap is not needed| O(1) space
- avg  : O(n^2)time | O(1)space
- worst: O(n^2)time | O(1)space

```
function bubbleSort(arr){
    for(let i = 0; i < arr.length; i++){
        let sortedElIdx = arr.length-1

        for(let j = 0; j < sortedElIdx; j++){
            if(arr[j] > arr[j+1]){
                let temp = arr[j+1]
                arr[j+1] = arr[j]
                arr[j] = temp
            }
        }
        sortedElIdx -= 1;
    }
return arr
}
```

2. Use while loop & for loop
- best : O(n)time - when the arr is sorted swap is not needed| O(1) space
- avg  : O(n^2)time | O(1)space
- worst: O(n^2)time | O(1)space

```
function bubbleSort(arr){
    let isSorted = false;
    let counter = 0

    while(!isSorted){
        isSorted = true
        for(let i = 0; i < arr.length -1 -counter; i++){
            if(arr[j] > arr[j+1]){
                isSorted = false
                let temp = arr[j+1]
                arr[j+1] = arr[j]
                arr[j] = temp
            }
        }
        counter += 1
    }
return arr
}
```