---
layout: pattern
title: Singleton
folder: singleton
permalink: /patterns/singleton/
categories: Creational
tags:
 - Java
 - Gang Of Four
 - Difficulty-Beginner
---

## 의도
클래스에 인스턴스가 하나만 있는지 확인하고 글로벌 포인트를 제공합니다.
접속할 수 있습니다.


## 설명
실생활 예문

> 마법사들이 마법을 연구하는 아이보리색 타워가 있다 하자. 같은 마법에 걸린 아이보리색 타워는 항상 마법사들에게 사용된다. 여기서 아이보리색 타워는 싱글톤이다.

간략

> 특정한 클래스에서 객체는 하나만 형성되도록 한다.

위키피디아에 의하면

> 소프트웨어 엔지니어링에서 싱글톤 패턴은 한 객체에 대한 클래스의 인스턴스 생성을 금지한다. 이것은 정확히 한가지의 객체가 시스템에 대한 행동들을 조직화 할 때 유용하다.

**프로그램 예시**

Joshua Bloch, Effective Java 2nd Edition p.18

> 싱글 엘리먼트 에넘 타입은 싱글톤을 구현하는 가장 좋은 방법이다.

```java
public enum EnumIvoryTower {
  INSTANCE;
}
```

그리고 나서 사용하기 위해서.

```java
EnumIvoryTower enumIvoryTower1 = EnumIvoryTower.INSTANCE;
EnumIvoryTower enumIvoryTower2 = EnumIvoryTower.INSTANCE;
assertEquals(enumIvoryTower1, enumIvoryTower2); // true
```

## 적용 가능성
이럴때 Singleton 패턴 사용합니다

* 클래스에 정확히 한가지의 인스턴스가 필요로 할 때, 그리고 잘 알려진 접근점에서 반드시 클라이언트들에게 접근성을 주어야 한다.
* 하위 분류에 의해 유일한 인스턴스가 확장되어야 하고, 클라이언트는 코드를 수정하지 않고 확장된 인스턴스를 사용할 수 있어야 하는 경우.

## 일반적인 사용 사례

* 로깅 클래스
* 데이터베이스에 연결을 관리할 때
* 파일 매니저

## 예제

* [java.lang.Runtime#getRuntime()](http://docs.oracle.com/javase/8/docs/api/java/lang/Runtime.html#getRuntime%28%29)
* [java.awt.Desktop#getDesktop()](http://docs.oracle.com/javase/8/docs/api/java/awt/Desktop.html#getDesktop--)
* [java.lang.System#getSecurityManager()](http://docs.oracle.com/javase/8/docs/api/java/lang/System.html#getSecurityManager--)


## 결과

* Violates Single Responsibility Principle (SRP) by controlling their own creation and lifecycle.
* Encourages using a global shared instance which prevents an object and resources used by this object from being deallocated.     
* Creates tightly coupled code. The clients of the Singleton become difficult to test.
* Makes it almost impossible to subclass a Singleton.

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Effective Java (2nd Edition)](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683)
