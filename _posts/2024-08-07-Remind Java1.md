---
title: Remind Java1
tags: [Java]
date: 2024-08-07 22:00 +0900
categories: [Java, Inflearn]
toc: true
---

## 자바 프로그램 실행


**Hello Java**

```java
public class HelloJava {

    public static void main(String[] args) {
        System.out.println("hello java");
    }
}
```

### 실행 결과

```java
public class HelloJava
```
- HelloJava = 클래스(class)
- 파일명은 클래스 이름과 같아야 한다.
- **{}** 블록으로 클래스의 시작과 끝 나타낸다.

```java
public static void main(String[] args)
```
- **main method**
-  자바는 main(String[] args) method를 찾아서 프로그램을 시작한다.
- main = 프로그램의 시작점
- - **{}** 블록으로 클래스의 시작과 끝 나타낸다.

```java
System.out.println("hello java");
```
- System.out.println() = 값을 콘솔에 출력하는 기능
- "hello java" : 문자열 사용시, ""사용

---

## ❗️ Java의 컴파일과 실행

자바 프로그램은 **컴파일, 실행 단계**를 거친다.
- [자바 소스 코드](#자바-프로그램-실행)와 같은 코드는 개발자가 작성.
- 자바 컴파일러를 사용하여 소스 코드 **컴파일**
  - 자바가 제공하는 **javac** 프로그램 사용
  - .java -> .class 파일 생성됨
  - 자바 소스 코드 -> byte 코드로 변환 : 빠른 실행을 위한 최적화 및 문법 오류 검출
- 자바 프로그램 **실행**
  - 자바가 제공하는 **java** 프로그램 사용
  - JVM(자바 가상 머신)이 실행되고 프로그램 작동