# variable

- var: 함수 스코프
- let, const: 블록 스코프, TDZ

> **TDZ (Temporal Dead Zone)** 란?
> 변수가 선언된 스코프의 시작 지점부터 변수가 초기화되는 지점까지 해당 변수에 접근할 수 없는 구간
> let과 const는 호이스팅되지만 스코프 내에서 선언되기 전에는 변수에 접근할 수 없다

```js
var name1 = '이름'
var name1 = '이름2' // var를 사용하면 같은 스코프 내에서 변수를 재선언할 수 있다


let name2 // undefined
console.log(name2)
/*
 let name;의 경우처럼 변수를 선언만 하고 값을 할당하지 않은 상태에서는 TDZ를 벗어난 것으로 간주된다.
 즉, 변수 name은 선언과 동시에 undefined로 초기화되어 있기 때문에, TDZ에 해당하지 않는다.
 */
name2 = '이름' // let으로 선언된 변수는 재할당 가능

const name3 = '이름' // const는 선언과 동시에 초기화해야 하며, 재할당 불가능
```

## 전역 공간 사용을 최소화하자

전역 변수를 선언할 때는 기존의 전역 객체나 함수와 충돌하지 않도록 주의해야 한다.
예를 들어, 내장 함수 setTimeout의 이름을 전역 변수로 사용하면 원래의 setTimeout 함수에 접근할 수 없게 된다.

```js
var setTimeout = 'setTimeout'
// 전역으로 setTimeout으로 변수를 선언할 경우 window API인 setTimeout을 사용할 수 없다
```

> **Monkey patch**란?
> 소스코드를 변경하지 않고 실행 시 코드 기본 동작을 추가, 변경 또는 억제하는 기술이다.
> 쉽게 말해 어떤 기능을 위해 이미 있던 코드에 삽입하는 것을 말한다.

```js
// 기존의 Array.prototype.push 메서드 저장
const originalPush = Array.prototype.push;

// Array.prototype.push 메서드를 확장하여 요소가 추가될 때마다 메시지를 출력
Array.prototype.push = function(...args) {
    console.log(`Adding ${args.length} elements:`, args);
    return originalPush.apply(this, args);
};

// 사용 예시
const myArray = [1, 2, 3];
myArray.push(4); // 콘솔에 "Adding 1 elements: [4]"가 출력
myArray.push(5, 6); // 콘솔에 "Adding 2 elements: [5, 6]"가 출력
```

> Monkey Patching은 강력한 기능이지만, 그 사용은 코드의 복잡성과 유지보수 문제를 야기할 수 있기 때문에,
> 필요한 경우에만 신중하게 사용해야 한다.

## 임시변수를 사용을 최소화하자

임시변수가 가득한 코드는 명령형으로 가득한 코드이며, 디버깅하기 힘들게 된다

```js
function getRandomNumber (min, max) {
  const randomNumber = Math.floor(Math.random() * (max + 1) + min)
  return randomNumber
}
```

```js
function getRandomNumber (min, max) {
  const randomNumber = Math.floor(Math.random() * (max + 1) + min)

  randomNumber.추가작업 // getRandomNumber 사용하는 곳들에서 문제가 생길 수 있다.

  return randomNumber
}
```

```js
function calculateOrderPrice(items) {
  let totalPrice = 0;
  let itemCount = items.length;
  for (let i = 0; i < itemCount; i++) {
    let itemPrice = items[i].price;
    let itemQuantity = items[i].quantity;
    let itemTotal = itemPrice *itemQuantity;
    totalPrice += itemTotal;
  }
  let tax = totalPrice* 0.1;
  let shipping = itemCount > 10 ? 0 : 20;
  let orderTotal = totalPrice + tax + shipping;
  return orderTotal;
}
```

- 임시변수 최소화

```js
function calculateOrderPrice(items) {
  const totalPrice = items.reduce((total, item) => total + item.price *item.quantity, 0);
  const tax = totalPrice* 0.1;
  const shipping = items.length > 10 ? 0 : 20;
  return totalPrice + tax + shipping;
}
```

> 경우에 따라 완전히 제거하지 않는 것이 코드의 가독성과 유지보수성에 더 도움이 될 수 있다.

### **해결책**

1. 함수 나누기
2. 바로 반환하기
3. 고차함수 사용하기 (map, filter, reduce)
4. 선언형으로 작성하기

## 호이스팅 주의하기

런타임시 선언이 최상단으로 끌어올려짐
코드 작성시 예측하지 못한 실행 결과가 나올 수 있다

```js
myFuncExpr(); // TypeError: myFuncExpr is not a function

var myFuncExpr = function() {
  console.log("Hello, World!");
};
```

var로 선언하였기 때문에 런타임시 아래와 같이 동작하게 된다

```js
var myFuncExpr;
myFuncExpr(); // TypeError: myFuncExpr is not a function

var myFuncExpr = function() {
  console.log("Hello, World!");
};
```
