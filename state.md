---
layout: pattern
title: State
folder: state
permalink: /patterns/state/
categories: Behavioral
tags:
 - Java
 - Difficulty-Intermediate
 - Gang Of Four
---

## 다른 명칭
Objects for States

## 의도
Allow an object to alter its behavior when its internal state
changes. The object will appear to change its class.

![alt text](./etc/state_1.png "State")

## 적용 가능성
이럴때 스테이트 패턴을 사용합니다

* 오브젝트의 행동이 그 상태에 의존하고, 그리고 행동을 상태에 따른 런타임 때에 반드시 바꿔야 할 때
* 조작은 객체의 상태에 따른 크고, 다수 참가의 조건적인 서술을 갖는다. 이 상태는 보통 한가지 혹은 더 많은 열거된 항수에 의해 나타내어진다. 종종, 몇몇의 조작은 같은 조건적인 구조를 내포할 것이다. 스테이트 패턴은 각각의 조건적인 가지를 다른 클래스에 넣을 것이다. 이는 당신이 객체의 상태를 타에 의존하지 않는 객체이며 다른 객체와 독립되도록 다룰 수 있게 한다.

## 예제

* [javax.faces.lifecycle.Lifecycle#execute()](http://docs.oracle.com/javaee/7/api/javax/faces/lifecycle/Lifecycle.html#execute-javax.faces.context.FacesContext-) controlled by [FacesServlet](http://docs.oracle.com/javaee/7/api/javax/faces/webapp/FacesServlet.html), the behavior is dependent on current phase of lifecycle.
* [JDiameter - Diameter State Machine](https://github.com/npathai/jdiameter/blob/master/core/jdiameter/api/src/main/java/org/jdiameter/api/app/State.java)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
