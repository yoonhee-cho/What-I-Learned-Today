# "fatal: refusing to merge unrelated histories" Git error

- It occurs when two unrelated projects are merged (projects that are not aware of each other's existence and have mismatching commit histories)
- 나의 경우에는 MEAL :P 프로젝트 할 때 master branch에서 작업하고 있엇는데 갑자기 main 브렌치가 나타나서 main(default) branch로 merge 하려고 했는데 error가 떴음 

## Solution 
 ```
 git pull origin master --allow-unrelated-histories
 ```
