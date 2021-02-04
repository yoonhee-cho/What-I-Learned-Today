## React

## why use REACT ?
- components are reusable
- state management
- virtual DOM** why it is fast-  makes reload fast, 
- JS world / CSS world  / DOM world
- when crossing, toll needs to be paid - > performance
- react does it for you
- technical reasons to use it

## Model View Controller
- View : what users see
- Model : data
- Controller : business logic


```
                VIEW
send requests,
renders        /   \    display
    CONTROLLER   --    MODEL
```

## Making a table (React Interview Question)
- make data with an array with objects
- array with arrays is not a good idea
- import Table from 'table' 
```
<Table  data ={data} headers={headers}/>
```
- how to put header? : seperate array of objects
```const headers = [{label:'Name', id: 'name}, {label: 'Age', id: 'age'}
]

const data = [
    {name: 'Allen', age: 35}, {name: 'Charlie, age:21}
]
```
- Table component

```
functional component
const {data, headers} = props;
return (
    <div>
        <table>
            <thead>
                <tr>
                    <td>{headers[0].label}</td>
                    <td>{headers[1].label}</td>
                    {
                        headers.map((header)=> {
                            // h is {label: 'Name', id: 'name'} - good tip
                            return ( <td key={header.label}>{header.label}</td>)
                        }
                    }
                </tr>
            </thead>
            <tbody>
                    {
                        data.map((d, i)=> {
                            // d = {name: 'Allen', age: 35}
                            return <tr key = {`row-%{i}`}>
                                        //wrong
                                        <td>{d.name}</td>
                                        <td>{d.age}</td>
                                        //correct
                                        {
                                            headers.map((h, j)=>{
                                                //h is  h is {label: 'Name', id: 'name', component : Checkbox}
                                                return <td key={`cell-${i}-${j}`}>{d[h.id]}</td>
                                            })
                                        }

                                   </tr>
                        })
                    }
            </tbody>
        </table>
    </div>
)

```

- view is same but if data is changed, view doesn't need to be change - good react code !!! 

- virtual DOM element id needs to compare with original DOM
- https://drive.google.com/drive/folders/11NAjgjkVUUJS2sJxDMu1z5jK_zamP3F3?usp=sharing

- key가 있으면 테이블 row column 바꿀수있음 쉽게 효율적으로 importance of key

- Checkbox component
- headrs array에 component: Checkbox 추가

 ```
 <td></td>
```
- headers: what td would display 

## Q & A 
- JavaScript > React
- 5 -10 questions, when would you use which components? design entire tables from scratch
- lifecycle of components
- callback 
- setState is async foo is 2 happens after the stack is empty
- it is async bc badge operation : otherwise gets lazy -_- ?
- 2-3 skillset: cultural fit, JavaScript fundamental: const var let / async sync/ cb pattern, problem solving skill - leetcode, codewars , 

- GraphQL, apolloPlan, 
- JS > CSS (e commerce / AWS) bigger rock, smaller rock, 하나에 전문가가 되기 9, 5 
- https://drive.google.com/drive/folders/11NAjgjkVUUJS2sJxDMu1z5jK_zamP3F3
- Backend > JS > CSS
- Projects optimize for learning, no grap attention
- General interviews : small company: react, css - bigger company: js, 
- business eco system , bussiness problems into technical solutions , 
- 