# Problems that get asked during a JavaScript interview
- Speaker: Dominique Canlas

## Interview Cheat Sheet :
1. ***** Clarify what is being asked, what is confusing, expected input output, edge cases
2. Ask how many questions they plan to ask so that you can pace yourself
3. *********** Speak while you code 아는데 실천이 넘나 어려움 ㅠ_ㅠ 
4. Write test cases for your code (Even before you start) 뭐 잘못이해하고있는지 인터뷰어가 캐치할수있음
5. Be prepared to use white board

- Useful Resources
http://javascript.info/
http://bonsaiden.github.io/JavaScript-Garden/
http://ejohn.org/apps/learn/
https://leanpub.com/understandinges6/read

- facebeook ui developer : javascript으로 다무러봄, foundational JavaScript이 리엑트보다중요 함... 

## JavaScript Questions
- highly looking at the library 혼자 복제해보기 low dash ???? 되게도움많이됨.

1. CLOSURE 
- Execute function after x times

- Create a function "after" that returns a new function where this new function executes the original function only after it has been executed x times


- only execute func2, after it has been called two times, after third times
- think skeleton of func body

```
Sample calls

var newFunc1 = after(3, func1);
var newFunc2 = after(2, func2);

var func1 = () => console.log("fisrt one");
var func2 = (x)=> console.log("the 2nd one, x)

newFunc1();
newFunc1();
newFunc1();
newFunc1(); // actually calls func1()

newFunc2("a");
newFunc2("a");
newFunc2("a"); // actually calls func2()
newFunc1(); // calls func1() again

function after(num, func) {
    let count = 0;
    
    return function(x){
        if( count >= num ){
            return func(x);
        }
        else{
            count += 1;
        }
    }
}

- keeps remember the count references it.
- {} every curly braces set is closure


- 위에서 args패스하지않아도 항상 available해

function after(num, func) {
    let count = 0;
    
    return function(){
        if( count >= num ){
        //arguments -> array [x, y, z]
        //.call() vs .apply() 꼭 나올 문제
        //   코마세퍼레이티드억셉  어레이 억셉
        
        return func.apply(null, arguments);
        // why put null ? 
        // accept context as 1st arguments
        // we don't need context on this prob so we pass null
        // documentation 찾아서 읽어보기
        }
        else{
            count += 1;
        }
    }
}
```

# call, apply, bind - this 
- call : this는 call을 사용하면, this를 다른 값으로 변경할 수 있다.
```
    const h1 = {name: "Yoon"};
    const h2 = {name: "Philip"};
    function i(){
        return `hi ${this.name}`
    }

    i();        -> hi undefined
    i.call(h1); -> hi Yoon
    i.call(h2); -> hi Philip
```

```
    function j(a,b){
        this.aa = a;
        this.bb = b;
    }
    j.call(h1, 1234, 5678) -> h1 = {name: "Yoon", aa: 1234, bb: 5678}
```

- apply : call과 작동원리는 같지만, call이 매개변수(paramenter)를 직접받는 구조라면, apply는  배열 그 자체를 매개변수로 대입할 수 있음
```
    j.apply(h1, ['aaa', 'bbb']); -> h1 = {name: "Yoon", aa: 'aaa', bb: 'bbb'}

    const h3 = [1, 2, 5, 8, -10, 11, 234];
    Math.min.apply(null, h3); -> -10
    Math.max.apply(null, h3); -> 234
```
- bind : this 값을 바꿀 수 있다는 점은 call, apply랑 같다고 볼 수 있지만, bind는 this값을 영구적으로 바꿀 수 있다.
```
    const newJ = j.bind(h1);
    newJ('ccc', 'ddd'); -> h1 = { name: 'Yoon', aa: 'ccc', bb: 'ddd'}
    newJ.call(h2, 'eee', 'fff'); -> h1 = { name: 'Yoon', aa: 'eee', bb: 'fff'} / h2 = {name : 'Philip}
```
- bind를 쓰고 난 후, call이나 apply를 쓰면 this 값이 지정한대로 대입이 안되서 같이 쓰지 않는 것이 좋음
- 근데 왜 이런 method들이 있어야하지? -> this를 자유자재로 설정할 수 있다는 게 객체지향프로그램의 기초가 되고, 단순히 선언하고사용하는 것이 아니라 필요한 부분에 조합해서 최적의 성능을 만들어내는 기초.. 

