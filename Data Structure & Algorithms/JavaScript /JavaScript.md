## JavaScript
- single thread language means it can only do one thing at a time
- The event loop's job is looking at the stack and the task queue, if the stack is empty, it takess first thing on the task queue and pushes it on the the stack 
- process.nextTick > SettimeOut > Setimmediate

```
JS - heap, stack

WebAPIs - DOM(document), ajax(XMLHttpRequest), setTimeout

callback Queue - []
```

- how to reset for loop : set i = -1 / why not i = 0 ? because i++ will bring it back up one more. 