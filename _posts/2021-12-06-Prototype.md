---
layout: single
title: "Prototype"
categories: Javascript
tag: [Javascript, Prototype, 프로토타입, 프로토타입 체인]
toc: true
---

## 이 글에서 알 수 있는 내용

- 프로토타입은 무엇인가
- 프로토타입 작동 원리
- 프로토타입 체인
- 프로토타입으로부터 얻을 수 있는 점

## Prototype

> 자바스크립트에서 클래스, 객체의 내용 복사 없이 연결을 통해 상속을 구현할 수 있게 해주는 방법

## 작동 원리

① 함수를 생성하면 JS엔진은 해당 함수에 **prototype의 프로퍼티**를 생성함  
② 생성한 prototype의 프로퍼티는 **그 함수의 prototype의 객체**를 가리킴  
③ 함수의 prototype의 객체는 자신도 같은 함수의 소속이라는 것을 명시하기 위해 **constructor 프로퍼티를 만들고 해당 함수를 가리킴**  
&nbsp; &nbsp;➡︎ 함수와 함수의 prototype 객체는 `순환 참조`를 이룸

④ 해당 함수를 생성자 함수로서 사용하는 경우(`new 연산자`로서 함수를 호출하는 경우), `instance`에는 `__proto__`가 생성되며 생성자 함수의 Prototype 객체를 가리킴

### 예제

**Q. MC 객체는 어떻게 `getName()`을 가지고 있을까?**

```javascript
var Person = function (name, age) {
  this.name = name;
  this.age = age;
};
Person.prototype.getName = function () {
  return this.name;
};
var MC = new Person("유재석", 48);
console.log(MC); // {name:"유재석", age:48, getName: f()}
```

<img src="https://user-images.githubusercontent.com/40657327/144814400-3765dfa7-76ab-492b-9bc1-4b65a675d76a.png" width="550" height="300">

**A. MC의 `__proto__` 프로퍼티를 통해 상위계층의 Prototype에 접근할 수 있으므로 Person의 Prototype 객체이 있는 `getName()`을 참조할 수 있다.(프로토타입 체인)**

## Prototype Chain

> 어떤 메서드 내의 특정한 프로퍼티를 찾기 위한 것

### 동작 방식

> 어떤 메서드를 호출하면 JS엔진은 데이터 자신의 프로퍼티들을 검사함
>
> 1. 원하는 프로퍼티가 있다면? ⇨ 그것을 바로 실행
> 2. 원하는 프로퍼티가 없다면? ⇨ 차례대로 `__proto__` 를 검색해서 있으면 그 프로퍼티를 실행 ( 최상위 객체인 `Object.prototype`까지 검색하여 없다면 `undefined`를 출력함)

## Prototype을 통해 얻는 이점

- 해당 객체에 존재하지 않는 프로퍼티를 찾을 수 있음(**프로토타입 체인**)
- 생성자 함수로부터 생성될 모든 `instance`들이 공통적으로 사용할 프로퍼티/메서드를 미리 구현해 놓음으로써 **불필요한 코드 중복을 줄일 수 있음**
