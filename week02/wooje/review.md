# 이번주 리뷰
<br>
## Redux
> state가 엄청나게 많아졌을 때 사용, 컴포넌트에서 관리하는 값이 여러개가 되어서 상태의 구조가 복잡해질 때 사용. 버그 잡기도 용이

- Redux사용 이유 1. props없이 모든 컴포넌트가 state를 갖다쓸 수 있다.
    - state 데이터 사용하려면 원하는 컴포넌트에서 props의 형태로 등록하고 쓴다.
             
- Redux사용 이유 2. state 데이터 관리가능  
    - Redux에선 state 데이터의 수정방법을 미리 정의한다.
    
### Reducer
> 수정된 state를 return
- 데이터 수정하고 싶을 때, reducer로 수정하는 방법을 만들고, dispatch()로 수정하면 된다.

```jsx
function reducer(state, action) { // 기본state는 state의 초기값을 넣는 default parameter문법. parameter자리에 어떤 값을 입력하지 않으면 그 변수를 parameter에 집어넣는다.                                           
 
 // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```

```jsx
// index.js
<Provider store={store}>
      <App />
      </Provider>
...

import { createStore} from 'redux';


let 기본state = [
    {id: 0, name : '멋진신발', quan:2},
    {id: 1, name : '멋진신발2', quan:1}
];

function reducer(state = 초기값, 액션){ 
  if(액션.type === '수량증가'){ // 새로운 상태를 만드는 로직
    let copy = [...state]; // deep copy
    copy[0].quan++;
    return copy
  } else if(액션.type === '수량감소'){
    let copy = [...state]; 
    copy[0].quan--;
    return copy
  }  
  else {
  return state
}
    
let store = createStore(reducer);
```
```jsx
// Cart.js
<td>
    <button onClick={()=>{ props.dispatch({type : '수량증가'})}}>+</button>
    <button onClick={()=>{props.dispatch({type: '수량감소'})}}>-</button>
</td> 
```                      

## Reducer 여러개 쓰기
> combineReducers로 reducer여러개 일 때 사용
- ```import { combineReducers, createStore} from 'redux';```해주기
```jsx
let store = createStore(combineReducers({reducer, reducer2}));
```
```jsx
function state를props화(state) { // store안에 있던 데이터 가져와 props로 만들어줌
    //console.log(state);
    return{
     state : state.reducer,
     alert열렸니 : state.reducer2 // 여기도 수정
    }
}

export default connect(state를props화)(Cart)
```
- Redux에 저장하는 것은 한 컴포넌트에서만 쓰는 것에서는 사용X, 그럴 경우useState()사용하는게 낫다.

## dispatch로 수정요청할 때 데이터 보내기
```dispatch({type: '[type명]', payload: [보낼Data] })```
- 보낸 자료는 action parameter에 저장되어있다.

# 튜터에게 궁금한 점
useReducer(Hook)와  Redux가 초기 로직은 비슷한 부분이 있는 것 같아 두개의 차이점이 궁금합니다.