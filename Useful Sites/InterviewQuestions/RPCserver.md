# RPC server

```
let nextStorage = {
    //id: [{id: 0, timeStamp: 0, status: 'start'}, {id: 0, timeStamp: 2, status: 'end'}]
}

function alertSetTimeOut(next){


  if(!nextStorage[next.id]){
    nextStorage[next.id] = [next]
  }
  else{
    nextStorage[next.id].push(next)
  }


  if(next.status === 'end'){
    if(Math.abs(nextStorage[next.id][0]['timeStamp'] - nextStorage[next.id][1]['timeStamp']) > 3){
      console.log(`next object with id ${next.id}timeStamp is over than 3`)
      delete nextStorage[next.id]
    }
  }
}
```
- What is RPC server?
- what other ways possible to make nextStorage approachable in the function?
- object.key === object['key']
- Math.abs() : get the absolute value
- substracts