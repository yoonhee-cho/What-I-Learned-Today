# BST Traversal
```
            10
           /  \
         5      15
       /  \       \
      2    5       22
     /
    1
```

## 1. in-order : L - Root - R : [1, 2, 5, 5,10, 15, 22]

## 2. pre-order : Root - L - R : [10, 5, 2, 1, 5, 15, 22]

## 3. post-order : L - R - Root : [1, 2, 5, 5, 22, 15, 10]

## Solution

- time : O(N) N is number of nodes in the tree
- space : O(N) we are creating another arr with length N/ if the func is displaying the node val, O(d) d is depth or height of BST bc adding frames on the callstack 

```
function inOrderTraverse(tree, array) {
  // Write your code here.
	if(tree !== null){
		inOrderTraverse(tree.left, array)
		array.push(tree.value)
		inOrderTraverse(tree.right, array)
	}
	return array
}

function preOrderTraverse(tree, array) {
  // Write your code here.
	if(tree !== null){
		array.push(tree.value)
		preOrderTraverse(tree.left, array)
		preOrderTraverse(tree.right, array)
	}
	return array
}

function postOrderTraverse(tree, array) {
  // Write your code here.
	if(tree !== null){
		postOrderTraverse(tree.left, array)
		postOrderTraverse(tree.right, array)
		array.push(tree.value)
	}
	return array
}

```