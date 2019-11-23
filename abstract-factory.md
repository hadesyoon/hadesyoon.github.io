---
layout: pattern
title: Abstract Factory
folder: abstract-factory
permalink: /patterns/abstract-factory/
categories: Creational
tags:
 - Java
 - Gang Of Four
 - Difficulty-Intermediate
---

## 다른 명칭
Kit

## 의도
구체적으로 등급이 명시되지 않은 것에 대해 관련 또는 종속 제품군 생성을 위한 인터페이스 제공

## 설명
실생활 예문

> 왕국을 만들기 위해서는 공통적인 주제를 가진 물체가 필요하다. 엘벤 왕국은 엘벤 왕, 엘벤 성, 엘벤 군대가 필요한 반면, 오르크 왕국은 오르크 왕, 오르크 성, 오르크 군이 필요하다. 왕국에 있는 물건들 사이에는 의존성이 있다.

간략

> 공장의 공장, 개별적이지만 관련/의존적인 공장을 구체적인 등급을 지정하지 않고 하나로 묶는 공장을 말합니다

위키피디아에 의하면

> 추상적인 공장 패턴은 구체적인 클래스를 지정하지 않고 공통 테마를 가진 개별 공장 그룹을 캡슐화할 수 있는 방법을 제공합니다.

**프로그램 예시**

위의 왕국의 예를 번역하자면. 우선, 우리는 왕국의 사물들을 위한 인터페이스와 구현을 가지고 있습니다.

```java
public interface Castle {
  String getDescription();
}
public interface King {
  String getDescription();
}
public interface Army {
  String getDescription();
}

// Elven implementations ->
public class ElfCastle implements Castle {
  static final String DESCRIPTION = "This is the Elven castle!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}
public class ElfKing implements King {
  static final String DESCRIPTION = "This is the Elven king!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}
public class ElfArmy implements Army {
  static final String DESCRIPTION = "This is the Elven Army!";
  @Override
  public String getDescription() {
    return DESCRIPTION;
  }
}

// Orcish implementations similarly...

```

그럼 킹덤 공장에 대한 추상화와 구현이 있습니다.

```java
public interface KingdomFactory {
  Castle createCastle();
  King createKing();
  Army createArmy();
}

public class ElfKingdomFactory implements KingdomFactory {
  public Castle createCastle() {
    return new ElfCastle();
  }
  public King createKing() {
    return new ElfKing();
  }
  public Army createArmy() {
    return new ElfArmy();
  }
}

public class OrcKingdomFactory implements KingdomFactory {
  public Castle createCastle() {
    return new OrcCastle();
  }
  public King createKing() {
    return new OrcKing();
  }
  public Army createArmy() {
    return new OrcArmy();
  }
}
```

이제 우리는 추상적인 공장을 가지고 있습니다. 우리가 관련된 물건들로 가족을 만들 수 있도록 말이죠. 엘벤 왕국 공장은 엘벤 성, 왕과 군대 등을 만듭니다.

```java
var factory = new ElfKingdomFactory();
var castle = factory.createCastle();
var king = factory.createKing();
var army = factory.createArmy();

castle.getDescription();  // Output: This is the Elven castle!
king.getDescription(); // Output: This is the Elven king!
army.getDescription(); // Output: This is the Elven Army!
```

Now, we can design a factory for our different kingdom factories. In this example, we created FactoryMaker, responsible for returning an instance of either ElfKingdomFactory or OrcKingdomFactory.  
The client can use FactoryMaker to create the desired concrete factory which, in turn, will produce different concrete objects (Army, King, Castle).  
In this example, we also used an enum to parameterize which type of kingdom factory the client will ask for.

```java
public static class FactoryMaker {

  public enum KingdomType {
    ELF, ORC
  }

  public static KingdomFactory makeFactory(KingdomType type) {
    switch (type) {
      case ELF:
        return new ElfKingdomFactory();
      case ORC:
        return new OrcKingdomFactory();
      default:
        throw new IllegalArgumentException("KingdomType not supported.");
    }
  }
}

public static void main(String[] args) {
  var app = new App();

  LOGGER.info("Elf Kingdom");
  app.createKingdom(FactoryMaker.makeFactory(KingdomType.ELF));
  LOGGER.info(app.getArmy().getDescription());
  LOGGER.info(app.getCastle().getDescription());
  LOGGER.info(app.getKing().getDescription());

  LOGGER.info("Orc Kingdom");
  app.createKingdom(FactoryMaker.makeFactory(KingdomType.ORC));
  -- similar use of the orc factory
}
```


## 적용 가능성
이럴때 추상 메소드를 사용합니다

* 시스템은 제품이 생성, 구성 및 표현되는 방법과 독립적이어야 합니다.
* 시스템은 여러 제품군 중 하나로 구성되어야 합니다.
* 관련 제품 개체군은 함께 사용하도록 설계되었으며 이 제약 조건을 적용해야 합니다.
* 제품의 클래스 라이브러리를 제공하고, 제품 구현이 아닌 인터페이스만 공개하려고 합니다.
* 의존성의 수명은 개념적으로 소비자의 수명보다 짧습니다
* 특정 종속성을 구성하려면 런타임 값이 필요합니다
* 런타임에 가족으로부터 전화를 걸 제품을 결정하려고 합니다
* 종속성을 해결하려면 런타임에만 알려진 하나 이상의 매개 변수를 제공해야 합니다.
* 제품 간의 일관성이 필요할 때 사용합니다
* 프로그램에 새 제품 또는 제품군을 추가할 때 기존 코드를 변경하지 않습니다.
 
## 사용 사례:	

* 런타임에 FileSystemAcmeService 또는 DatabaseAcmeService 또는 NetworkAcmeService의 적절한 구현을 호출하도록 선택합니다.
* 유닛 테스트 케이스 쓰기가 훨씬 쉬워집니다.
* 다양한 OS에 대한 UI 도구입니다.

## 결과:

*java의 종속성 주입은 컴파일 시 발생할 수 있는 런타임 오류를 초래할 수 있는 서비스 클래스 종속성을 숨깁니다.
* 미리 정의된 개체를 생성할 때는 패턴이 좋지만 새 개체를 추가하는 것은 어려울 수 있습니다.
* 많은 새로운 인터페이스와 클래스가 패턴과 함께 도입되기 때문에 코드는 필요 이상으로 복잡해질 수 있습니다.

## 튜토리얼
* [추상메소드 튜토리얼](https://www.journaldev.com/1418/abstract-factory-design-pattern-in-java) 


## 예제

* [javax.xml.parsers.DocumentBuilderFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilderFactory.html)
* [javax.xml.transform.TransformerFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/transform/TransformerFactory.html#newInstance--)
* [javax.xml.xpath.XPathFactory](http://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/XPathFactory.html#newInstance--)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
