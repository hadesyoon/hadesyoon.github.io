---
layout: pattern
title: Factory Method
folder: factory-method
permalink: /patterns/factory-method/
categories: Creational
tags:
 - Java
 - Difficulty-Beginner
 - Gang Of Four
---

## 다른 명칭
Virtual Constructor

## 의도
개체를 생성하기 위한 인터페이스를 정의하지만 하위 클래스는 허용합니다.
인스턴스화할 클래스를 결정합니다. 공장 방법을 사용하면 클래스가 인스턴스화를 하위 클래스로 연기할 수 있습니다.

## 설명
실생활 예문

> 블랙스미스는 무기를 제조합니다. 엘프는 엘비쉬 무기를, 오르크는 오르크 무기를 필요로 합니다. 당면한 고객에 따라 올바른 유형의 대장장이가 소환됩니다.

간략

> 인스턴스화 논리를 하위 클래스에 위임할 수 있는 방법을 제공합니다.

위키피디아에 의하면

> 클래스 기반 프로그래밍에서 공장 방법 패턴은 생성될 개체의 정확한 클래스를 지정하지 않고도 공장 방법을 사용하여 개체 생성 문제를 처리하는 창조적 패턴입니다. 이는 인터페이스에 지정되어 하위 클래스에 의해 구현된 공장 방법을 호출하거나, 생성자를 호출하는 대신 파생 클래스에 의해 선택적으로 재정의된 기본 클래스에 구현하여 개체를 생성하는 방식으로 수행됩니다.

 **프로그램 예시**

우리 대장장이의 예를 들자면요. 우선, 우리는 대장간 인터페이스와 그것을 위한 몇 가지 구현

```java
public interface Blacksmith {
  Weapon manufactureWeapon(WeaponType weaponType);
}

public class ElfBlacksmith implements Blacksmith {
  public Weapon manufactureWeapon(WeaponType weaponType) {
    return ELFARSENAL.get(weaponType);
  }
}

public class OrcBlacksmith implements Blacksmith {
  public Weapon manufactureWeapon(WeaponType weaponType) {
    return ORCARSENAL.get(weaponType);
  }
}
```

이제 고객이 오면 올바른 유형의 대장장이가 소환되고 요청된 무기가 제조됩니다.

```java
Blacksmith blacksmith = new ElfBlacksmith();
blacksmith.manufactureWeapon(WeaponType.SPEAR);
blacksmith.manufactureWeapon(WeaponType.AXE);
// Elvish weapons are created
```

## 적용 가능성
이럴때 팩토리 메소드를 사용합니다

* 클래스는 생성해야 하는 개체 클래스를 예상할 수 없습니다.
* 클래스는 하위 클래스에서 자신이 생성하는 개체를 지정합니다.
* 클래스는 여러 도우미 하위 클래스 중 하나에 대한 책임을 위임하며, 어떤 도우미 하위 클래스가 위임인지에 대한 지식을 현지화하려고 합니다.

## 사용 사례

* [java.util.Calendar](http://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#getInstance--)
* [java.util.ResourceBundle](http://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-)
* [java.text.NumberFormat](http://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getInstance--)
* [java.nio.charset.Charset](http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html#forName-java.lang.String-)
* [java.net.URLStreamHandlerFactory](http://docs.oracle.com/javase/8/docs/api/java/net/URLStreamHandlerFactory.html#createURLStreamHandler-java.lang.String-)
* [java.util.EnumSet](https://docs.oracle.com/javase/8/docs/api/java/util/EnumSet.html#of-E-)
* [javax.xml.bind.JAXBContext](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/JAXBContext.html#createMarshaller--)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
