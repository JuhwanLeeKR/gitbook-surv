# array

## Javascript의 배열은 `객체`다

```js
const arr = [1,2,3]

arr[3] = 'test'
arr['property'] = 'string value'
arr['obj'] = {}
arr[{}] = [1,2,3]
arr['func'] = function () {
  return 'hello'
}

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i])
}
/**
 * 출력
 * 1
 * 2
 * 3
 * test
 * ❗️ for문의 let이 Number이기 때문에 출력이 안된다
 */

// 실제 arr 값
console.log(arr)
/**
[
  1,
  2,
  3,
  'test',
  property: 'string value',
  obj: {},
  '[object object]': [1,2,3],
  func: ƒ
]
*/
```

- 배열을 아래와 같이 생각해 볼 수 있기 때문에 배열을 다룰 때는 주의를 해야한다

```js
const arr = [1,2,3]

const obj = {
  0: 1,
  1: 2,
  2: 3
}
```

- javascript에서 배열을 확인할 때는 `Array.isArray()`를 사용하자

## Array.length
