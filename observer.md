---
layout: pattern
title: Observer
folder: observer
permalink: /patterns/observer/
categories: Behavioral
tags:
 - Java
 - Difficulty-Beginner
 - Gang Of Four
 - Reactive
---

## 다른 명칭
Dependents, Publish-Subscribe

## 의도
개체 간의 일대다 종속성을 정의하여 개체 간 종속성을 정의합니다.
개체의 상태가 변경되고 모든 종속 항목이 자동으로 업데이트됩니다.

![alt text](./etc/observer.png "Observer")

## 적용 가능성
이럴때 Observer 패턴을 사용합니다

* 추상화가 두 가지 측면을 가지고 있을 때, 하나는 다른 것에 의존합니다. 이러한 측면을 개별 객체에 캡슐화하면 독립적으로 변경하고 재사용할 수 있습니다.
* 한 객체에 대한 변경이 다른 객체를 변경해야 하는 경우, 그리고 얼마나 많은 객체를 변경해야 하는지 알 수 없습니다.
* 개체가 이러한 개체가 누구인지 추정하지 않고 다른 개체에게 통지할 수 있어야 하는 경우. 즉, 이 물체들이 단단히 결합되는 것을 원하지 않는다.

## 일반적인 사용 사례

* 한 개체에서 변경하면 다른 개체의 변경으로 이어진다.

## 예제

* [java.util.Observer](http://docs.oracle.com/javase/8/docs/api/java/util/Observer.html)
* [java.util.EventListener](http://docs.oracle.com/javase/8/docs/api/java/util/EventListener.html)
* [javax.servlet.http.HttpSessionBindingListener](http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpSessionBindingListener.html)
* [RxJava](https://github.com/ReactiveX/RxJava)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Java Generics and Collections](http://www.amazon.com/Java-Generics-Collections-Maurice-Naftalin/dp/0596527756/)
