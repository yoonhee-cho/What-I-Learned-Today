# BST 

- all left nodes values are stricly less than root node
- all right nodes values are strictly greater than root node

- 진행 될 때 마다, 봐야할 노드가 반으로 줄어듬 => beauty of BST
```
        10
       /  \
      5    15
    /  \   / \
   2   5  13  22
  /       / \
 1      12   14

```
## Deletion Node method is tough due to a few edge cases


1. 부모노드 있고없고 상관없이 자식노드가 둘다 있을 경우 //(루트 노드(부모없는 노드) 포함)
- if the node has left&right child nodes // root node (10) ->
- grab the smallest value in the right sub tree
- grab (12) value from right subtree, erase (10), replace (10) with (12), remove (12) on the right sub tree
 
2. 부모노드가 없고, 자식노드는 하나밖에 없거나 아예 없을 경우( parent node x 부모노드없을 경우)
- 지워야할 현재노드에 왼쪽 자식노드가 있을 경우 : 현재 노드 벨류를 왼쪽 자식노드 벨류 갑으로 대체, 
- 지워야할 현재노드에 오른쪽 자식노드가 있을 경우 
- 지워야할 루트 노드의 자식노드가 없을 때 do nothing

3. 부모노드 있고, 자식이 하나밖에 없거나 아예 없을 경우
- 부모노드의 왼쪽자식노드가 현재 지워야할 노드일 경우 : 현재노드의 왼쪽 자식노드가 있으면 그게 부모느드의 왼쪽 자식노드가 되고, 아니면 현재노드의 오른쪽 자식노드가 부모노드의 왼쪽 자식노드가 됨
- 부모노드의 오른쪽 자식노드가 지워야할 현재노드 일 경우 : //


## Solution
- avg   : time : O(log(n))  |   space: O(1) // recursion 쓰면 O(log(n)) O(d) : depth of the tree (because of usage of callstack)
- worst : time : O(n)       |   space: O(1)
- unbalancedd tree cannot be elimated half of the tree

```

class BST {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }

  insert(value) {
		let currentNode = this;
		while(true){
			if(value < currentNode.value){
				if(currentNode.left === null){
					currentNode.left = new BST(value);
					break
				}else{
					currentNode = currentNode.left;
				}
			}
			else if(value >= currentNode.value){
				if(currentNode.right === null){
					currentNode.right = new BST(value)
					break
				}
				else{
					currentNode = currentNode.right
				}
			}
			
		}
		return this
  }

  contains(value) {
		let currNode = this
		
		while(currNode !== null){
			
			if( value === currNode.value){
				return true
			}
			else if(value < currNode.value){
				currNode = currNode.left
			}
			else if(value > currNode.value){
				currNode = currNode.right
			}
		}
		return false
  }

  remove(value, parentNode = null) {
		let currNode = this;
		
		while(currNode !== null){
			if(value < currNode.value){
				parentNode = currNode
				currNode = currNode.left
			}
			else if(value > currNode.value){
				parentNode = currNode
				currNode = currNode.right
			}
			else{
				if(currNode.left !== null && currNode.right !== null){
					currNode.value = currNode.right.getMinVal();
					currNode.right.remove(currNode.value, currNode)
				}
				else if(parentNode === null){
					if(currNode.left !== null){
						currNode.value = currNode.left.value
						currNode.right = currNode.left.right
						currNode.left = currNode.left.left
					}
					else if(currNode.right !== null){
						currNode.value = currNode.right.value
						currNode.left = currNode.right.left
						currNode.right = currNode.right.right
					}
					else{
							//do nothing
					}
				}
				else if(parentNode.left === currNode){
					parentNode.left = currNode.left !== null ? currNode.left : currNode.right
				}
				else if(parentNode.right === currNode){
					parentNode.right = currNode.left !== null ? currNode.left : currNode.right
				}
				break;
			}
		}
    return this;
  }
	
    getMinVal(){
        let currNode = this;
        while(currNode.left !== null){
            currNode = currNode.left
        }
    return currNode.value
    }
}

```