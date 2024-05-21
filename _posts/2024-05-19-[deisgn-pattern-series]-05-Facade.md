from [Dictionary - Facade](https://github.com/newkayak12/Dictionary/blob/master/java/designPattern/05.Facade.md)


# Facade
퍼사드 패턴(Facade Pattern)은 사용하기 복잡한 클래스 라이브러리에 대해 사용하기 편하게 간편한 인터페이스(API)를 구성하기 위한 구조 패턴이다.
이처럼 파사드는 복잡하게 얽혀 있는 것을 정리해서 사용하기 편한 인터페이스를 제공하려는 목적이라고 생각하면 된다.

>
> Facade라는 단어의 뜻은 건축물의 정면을 의미한다.
> 건축물의 정면은 보통 건축물의 이미지와 건축 의도를 나타내기 때문에 오래 전부터 특별한 디자인을 적용하여 의미를 부여했다.
> 이처럼 건축물 정면만 봐도 이 건물이 어떤 목적을 하는지 단번에 알수 있다는 특징을 차용하여 명명 지은 것이다.
> 

![](/assets/img/facade.png)

- Facade : 서브시스템 기능을 편리하게 사용할 수 있도록 하기 위해 여러 시스템과 상호 작용하는 복잡한 로직을 재정리해서 높은 레벨의 인터페이스를 구성한다. Facade 역할은 서브 시스템의 많은 역할에 대해 ‘단순한 창구’가 된다. 클라이언트와 서브시스템이 서로 긴밀하게 연결되지 않도록 한다.
- Additional Facade : 퍼사드 클래스는 반드시 한개만 존재해야 한다는 규칙같은 건 없다. 연관 되지 않은 기능이 있다면 얼마든지 퍼사드 2세로 분리한다. 이 퍼사드 2세는 다른 퍼사드에서 사용할 수도 있고 클라이언트에서 직접 접근할 수도 있다.
- SubSystem(하위 시스템) : 수십 가지 라이브러리 혹은 클래스들
- Client : 서브 시스템에 직접 접근하는 대신 Facade를 사용한다.

퍼사드 패턴은 전략 패턴이나 팩토리 패턴과 같은 여타 다른 디자인 패턴과는 다르게 클래스 구조가 정형화 되지 않은 패턴이다.
반드시 클래스 위치는 어떻고 어떤 형식으로 위임을 해야되고 이런것이 없다. 그냥 퍼사드 클래스를 만들어 적절히 기능 집약해주는 논리라고 생각하면 된다.

![](/assets/img/flyWeight2.png)

## 재귀적 Facade 패턴의 적용
재귀적 퍼사드란 Additional Facade 를 말하는 것이다. 예를 들어 다수의 클래스, 다수의 패키지를 포함하고 있는 큰 시스템에 요소 마다 Facade 패턴을 여기 저기 적용하고 다시 그 Facade를 합친 Facade를 만드는 식으로,
퍼사드를 재귀적으로 구성하면 시스템은 보다 편리하게 된다. 이처럼 퍼사드는 한 개만 있으라는 법은 없으며 필요에 의하면 얼마든지 늘려서 의존할 수 있다.

## 특징
### 사용 시기
- 시스템이 너무 복잡할때
- 그래서 간단한 인터페이스를 통해 복잡한 시스템을 접근하도록 하고 싶을때
- 시스템을 사용하고 있는 외부와 결합도가 너무 높을 때 의존성 낮추기 위할때

### 장점
- 하위 시스템의 복잡성에서 코드를 분리하여, 외부에서 시스템을 사용하기 쉬워진다.
- 하위 시스템 간의 의존 관계가 많을 경우 이를 감소시키고 의존성을 한 곳으로 모을 수 있다.
- 복잡한 코드를 감춤으로써, 클라이언트가 시스템의 코드를 모르더라도 Facade 클래스만 이해하고 사용 가능하다

>
> 외부에서 내부 로직을 직접 사용하기 때문에 내부 로직의 구조를 변경한다고 하거나 파라미터나 리턴값 등을 변경할 경우 직접적으로 영향을 받아 수정이 힘들거나
> 불가능한 경우가 종종 있다. 하지만 중간에 매개체 역할을 해주는 퍼사드 객체가 있기 때문에 실제 내부 로직이 어떻게 변경이 되더라도 상관이 없어지므로 의존성이 감소된다.
> 

### 단점
- 퍼사드가 앱의 모든 클래스에 결합된 최상위 객체가 될 수 있다
- 퍼사드 클래스 자체가 서브시스템에 대한 의존성을 가지게 되어 의존성을 완전히는 피할 수는 없다.