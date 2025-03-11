---
last_modified_at: '2025-03-11T19:10:06.678Z'
date: '2025-03-11T19:10:06.678Z'
---
# 디자인 패턴(Design Pattern)
> [!NOTE]  
> 소프트웨어 설계의 주어진 컨텍스트 내에서 공통적으로 발생하는 문제에 대해 일반적이고 재사용 가능한 솔루션

#### 디자인 패턴의 구성 요소
- 컨텍스트(Context)
    - 문제가 발생하는 여러 상황을 기술한다. 즉, 패턴이 적용될 수 있는 상황을 나타낸다. 경우에 따라서는 패턴이 유용하지 못한 상황을 나타내기도 한다.
- 문제(Problem)
    - 패턴이 적용되어 해결될 필요가 있는 여러 디자인 이슈들을 기술한다. 이떄 여러 제약 사항과 영향력도 문제 해결을 위해 고려해야 한다.
- 해결책(Solution)
    - 문제를 해결하도록 설계를 구성하는 요소들과 그 요소들 사이의 관계, 책임, 협력 관계를 기술한다. 해결은 반드시 구체적인 구현 방법이나 언어에 의존적이지 않으며 다양한 상황에 적용할 수 있는 일종의 템플릿이다.

#### 디자인 원칙
> 디자인 패턴은 객체 지향 프로그래밍의 주요 원칙들을 따른다. 

- 애플리케이션에서 달라지는 부분을 찾아내고, 달라지지않는 부분으로부터 분리시킨다.
- 구현(Concrete)이 아닌 인터페이스에 맞춰서 프로그래밍한다.
- 상속(Inheritance)보다는 합성(Composition)을 활용한다.
- 서로 상호작용하는 객체 사이에서 가능한 느슨하게 결합하는 디자인을 사용한다. = 느슨한 결합(Loose Coupling)
- 클래스는 확장에 대해서는 열려 있어야하지만, 코드 변경에 대해서는 닫혀있어야한다. = 개방/폐쇄 원칙(Open/Closed Principle)
- 정말 친한 친구하고만 얘기하라. = 최소 지식 원칙 (The Law of Demeter, LoD)
    - 모듈들 사이의 결합도를 줄여 코드의 품질을 높이는 것

- 추상화된 것에 의존하도록 만들어라. 구상 클래스에 의존하도록 만들지 않도록 한다. = 의존성 역전 원칙(Dependency-Inversion Principle, DIP)

- 어떤 클래스를 변경해야 하는 이유는 오직 단 하나 뿐이어야 한다. = 단일 책임 원칙(The Single Responsibility Principle, SRP)
    - 오직 하나의 책임만 가지고 있다.


## GoF 디자인 패턴의 분류 
- 생성 패턴(Creational Patterns)
- 구조 패턴(Structural Patterns)
- 행동 패턴(Behavioral Patterns)

### 생성 패턴(Creational Patterns) 
> 객체 생성에 관려된 패턴으로, 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공하는 패턴 

- 추상 팩토리(Abstract Factory)
- 빌더(Builder)
- 팩토리 메소드(Factory Method)
- 프로토타입(Prototype)
- 싱글턴(Singleton)

### 구조 패턴(Structural Patterns)
> 클래스나 객체를 조합해 더 큰 구조로 만들 수 있게 구성을 사용하는 패턴

- 어댑터(Adapter)
- 브릿지(Bridge)
- 컴포지트(Composite)
- 데커레이터(Decorator)
- 퍼사드(Facade)
- 플라이웨이트(Flyweight)
- 프록시(Proxy)

### 행위 패턴(Behavioral Patterns)
> 클래스와 객체들이 상호작용하는 방법과 책임 및 역할을 분담하는 방법을 다루는 패턴 

- 책임 연쇄(Chain of Responsibility)
- 커맨드(Command)
- 인터프리터(Interpreter)
- 중재자(Mediator)
- 이터레이터(Iterator)
- 메멘토(Memento)
- 옵저버(Observer)
- 상태(State)
- 전략(Strategy)
- 템플릿 메서드(Template Method)
- 방문자(Visitor)