2. Create Emitter Class
- create a class/function that returns an Emiiter Object. This object allows us to subscribe to an event and execute a callback whenever that event is triggered. The emit function will trigger all functions subscribed to an event and pass all supplied arguments

- A Callback can be removed from being subscribed to an event

- functions - subscribe(eventName, cb), emit(eventName, args)
- subscribe - returns 'release functionality'


    //skeleton what should input outut
```
function Emitter(){

    const eventTracker = {
        //key = eventName, value: arr of funcs
    }

    const subscribe = (name, cb) =>{
        eventTracker[name] = cb

        if(eventTracker[name]){
            eventTracker[name].push(cb)
        }
        else{
            eventTracker[name] = [cb];
        }

        const release = () => {
            let theCbs = eventTracker[name];
            let theIdx = theCbs.indexOf(cb); //못찾으면 -1리턴
            if(theIdx > -1 ){
                theCbs.splice(theIdx, 1);
            }
        }

        return {
            release
        }
    }

    const emit = (name, ...theArgs) => {
        let theCbs = eventTracker[name];
        for(let i = 0; i < theCbs.lenght; i++){
            let cb = theCbs[i];
            cb.apply(null, theArgs);
        }
    }

    return {
        subscribe: subscribe,
        emit: emit
    }
}

let myEmit = new Emitter();

function logArgs(...items) {
    console.log(items)
}

function sumAll(...nums){
    let result= nums.reduce((acc, cur)=> acc + cur, 0);
}

let sub1 = myEmit.subscribe("foo", logArs);
let sub2 = myEmit.subscribe("foo", sumAll);
let sub3 = myEmit.subscribe("bar", sumAll);

myEmit.emit("foo", 1, 2)
myEmit.emit("bar", 5, 6)
sub1.release();
myEmit.emit("foo", 1, 2);

export default Emitter;
```

- No there isn’t. Ruby refers to it as “hash”, JS as “object”, and python as “dictionary”

- Test spec 쓰는게 중요, 

https://codesandbox.io/s/jovial-jepsen-v27et?file=/src/emitter.js

## Q & A 
- front end back end 포지션 상관없이 다 풀스텍이야 . 어째튼 결국에는 다 해야됨. 뭐 스페셜티가 있을 수는 있겠지만 
- 1-2년후엔, build that from the ground up, being able to have responsibility를 기대?하는게 좋음
- var is replaced , let and const are what you supposed to use
- cannot use arguments as variable 
- rest of args becomes squeezed in to an arr
- at least 2 test cases , 1 for generic case easy no edge case, 1 for edge case // shows interviewer that this person thinks all possible cases 
- time complexity could be asked for this js 
- emit - O(n) loop over every single funcs
- how many coding problems ? 1-2 questions (1: easy? , 2:  )
- how long did you study? 1-2 months leetcode, brushing up 
- JavaScript Problems where to find them ? -> libraries,,, reimplement them. 라이브러리 구현해보기 자바스크립트로 
- Can you give me some examples of the libraries that you implemented?
- ...args -> in the arr -> no need to user ... -> play around with spread operator
- 다른사람과의 차별졈??? foundational, side projects, showing , (contributing to popular open source projects is also helpful)
- 시간다됐는데, 문제는푼경우 -> 스크린인터뷰 때 : 
- 일주일 남으면 뭐 준비할래 : 60% leetcode 데이터structure and algorithm / 40% UI front-end 
- soft skill questions : 사람들하고 충돌했을 때 어떻게 해결했는지 ?
- 모르는데 어떠캄 be honest about .. what you don't understand , let me think about this for a minute, these are the things that I don't know, and these are the things that i don't understand.  
- 약점뭐냐고 물어보면 뭐라고 답해? -> 실제약점 andthen what are you doing to improve that, 멀티테스킹 못하는데 켈린더로 킵트랙, 
- 못해도 뭐, 다시 다른데 하면되고, 육개월뒤에 다시연락옴
- 크레이그리스트 extra help 
- 새로운 언어배우는데 ? 하나 배워놓으면 다른거 배우는 건 그렇게 어렵지않아........?
- 1 : one object oriented language & 1: script language like javascript
- Survey: http://bit.ly/3orpmGh Subscription for mentors: https://www.skilledinc.com/subscription-mentor(Dominique is page 4)Event page: https://leads.skilledinc.com/skilled-events/ Learn more about Skilled: https://www.skilledinc.com/job-seeker