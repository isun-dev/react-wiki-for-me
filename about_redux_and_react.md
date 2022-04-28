## 리액트는 one-way data flow 이다.
- 상태(State)는 특정 시점에 앱의 상태를 설명한다.
- UI는 해당 상태를 기준으로 렌더링된다.
- 사용자의 액션에 따라, 어떤 일이 발생할 경우 발생한 내용에 따라 상태가 업데이트된다.
- UI는 새 상태를 기반으로 리렌더링된다.
- "Mutable" means "changeable". If something is "immutable", it can never be changed.
- JavaScript objects and arrays are all mutable by default.
- In order to update values immutably, your code must make copies of existing objects/arrays, and then modify the copies.
- We can do this by hand using JavaScript's array / object spread operators, as well as array methods that return new copies of the array instead of mutating the original array

## 리덕스 전문용어(처음에는 독립적인 개념으로 이해하는것이 사용하기 쉽게 느껴짐)
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
- 일종의 함수이고, current state와 action object를 받는다. state를 어떻게 업데이트 할지를 결정하고 업데이트를 한 후, new state를 return 한다.
- reducer는 수신된 작업(이벤트) 유형을 기준으로 이벤트를 처리하는 이벤트 수신기(event listener)로 간주할 수 있다.
- reducers는 아래 규칙을 반드시 따라야 한다.
1. new state 값은 state 및 action 인수를 기반으로만 계산해야 한다.
2. state의 불변성을 유지하기 위해, existing state를 변경하는건 절대 허용하지 않는다.기존 state를 복사해서, 복사된 state를 변경해야 한다.
3. 비동기 로직을 수행하거나, 임의의 값을 계산하거나, 다른 "side effect"을 일으키지 않아야 한다.
4. reducers 함수 내부의 로직은 일반적으로 동일한 일련의 단계를 따릅니다.
(1) reducer가 이 동작을 신경쓰는지 확인한다(즉 state변경과 관련된 내용이 있다면, 그리고 그 액션 타입과 관련된 내용이 있다면) => If so, make a copy of the state, update the copy with new values, and return it
(2) 그렇지 않다면, return the existing state unchanged
```javascript
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === 'counter/incremented') {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1
    }
  }
  // otherwise return the existing state unchanged
  return state
}
```
- 왜 Reducer라고 불리나?
1. 이걸 이해하기 위해서는 자바스크립트의 Array.reduce()를 잘 이해해야 한다.
2. reduce() 메서드는 배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환한다.
3. 리듀서 함수는 네 개의 인자를 가집니다.
- 누산기 (acc)
- 현재 값 (cur)
- 현재 인덱스 (idx)
- 원본 배열 (src)
- 리듀서 함수의 반환 값은 누산기에 할당되고, 누산기는 순회 중 유지되므로 결국 최종 결과는 하나의 값이 된다.
- arr.reduce(callback[, initialValue])
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
```javascript
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (previousValue, currentValue) => previousValue + currentValue,
  initialValue
);

console.log(sumWithInitial);
// expected output: 10

```
- A Redux reducer function is exactly the same idea as this "reduce callback" function! It takes a "previous result" (the state), and the "current item" (the action object), decides a new state value based on those arguments, and returns that new state.
- reducer과 reduce()의 차이점은 Array.reduce()의 경우 이 작업이 한 번에 수행되고 Redux의 경우 실행 중인 앱의 수명(lifetime) 동안 수행된다는 것이다.
