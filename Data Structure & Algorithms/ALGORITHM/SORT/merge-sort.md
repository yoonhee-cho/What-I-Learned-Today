# Merge Sort
- super famous algorithm, really important to understand how it works
- fundamental example of devide & conquer
```
-  0  1  2  3  4  5  6
- [8, 5, 2, 9, 5, 6, 3]
- [8, 5, 2, 9][5, 6, 3]
- [8, 5][2, 9]
- [8][5]
-       [2],[9]
_________________________________________________
- [5, 8]            ->sorted
-       [2, 9]      ->sorted
- using pointers, comparing elements
- [2, 5, 8, 9]
_________________________________________________
-              [5, 6][3]
-              [5][6][3]
-              [5, 6][3]
-              [3, 5, 6]
_________________________________________________
- [2, 3, 5, 5, 6, 8, 9]
```

## My Interpretation
- 어레이를 왼쪽, 오른쪽 반으로 갈라서, 그 어레이들이 엘리먼트가 한개만 남을 때 까지 계속 쪼개기
- 오른쪽 왼쪽 어레이의 엘리먼트 수를 담을 수 있는 비어있는 어레이 만들기
- 왼쪽어레이, 오른쪽어레이, 전체어레이의 엘리먼트를 가르키는 포인터 베리어블 만들기
- 엘리먼트가 한개만 남은 상태에서 왼쪽, 오른쪽 엘리먼트들을 비교해서 작은 순서대로 비어있는 어레이에 채워넣기
- 왼쪽 어레이의 엘리먼트가 다 채워졌는데, 아직 오른쪽 어레이에는 엘리먼트가 남아있을 경우
- 오른쪽 어레이의 엘리먼트들은 다 전체어레이로 채워졌는데, 아직 왼쪽 어레이에 엘리먼트가 남아있을 경우

## Solution
- O(n log(n)) time
- O(n log(n)) space
<!-- - O(n) space for creating copied two sub arrs, O(n) space for mergin sorted sub arrs into one arr (need to traverse all els) = O(2n) = O(n) -->

```
function mergerSort(arr){
    if(arr.length <= 1) return arr;
    const middleIdx = Math.floor(arr.length /2);
    const leftHalf = arr.slice(0, middleIdx);
    const rightHalf = arr.slice(middleIdx)l
    return mergeSortedArrs(mergeSort(leftHalf), mergeSort(rightHalf))
}

function mergeSortedArrs(leftHalf, rightHalf){
    const sortedArr = new Array(leftHalf.length + rightHalf.length);
    let sortedArrIdx = 0;
    let leftHalfIdx = 0;
    let rightHalfIdx = 0;

    while( leftHalfIdx < leftHalf.length && rightHalfIdx < rightHalf.length){
        if(leftHalf[leftHalfIdx] <=  rightHalf[rightHalfIdx]){
            sortedArr[sortedArrIdx++] = leftHalf[leftHalfIdx++]
        }
        else{
            sortedArr[sortedArrIdx++] = rightHalf[rightHalfIdx++];
        }
    }
    while(leftHalfIdx < leftHalf.length){
        sortedArr[sortedArrIdx++] = leftHalf[leftHalfIdx++]
    }
    while(rightHalfIdx < rightHalf.length){
        sortedArr[sortedArrIdx++] = rightHalf[rightHalfIdx++]
    }
    return sortedArr
}
```