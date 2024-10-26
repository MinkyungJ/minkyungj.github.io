---
title: Remind Java2 - Variable
tags: [Java]
date: 2024-08-13 22:00 +0900
categories: [Java, Inflearn]
toc: true
---

## 변수 (Variable)

```java
package variable;

public class Var1 {
  public static void main(String[] args) {
    System.out.println(10);
    System.out.println(10);
    System.out.println(10);
  }
}
```

### Package

> 패키지란, 간단하게 자바 파일을 구분하기 위한 폴더이다.

[패키지 예시](#Var1)를 만들었다면, 해당 패키지에 들어가는 자바 파일 첫줄에 " package variable; " 와 같이 소속된 패키지를 선언해주어야한다.

- 자바 파일이 위치하는 패키지와, "package variable" 선언 위치가 같아야한다.

```실행결과
10
10
10
```

다음엔 20을 3번 출력하는 예시를 만들어보자.

```java
package variable;

public class Var2 {
  public static void main(String[] args) {
    System.out.println(20);
    System.out.println(20);
    System.out.println(20);
  }
}
```

> 위와 같은 변화는 단순한 예제로 3번만 변경했지만, 숫자를 출력하는 횟수가 많아질수록 변경해야하는 코드의 수는 많아진다.
> 따라서 어딘가에 값을 보관해놓고 필요할 때 값을 꺼내 읽을 수 있는 **저장소**가 필요하다.

**이러한 문제를 해결하기 위해 변수 기능을 사용한다.**

```java
package variable;

public class Var3 {
  public static void main(String[] args) {
    int a; // 변수 선언
    a = 20;
    System.out.println(a);
    System.out.println(a);
    System.out.println(a);
  }
}
```

> a의 값에 따라서 출력 값의 결과가 모두 변경되는 점을 확인할 수 있다.

---

## 변수 선언

숫자 정수 보관함 **int**

- 숫자 정수(integer)을 보관할 수 있는 이름이 a라는 데이터 저장소 = 변수
- 숫자 정수 뿐만 아니라 문자, 소수와 같은 다양한 종류의 값을 저장할 수 있는 변수들이 존재한다.
  - 숫자 정수를 저장하는 변수는 **int**

---

## 변수 값 변경

변수에 저장되어있는 값은 언제든지 변경할 수 있다.
중간에 변수의 값을 변경해보는 예시를 만들어보자.

```java
package variable;

public class Var4 {
  public static void main(String[] args) {
    int a;  // 변수 선언
    a = 10; // 변수 초기화
    System.out.println(a); // 10 출력
    a = 50; // 변수 값 변경 (10 -> 50)
    System.out.println(a);  // 50 출력
  }
}
```

> 결과로 보면 알 수 있듯이, 변수의 값을 변경하면 변수에 들어가있던 기존의 값은 삭제된다.

---

## 변수 선언과 초기화

### 변수 선언

변수를 선언하면 컴퓨터의 메모리 공간을 확보하여 그곳에 데이터를 저장할 수 있다.<br>
그리고 변수의 이름을 통해 해당 메모리 공간에 접근할 수 있다.

```java
package variable;

public class Var5 {
  public static void main(String[] args) {
    int a;
    int b;
    int c,d;
  }
}
```

> 변수는 a,b와 같이 하나씩 선언할 수도 있고, c,d와 같이 한번에 여러 변수를 선언할 수도 있다.

---

### 변수 초기화

변수를 선언하고, 선언한 변수에 처음으로 값을 저장하는 것을 변수 초기화라고 한다.

```java
package variable;

public class Var6 {
  public static void main(String[] args) {
    int a;
    a = 1;
    System.out.println(a);  // 변수 선언, 초기화 따로 진행

    int b = 2;  // 변수 선언과 초기화를 한번에
    System.out.println(b);

    int c = 3, int d = 4; // 여러 변수 선언과 초기화 한번에
    System.out.println(c);
    System.out.println(d);
  }
}
```

---

### ❗️ 변수는 초기화 해야한다!!

> 만약 변수를 초기화하지 않는다면?

```java
package variable;

public class Var7 {
  public static void main(String[] args) {
    int a;
    System.out.println(a);
  }
};

// 실행결과
java : variable a might not have been initialized
```

위 자바 코드를 실행하면 다음과 같은 컴파일 에러가 발생한다. 이는 변수가 초기화되지 않았다는 오류다.

> 메모리는 여러 시스템이 함께 사용하는 공간으로 계속해서 값들이 저장된다.
> 변수를 선언하면 메모리상의 어떤 공간을 차지하고 사용하기 때문에 해당 공간에 기존에 어떤 값이 들어있었는지 알 수가 없다.
> 따라서 변수를 초기화하지 않으면 이상한 값이 출력된다.

---

## 변수 타입

변수는 데이터를 다루는 종류에 따라 다양한 형식이 존재함.

```java
package variable;

public class Var8 {
  public static void main(String[] args) {
    int a = 100;
    double d = 10.5;
    boolean c = true;
    char d = 'A';
    String e = "Hello Java";

    System.out.println(a);
    System.out.println(b);
    System.out.println(c);
    System.out.println(d);
    System.out.println(e);
  }
};

// 실행 결과
// 100
// 10.5
// true
// A
// Hello Java
```

> **변수** : 데이터를 다루는 형태에 따라 타입(type)이라는 다양한 형식이 존재하며, 각 변수는 지정된 타입에 맞는 값을 사용해야함
>
> - int : 정수를 다룸
> - double : 실수를 다룸
> - boolean : true, false 값만 사용 가능하며 참 거짓 판단
> - char : 문자 하나를 다룰 때 사용 (''를 사용하여 감싸야 함)
> - String : 문자열을 다룸 (""를 사용해야함)

---

### 리터럴

[코드](#변수-타입)와 같이 개발자가 직접 적은 100, 10.5와 같은 고정된 값을 리터럴(literal)이라고 한다.

> 정수 리터럴, 실수 리터럴, 불리언 리터럴, ...

**변수의 값은 변할 수 있지만, 리터럴은 개발자가 직접 입력한 고정 값이므로 변하지 않는다.**

---

## 변수 타입2

```java
package variable;

public class Var9 {
  public static void main(String[] args) {
    byte b = 127;
    short s = 32767;
    int i = 21454545;

    long l = 9292929292929292L;

    //실수
    float f = 10.0f;
    double d = 10.0;
  }
};
```

---

### 표현할 수 있는 숫자의 범위와 차지하는 메모리의 공간

**정수형**

- byte : -127 ~ 127 (1byte, 2^{8})
- short : 2byte, 2^{16}
- int : 4byte, 2^{32}
- long : 8byte, 2^{64}

**실수형**

- float : 대략 7자리 정밀도 (4byte, 2^{32})
- double : 대략 15자리 정밀도 (8byte, 2^{64})

**기타**

- boolean : true, false (1byte)
- char : 문자 하나 (1byte)
- String : 문자열 (길이에 따라 달라짐)

---

### 리터럴 타입 지정

- 정수 리터럴은 int를 기본으로 함
  - 20억을 넘어가면 long으로 변경해야함
- 실수 리터럴은 double을 기본으로 함
  - float형을 사용하려면 f를 붙여야함

---

## 변수 명명 규칙

**규칙**

1. 변수 이름은 숫자로 시작할 수 없다.
2. 이름에는 공백이 포함될 수 없다.
3. 자바의 예약어를 이름으로 사용할 수 없다. (int, class, ...)
4. 변수 이름에는 영문자, 숫자, 달러기호, 밑줄만 사용 가능

**관례**
소문자로 시작하는 낙타 표기법

- 변수 이름은 소문자로 시작하는 것이 일반적.
  - EX> orderDetail, myAccount, ...

> 요약
> 클래스는 대문자로 시작, 나머지는 소문자로 시작

---
