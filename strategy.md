---
layout: pattern
title: Strategy
folder: strategy
permalink: /patterns/strategy/
categories: Behavioral
tags:
 - Java
 - Difficulty-Beginner
 - Gang Of Four
---

## 다른 명칭
Policy

## 의도
알고리즘 제품군을 정의하고 각 제품군을 캡슐화하여 생성 교환할 수 있는 전략은 알고리즘을 사용하는 클라이언트와 독립적으로 다르게 한다.

![alt text](./etc/strategy_1.png "Strategy")

## 적용 가능성
이럴때 Strategy 패턴을 사용합니다

* 많은 관련 수업들은 그들의 행동에서만 다릅니다. 전략은 여러 동작 중 하나를 클래스에 구성할 수 있는 방법을 제공합니다.
* 다른 종류의 알고리즘이 필요합니다. 예를 들어 서로 다른 공간/시간 절충을 반영하는 알고리즘을 정의할 수 있습니다. 이러한 변형이 알고리즘의 클래스 계층으로 구현될 때 전략을 사용할 수 있습니다.
* 알고리즘은 클라이언트가 알면 안 되는 데이터를 사용한다. 전략 패턴을 사용하여 복잡한 알고리즘별 데이터 구조 노출 방지
* 한 계급은 많은 행동을 정의하며, 이러한 행동들은 그 운영에서 복수의 조건부로 나타난다. 여러 조건 대신 관련 조건부 지점을 자체 전략 클래스로 이동

## 튜토리얼
* [Strategy 패턴 튜토리얼](https://www.journaldev.com/1754/strategy-design-pattern-in-java-example-tutorial)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
* [Functional Programming in Java: Harnessing the Power of Java 8 Lambda Expressions](http://www.amazon.com/Functional-Programming-Java-Harnessing-Expressions/dp/1937785467/ref=sr_1_1)
