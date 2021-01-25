# Selection Sort

- we are not gonna make new arrs but, we make two sub arrs(one subarr : unsorted nums / another subarr: sorted nums ) withn in the given input arr by using pointer
- In the beginning, we started with our entire list representing that unsorted list
- Iterate the unsorted list bunch of times, and each time, find the smallest num in the unsorted list, and append it to the sorted sublist by swapping the elements
- keep doing this until we no longer have els in unsorted sublist.
- 가장작은 숫자를 선택(SELECTION)해서 sorted list 앞쪽으로 스왑해서 ??

## My Interpretation
- 가장 처음부터 시작. 어레이 가장 앞에 있는 엘리먼트가 가장 작을거라고 가정을 일단하기. 베리어블 현재엘리먼트위치 는 0
- 가장 작은엘리먼트를 가정하는 현제엘리먼트인덱스가 어레이길이 - 1 (= 두번째마지막, 어레이에서 마지막하나 남겨둔거) 일동안, 와일돌리기
- 와일룹 안에서 for loop을 가장 작은 엘리먼트를 가정하는 시작엘리먼트 '다음'부터 ~ 마지막 엘리먼트까지 돌려서 시작점이랑 비교해가면서 가장 작은 엘리먼트를 찾음 
- for loop이 끝나면 가장 작은 엘리먼트를 지칭하는 인덱스가 나온상태 
- 아직 와일룹 안에서 시작점에 있는 엘리먼트와 가장작은 엘리먼트를 바꿔줌 그리고나서, 시작점은 한칸 이동 ... 
- 그렇게 효과적인 알고리즘은 아니지만, 구현하기 쉬운 장점이 있음

## Solution
- best : O(n^2)time - even tho the arr is sorted and swap is not needed, while loop and for loop has to be gone thru | O(1) space
- avg  : O(n^2)time | O(1)space
- worst: O(n^2)time | O(1)space
```
    function selectionSort(arr){
        let currElIdx = 0 ; // 시작점  0 -> 1 -> 2 -> 3 -> 4 ...

        while(currElIdx < arr.length - 1 ){ //arr.length -1 마지막엘리먼트 전까지 
            let smallestElIdx = currElIdx; // 일단 가장작은 엘리먼트 인덱스가 시작점이라고 가정해두고 

            for( let i = currElIdx + 1; i < arr.length; i++ ){ // 시작점 다음 엘리먼트들을 돌아보면서 가장작은 엘리먼트를 찾음
                if(arr[smallestElIdx] > arr[i] ){
                   smallestElIdx = i;
                }
            }
            let temp = arr[smallestElIdx]; // 스왑
            arr[smallestElIdx] = arr[currElIdx];
            arr[currElIdx] = temp
            currElIdx +=1 ;             // 시작점을 하나 증가해주기 
        }
        return arr;
    }

    let arr = [5, 2, 3, 1, 2]
    let arr = [1, 2, 3, 5, 2]
    let arr = [1, 2, 2, 5, 3]
    let arr = [1, 2, 2, 3, 5]


    

    currElIdx = 0; (5)
    while loop passes -> i = 1,2,3,4, ( 현재 시작엘리먼트랑 비교해서 제일작은엘리먼트 인덱스를 저장)
```