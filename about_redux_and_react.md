## 리액트는 one-way data flow 이다.
- 상태(State)는 특정 시점에 앱의 상태를 설명한다.
- UI는 해당 상태를 기준으로 렌더링된다.
- 사용자의 액션에 따라, 어떤 일이 발생할 경우 발생한 내용에 따라 상태가 업데이트된다.
- UI는 새 상태를 기반으로 리렌더링된다.
- "Mutable" means "changeable". If something is "immutable", it can never be changed.
- JavaScript objects and arrays are all mutable by default.
- In order to update values immutably, your code must make copies of existing objects/arrays, and then modify the copies.
- We can do this by hand using JavaScript's array / object spread operators, as well as array methods that return new copies of the array instead of mutating the original array

## 리덕스 전문용어
### Actions == 발생하는 이벤트에 대한 설명
- type 필드를 가진 순수 자바스크립트 객체이다. 
- 응용 프로그램에서 발생한 일을 설명하는 이벤트라고 생각할 수 있습니다.
- 타입필드는 액션에 대한 설명을 할 수 있는 이름으로 짓고, string 이어야 한다. 
- 주로 사용하는 형식은 domain/eventName이고,  domain는 일종의 카테고리 이고, eventName은 발생하는 특정한 사건을 의미한다. 
- An action object can have other fields with additional information about what happened. By convention, we put that information in a field called payload.
```javascript
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```
### Reducers
- 일종의 함수이고, current state와 action object를 받는다. state를 어떻게 업데이트 할지를 결정하고, new state를 return 한다.
- reducer는 수신된 작업(이벤트) 유형을 기준으로 이벤트를 처리하는 이벤트 수신기(event listener)로 간주할 수 있다.
