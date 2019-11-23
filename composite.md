---
layout: pattern
title: Composite
folder: composite
permalink: /patterns/composite/
categories: Structural
tags:
 - Java
 - Gang Of Four
 - Difficulty-Intermediate
---

## 의도
객체를 트리 구조로 컴파일 하여 전체의 계층 구조를 표시한다. 합성물은 클라이언트가 각자의 개체와 구성을 균등하게 처리할 수 있게 한다.

## 설명

실생활 예시

> 모든 문장들은 문자가 차례대로 구성되어 있다. 이 object 들은 각각 출력할 수 있고 문장처럼 앞이나 뒤에도 출력할 수 있습니다. 문장들은 항상 완전한 정지 상태로 끝나야 하며 단어 앞에는 항상 공간이 있어야 한다.

간략

> 복합 패턴을 통해서 고객은 개별 객체를 동등하게 취급할 수 있다.

위키피디아에 의하면

> 소프트웨어 엔지니어링에서 복합 패턴은 분할 설계 패턴입니다. 복합 패턴은 개체 그룹이 개체의 단일 인스턴스와 동일한 방식으로 처리되어야 함을 설명합니다. 복합물의 목적은 오브젝트를 트리 구조로 합성하여 전체 계층 구조를 나타내는 것이다. 복합 패턴을 구현하면 클라이언트는 개별 객체와 구성을 균일하게 처리할 수 있다.

**프로그램 예시**

위에서 본 문장을 예로 들자면 여기 기본 클래스와 인쇄 가능한 여러 종류가 있다.

```java
public abstract class LetterComposite {

  private List<LetterComposite> children = new ArrayList<>();

  public void add(LetterComposite letter) {
    children.add(letter);
  }

  public int count() {
    return children.size();
  }

  protected void printThisBefore() {
  }

  protected void printThisAfter() {
  }

  public void print() {
    printThisBefore();
    children.forEach(LetterComposite::print);
    printThisAfter();
  }
}

public class Letter extends LetterComposite {

  private char character;

  public Letter(char c) {
    this.character = c;
  }

  @Override
  protected void printThisBefore() {
    System.out.print(character);
  }
}

public class Word extends LetterComposite {

  public Word(List<Letter> letters) {
    letters.forEach(this::add);
  }

  public Word(char... letters) {
    for (char letter : letters) {
      this.add(new Letter(letter));
    }
  }

  @Override
  protected void printThisBefore() {
    System.out.print(" ");
  }
}

public class Sentence extends LetterComposite {

  public Sentence(List<Word> words) {
    words.forEach(this::add);
  }

  @Override
  protected void printThisAfter() {
    System.out.print(".");
  }
}
```

그러면 우리는 메시지를 전달해줄 메신저가 있다.

```java
public class Messenger {

  LetterComposite messageFromOrcs() {

    var words = List.of(
        new Word('W', 'h', 'e', 'r', 'e'),
        new Word('t', 'h', 'e', 'r', 'e'),
        new Word('i', 's'),
        new Word('a'),
        new Word('w', 'h', 'i', 'p'),
        new Word('t', 'h', 'e', 'r', 'e'),
        new Word('i', 's'),
        new Word('a'),
        new Word('w', 'a', 'y')
    );

    return new Sentence(words);

  }

  LetterComposite messageFromElves() {

    var words = List.of(
        new Word('M', 'u', 'c', 'h'),
        new Word('w', 'i', 'n', 'd'),
        new Word('p', 'o', 'u', 'r', 's'),
        new Word('f', 'r', 'o', 'm'),
        new Word('y', 'o', 'u', 'r'),
        new Word('m', 'o', 'u', 't', 'h')
    );

    return new Sentence(words);

  }

}
```

그리고 그것은 다음과 같이 사용될 수 있다.

```java
var orcMessage = new Messenger().messageFromOrcs();
orcMessage.print(); // Where there is a whip there is a way.
var elfMessage = new Messenger().messageFromElves();
elfMessage.print(); // Much wind pours from your mouth.
```

## 적용 가능성
이럴때 컴퍼지트 패턴을 사용합니다

* 객체의 전체 계층 구조를 나타내려는 경우
* 고객이 객체의 구성과 개별 객체의 차이를 무시할 경우 클라이언트는 복합 구조의 모든 객체를 균일하게 처리한다

## 예제

* [java.awt.Container](http://docs.oracle.com/javase/8/docs/api/java/awt/Container.html) and [java.awt.Component](http://docs.oracle.com/javase/8/docs/api/java/awt/Component.html)
* [Apache Wicket](https://github.com/apache/wicket) component tree, see [Component](https://github.com/apache/wicket/blob/91e154702ab1ff3481ef6cbb04c6044814b7e130/wicket-core/src/main/java/org/apache/wicket/Component.java) and [MarkupContainer](https://github.com/apache/wicket/blob/b60ec64d0b50a611a9549809c9ab216f0ffa3ae3/wicket-core/src/main/java/org/apache/wicket/MarkupContainer.java)

## Credits

* [Design Patterns: Elements of Reusable Object-Oriented Software](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)
