---
layout: pattern
title: Command
folder: command
permalink: /patterns/command/
categories: Behavioral
tags:
 - Java
 - Gang Of Four
 - Difficulty-Intermediate
 - Functional
---

## 다른 명칭
Action, Transaction

## 의도
요청을 개체로 캡슐화하여 사용할 수 있습니다. 다른 요청, 대기열 또는 로그 요청을 가진 클라이언트를 매개 변수화합니다. 실행 취소할 수 있는 작업을 지원합니다.
![alt text](./etc/command.png "Command")

## 적용 가능성
이럴때 Command 패턴을 사용합니다

* 수행할 작업을 통해 객체를 매개변수화한다. 콜백 기능, 즉 나중에 불러야 할 곳에 등록되어 있는 기능을 절차적인 언어로 파라미터화를 표현할 수 있다. 명령은 콜백에 대한 객체 지향적인 대체물이다.
* 다양한 시간에 요청을 지정, 대기열 및 실행합니다. 명령 개체는 원래 요청과 무관하게 수명을 가질 수 있습니다. 요청 수신기를 주소 공간과 무관하게 나타낼 수 있는 경우 요청에 대한 명령 개체를 다른 프로세스로 전송하고 요청을 수행할 수 있습니다.
* 지원 취소. 명령의 실행 작업은 명령 자체의 효과를 반전시키기 위한 상태를 저장할 수 있다. 명령 인터페이스는 실행하기 위한 이전 호출의 효과를 반전시키는 추가 실행 취소 작업이 있어야 한다. 실행된 명령은 기록 목록에 저장된다. 실행 및 실행 취소는 각각 실행 취소와 실행을 호출하여 이 목록을 앞뒤로 통과시킴으로써 수행된다.
* 시스템 충돌 시 다시 적용할 수 있도록 로깅 변경 지원 로드 및 저장 작업으로 명령 인터페이스를 강화하면 변경 사항의 영구 로그를 유지할 수 있다. 충돌에서 복구하려면 Disk에서 기록된 명령을 다시 로드하고 실행 작업으로 다시 실행해야 함
* 원시적 운용을 기반으로 하는 상위 수준의 운영 중심으로 시스템을 구성한다. 이러한 구조는 거래를 지원하는 정보시스템에서 흔히 볼 수 있다. 트랜잭션은 데이터에 대한 일련의 변경 사항을 캡슐화한다. 명령 패턴은 거래를 모델링하는 방법을 제공한다. 명령은 공통 인터페이스를 가지므로 모든 트랜잭션을 동일한 방식으로 호출할 수 있다. 또한 이러한 패턴으로 인해 새로운 트랜잭션으로 시스템을 쉽게 확장할 수 있다.

## 일반적인 사용 사례

* 요청 기록을 보관합니다.
* 콜백 기능을 구현합니다.
* 실행 취소 기능을 실행합니다.

## 예제

* [java.lang.Runnable](http://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html)
* [org.junit.runners.model.Statement](https://github.com/junit-team/junit4/blob/master/src/main/java/org/junit/runners/model/Statement.java)
* [Netflix Hystrix](https://github.com/Netflix/Hystrix/wiki)
* [javax.swing.Action](http://docs.oracle.com/javase/8/docs/api/javax/swing/Action.html)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
