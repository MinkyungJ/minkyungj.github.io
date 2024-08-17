---
title: Remind Java3 - Operator
tags: [Java]
date: 2024-08-17 22:00 +0900
categories: [Java, Inflearn]
toc: true
---

## 연산자 종류
- 산술 연산자 : +, -, *, /, %
- 증감 연산자 : ++, --
- 비교 연산자 : ==, !=, >, <, >=, <=
- 논리 연산자 : &&, ||, !
- 대입 연산자 : =, +=, -=, *=, %=
- 삼항 연산자 : ? :

---

### 연산자와 피연산자

``` Number
3 + 4
A + B
```

- 연산자 : 연산 기호 : +, -
- 피연산자 : 연산 대상 : 3, 4, a, b

---

## 산술 연산자

```Java
public operator;

public class Operator1 {
  public static void main(String[] args) {
    int a = 5;
    int b = 2;

    int sum = a + b;
    System.out.println("a + b = " + sum);

    int diff = a - b;
    System.out.println("a - b = " + diff);

    int multi = a * b;
    System.out.println("a * b = " + multi);

    int div = a / b;
    System.out.println("a / b = " + div);

    int mod = a % b;
    System.out.println("a % b = " + mod);
  }
}
```

> 나누기 경우에, 5 / 2 = 2.5이지만 결과는 소수점이 제거된 2가 나온다.
> - 자바에서 같은 int형끼리 계산하면 결과도 int형을 사용한다.

---

## 문자열 더하기

```Java
public operator;

public class Operator2 {
  public static void main(String[] args) {
    
    String result1 = "hello " + "world";
    System.out.println(result1);

    String s1 = "string1";
    String s2 = "string2";
    String result2 = s1 + s2;
    System.out.println(result2);

    String result3 = "a + b =" + 10;
    System.out.println(result3);

    int num = 20;
    String str = "a + b =";
    String result4 = str + num;
    System.out.println(result4);
  }
}

//실행 결과
// hello world
// string1string2
// a + b = 10
// a + b = 20

```