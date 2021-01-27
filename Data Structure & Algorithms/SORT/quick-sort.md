# Quick Sort
- pivot 값 (중심축)이 항상 어레이의 앞에 두고
- 왼쪽 인덱스가 오른쪽 인덱스랑 같거나 작을동안만 (크면 멈춤 =넘어가면)
-   pivot 값보다 작은쪽이 왼쪽, 큰쪽이 오른쪽에 있어야 함 -> 제대로 배치되어있으면 그냥 다음 엘리먼트로 옮겨주기
-   pivot 값보다 큰데 왼쪽에 있고, pivot 값보다 작은데 오른쪽에 있으면 스왑!
- while loop을 빠져나왔다는 것은, 오른쪽 인덱스는 바꿔야되는데 왼쪽인덱스가 가르키는 엘리먼트가 pivot 값보다 계속 작으니까 인덱스가 계속 증가해서 끝나버린 상황 ----> 어째튼 오른쪽인덱스 엘리먼트값이 pivot값보다는 원래 커야되는데 작은 상황이니까, pivot값하고 오른쪽 인덱스값 스왑
- recursion을 이용하기 때문에, space complexity를 줄여주기 위해서, 어레이가 작은 것부터 재귀함수로 호출해주기.

## Solution
- best  : O(n log (n)) time | O(log(n)) space
- avg   : O(n log (n)) time | O(log(n)) space
- worst : O(n^2))      time | O(log(n)) space pivot 값이 가운데로 스왑되는게 아니고 계속 맨끝에서 스왑되면 그다음에 다루어야 할 값이 n-1, n-2 하나씩 줄어들면 n^2가 됨


```
function quickSort(arr) {
	quickSortHelper(0, arr.length-1, arr)
	
	return arr
}

//           P  R   L 
//let arr = [2, 1 , 3, 5]
function quickSortHelper(startIdx, endIdx, arr){
	//base case
	if(startIdx >= endIdx ) return
	
	//recursive case
	let pivotIdx = startIdx;
	let leftIdx = startIdx + 1;
	let rightIdx = endIdx;
	
	while(leftIdx <= rightIdx){
		if(arr[leftIdx] > arr[pivotIdx] && arr[rightIdx] < arr[pivotIdx]){
			swap(leftIdx, rightIdx, arr)
		}
		
		if(arr[leftIdx] <= arr[pivotIdx]){
			leftIdx += 1;
		}
		if(arr[rightIdx] >= arr[pivotIdx]){
			rightIdx -= 1;
		}
	}
	swap(pivotIdx, rightIdx, arr)

	let leftSideArrLength = (rightIdx - 1) - startIdx 
	let rightSideArrLength = endIdx - (rightIdx + 1)
	let isLeftSideArrLengthSmaller = leftSideArrLength < rightSideArrLength
	
	if(isLeftSideArrLengthSmaller){
		quickSortHelper(startIdx, rightIdx-1, arr)
		quickSortHelper(rightIdx+1, endIdx, arr)
	}
	else{
		quickSortHelper(rightIdx+1, endIdx, arr)
		quickSortHelper(startIdx, rightIdx-1, arr)
	}
}

function swap(i, j, arr){
	let temp = arr[i]
	arr[i] = arr[j]
	arr[j] = temp
}
```