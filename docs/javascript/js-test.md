# 재밌는 Javascript 테스트

헷갈리기 쉬운 또는 아예 모르고 쓰고 있었을법한.. js 문법들을 테스트 해볼 수 있는 연재물이다 ㅎㅎ

[Interview](https://learn.coderslang.com/tags/js-test)

하나하나 살펴보자

1. type-conversion

```javascript
let str = "1";
typeof +!str; // number
```

- ‘1’ 인 string 은 !’1’ 인 경우에 !1 과 같아서 false 를 반환하고 +false 는 +0 이어서 number 로 type-conversion이 된다..!

3.

```javascript
const x = '2' + 3 - true + '1'; // '221'
```

- '23' - true 가 가능하려면 둘 다 number 로 casting 된다.


5. arrow function으로 getter를 구현할 수 없다.

this bound

6.

- arrow functions don’t have access to the arguments array.

8. setTimeout with 0ms delay

```javascript
setTimeout(() => console.log('hello'), 0)
```

위와 같이 delay에 0을 넣은 setTimeout 이라고해서 바로 수행되는 것은 아니다. 3ms 정도 후에 수행되게 되는데 그 이유는 setTimeout에 인자로 넘어간 함수는 `message queue` 에 들어가서 async 하게 동작한다. 그래서 다음 sync execution 이후에 수행되게 되며 그게 브라우저 구현마다 다르겠지만 대략 3ms 정도 된다고 함!


