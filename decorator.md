---
layout: pattern
title: Decorator
folder: decorator
permalink: /patterns/decorator/
categories: Structural
tags:
 - Java
 - Gang Of Four
 - Difficulty-Beginner
---

## 다른 명칭
Wrapper

## 의도
개체에 대한 추가 책임을 동적으로 연결합니다.
디코레이터는 기능 확장을 위한 하위 분류에 대한 유연한 대안을 제공합니다.

## 설명

실생활 예문

> 인근 야산에 성난 트롤이 살고 있습니다. 보통은 맨손에 쓰지만 때로는 흉기를 가지고 있기도 합니다. 트롤을 무장시키려면 새로운 트롤을 만들 필요가 없고 적합한 무기로 동적으로 장식할 필요가 있습니다.

간략

> 데코레이터 패턴을 사용하면 실행 시 객체의 동작을 실내 장식용 클래스의 객체로 동적으로 변경할 수 있습니다.

위키피디아에 의하면

> 객체 지향 프로그래밍에서 실내 장식자 패턴은 동일한 클래스의 다른 객체의 동작에 영향을 주지 않고 정적 또는 동적으로 개별 객체에 동작을 추가할 수 있는 설계 패턴입니다. 실내 장식자 패턴은 종종 단일 책임 원칙을 준수하는 데 유용합니다. 기능성을 고유한 관심 영역으로 세분화할 수 있기 때문입니다.

**프로그램 예시**

트롤의 예를 들어보겠습니다. 우선 트롤 인터페이스를 구현하는 간단한 트롤이 있습니다.

```java
public interface Troll {
  void attack();
  int getAttackPower();
  void fleeBattle();
}

public class SimpleTroll implements Troll {

  private static final Logger LOGGER = LoggerFactory.getLogger(SimpleTroll.class);

  @Override
  public void attack() {
    LOGGER.info("The troll tries to grab you!");
  }

  @Override
  public int getAttackPower() {
    return 10;
  }

  @Override
  public void fleeBattle() {
    LOGGER.info("The troll shrieks in horror and runs away!");
  }
}
```

다음은 트롤을 위한 클럽을 추가하고자 합니다. 실내장식을 이용해서 역동적으로 할 수 있습니다.

```java
public class ClubbedTroll implements Troll {

  private static final Logger LOGGER = LoggerFactory.getLogger(ClubbedTroll.class);

  private Troll decorated;

  public ClubbedTroll(Troll decorated) {
    this.decorated = decorated;
  }

  @Override
  public void attack() {
    decorated.attack();
    LOGGER.info("The troll swings at you with a club!");
  }

  @Override
  public int getAttackPower() {
    return decorated.getAttackPower() + 10;
  }

  @Override
  public void fleeBattle() {
    decorated.fleeBattle();
  }
}
```

여기 트롤이 있습니다.

```java
// simple troll
Troll troll = new SimpleTroll();
troll.attack(); // The troll tries to grab you!
troll.fleeBattle(); // The troll shrieks in horror and runs away!

// change the behavior of the simple troll by adding a decorator
Troll clubbedTroll = new ClubbedTroll(troll);
clubbedTroll.attack(); // The troll tries to grab you! The troll swings at you with a club!
clubbedTroll.fleeBattle(); // The troll shrieks in horror and runs away!
```

## 적용 가능성
이럴때 Decorator 패턴을 사용합니다.

* 개별 객체에 동적이고 투명하게 책임을 추가하는 것, 즉 다른 객체에 영향을 주지 않는 것입니다.
* 철회할 수 있는 책임에 대하여
* 하위 분류에 의한 확장이 비실용적인 경우. 때때로 많은 수의 독립적인 확장이 가능하고 모든 조합을 지원하기 위해 하위 클래스의 폭발을 일으킬 수 있다. 또는 클래스 정의가 숨겨지거나 하위 분류에 사용할 수 없음

## 튜토리얼
* [Decorator 패턴 튜토리얼](https://www.journaldev.com/1540/decorator-design-pattern-in-java-example)

## 예제
 * [java.io.InputStream](http://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html), [java.io.OutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html),
 [java.io.Reader](http://docs.oracle.com/javase/8/docs/api/java/io/Reader.html) and [java.io.Writer](http://docs.oracle.com/javase/8/docs/api/java/io/Writer.html)
 * [java.util.Collections#synchronizedXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#synchronizedCollection-java.util.Collection-)
 * [java.util.Collections#unmodifiableXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#unmodifiableCollection-java.util.Collection-)
 * [java.util.Collections#checkedXXX()](http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#checkedCollection-java.util.Collection-java.lang.Class-)


## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Functional Programming in Java: Harnessing the Power of Java 8 Lambda Expressions](http://www.amazon.com/Functional-Programming-Java-Harnessing-Expressions/dp/1937785467/ref=sr_1_1)
* [J2EE Design Patterns](http://www.amazon.com/J2EE-Design-Patterns-William-Crawford/dp/0596004273/ref=sr_1_2)
