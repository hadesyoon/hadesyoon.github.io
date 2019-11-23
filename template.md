---
layout: pattern
title: Template method
folder: template-method
permalink: /patterns/template-method/
categories: Behavioral
tags:
 - Java
 - Difficulty-Beginner
 - Gang Of Four
---

## 의도
작업에서 알고리즘의 골격을 정의하고 일부 단계를 하위 클래스로 연기합니다. 템플릿 방법을 사용하면 알고리즘의 구조를 변경하지 않고 하위 클래스가 알고리즘의 특정 단계를 재정의할 수 있습니다.

하위 클래스가 템플릿 메서드를 재정의하지 않도록 하려면 템플릿 메서드를 "최종"으로 선언해야 한다.

![alt text](./etc/template-method_1.png "Template Method")

## 적용 가능성
이럴때 템플렛 메소드를 사용합니다
* 알고리즘의 불변성 부분을 한 번 구현하고 이를 하위 클래스까지 남겨서 다양한 동작을 구현한다.
* 코드 복제를 방지하기 위해 하위 클래스 간의 공통 행동을 고려 및 현지화해야 하는 경우. Opdyke와 Johnson이 설명한 "일반화를 위한 재조사"의 좋은 예다. 먼저 기존 코드의 차이를 확인한 다음, 그 차이를 새로운 작업으로 구분하십시오. 마지막으로, 다른 코드를 이러한 새 작업 중 하나를 호출하는 템플릿 방법으로 교체하십시오.
* 하위 클래스 확장 제어. 특정 지점에서 "후크" 작업을 호출하여 해당 지점에서만 확장을 허용하는 템플릿 방법을 정의할 수 있음

## 튜토리얼
* [Template-method Pattern 튜토리얼](https://www.journaldev.com/1763/template-method-design-pattern-in-java)

## 예제
* [javax.servlet.GenericServlet.init](https://jakarta.ee/specifications/servlet/4.0/apidocs/javax/servlet/GenericServlet.html#init--): 
Method `GenericServlet.init(ServletConfig config)` calls the parameterless method `GenericServlet.init()` which is intended to be overridden in subclasses.
Method `GenericServlet.init(ServletConfig config)` is the template method in this example.

## Credits
* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
