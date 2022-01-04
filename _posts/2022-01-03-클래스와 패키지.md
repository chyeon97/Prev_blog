---
layout: single
title: "클래스와 패키지"
categories: java
tag: [java, class, instance, package]
toc: true
---

## 이 글에서 알 수 있는 내용

- 클래스와 인스턴스 정의
- 클래스 구성 요소
- 패키지 정의

## 클래스(Class)와 인스턴스(Instance)

> 클래스: 객체를 정의하는 틀  
> 인스턴스: 메모리에 할당된 객체

### 클래스 인스턴스화?

> 클래스로부터 객체를 선언하는 과정

```java
SmapleClass example = new SampleClass();
```

## 🤔 클래스에는 어떤 것들이 있을까?

- 인스턴스 변수
- 인스턴스 메서드
- 생성자

### 인스턴스 변수

> 클래스 내에서 선언된 변수를 의미함  
> 같은 클래스 내에 위치한 메서드 내에서 접근이 가능함

### 인스턴스 메서드

> 클래스 내에서 선언된 메서드를 의미함

### 생성자(Construcor)

> 객체의 생성과 동시에 인스턴스 변수를 원하는 값으로 초기화하기 위한 것

#### 🟠 생성자 규칙

- 클래스 이름과 동일해야 한다
- 값을 반환❌ , 반환형 표시❌
- 인스턴스 생성의 마지막 단계이다
- 어떤 이유든 생성자 호출이 생략된 인스턴스는 인스턴스가 아니다 → 반드시 클래스 내에 생성자가 존재해야 하는 이유 <span style="color:green">✔︎</span>

<details>
<summary>디폴트 생성자(Default Constuctor)</summary>
<div markdown="1">
> 컴파일러가 인스턴스 생성 규칙인 `생성자 호출`을 유지하기 위해 삽입함  
> 인자가 없는 형태로 정의됨
</div>
</details>

<details>
<summary>this 참조변수</summary>
<div markdown="1">
> 인스턴스가 바로 자기 자신을 참조하는 데 사용하는 변수

```java
class Test{
  private int num;

  public Test(int num){
    this.num = num;
  }
}
```

<span style="color:green">✔︎</span> 위 예시와 같이 this 키워드는 생성자의 매개변수명과 인스턴스 변수명이 일치할 때 인스턴스 변수명 앞에 사용한다  
<span style="color:green">✔︎</span> this 참조변수는 인스턴스 메서드(`static` 키워드가 없는 메서드) 에서만 사용이 가능하다

</div>
</details>

<details>
<summary>this()</summary>
<div markdown="1">
> - 같은 클래스의 다른 생성자를 호출할 때 사용함   
> - 생성자 내에서만 사용이 가능함

<span style="color:green">✔︎</span> `this()`에 인수를 전달하면 생성자 중에서 메서드 시그니처가 일치하는 다른 생성자를 호출함

</div>
</details>

## 패키지(Package)

> 비슷한 성격의 클래스를 모아 놓은 디렉터리

### 🤷🏻‍♂️ 왜 사용할까?

- 공통된 특성의 클래스를 모을 수 있으므로, 클래스 분류가 용이함
- 동일한 클래스명이 있더라도 패키지명을 달리하면 해당 클래스를 사용할 수 있음

### 패키지 이름을 짓는 규칙은 뭐가 있을까?

- 클래스와 구분하기 위해 소문자로 구성한다
- 클래스를 제공하는 인터넷 도메인 이름의 역순으로 설정한다
- 패키지명 끝에 클래스를 정의한 주체명을 추가한다

## 🧗🏼‍♀️ 알고 있으면 좋을 내용

<details>
<summary>클래스 파일이 생성되는 수는 몇 개 일까?</summary>
<div markdown="1">
> `.class` 파일은 `.java` 내에 정의된 클래스 수만큼 생성된다
</div>
</details>

<details>
<summary>
JVM은 어떻게 class 파일을 찾을까?
</summary>
<div markdown="1">
> `class path`를 통해 찾는다

```bash
├── PackageStudy
│   ├── WhatYourName.class
│   └── Myclass
│         ├── AAA.class
│         ├── BBB.class
```

🔴 위 파일구조에서 문제점은 무엇일까?  
`PackageStudy`위치에서 `AAA.class`와 `BBB.class` 파일에 접근이 불가능하므로 JVM은 두 개의 class 파일을 찾을 수 없다

🟢 어떻게 해결해야하나?  
`PackageStudy` 위치에서 **set classpath = .; ...\PackageStudy\Myclass** 를 입력한다  
이는, 현재 디렉터리(.)와 Myclass 경로를 class path를 설정하는 것을 의미한다

</div>
</details>
