---
layout: post
title: Effective java
categories: [EFFECTIVE_JAVA]
---


# 상속보다는 컴포지션

상속은 코드 재사용의 기초지만 항상 최선은 아니다. 상위 - 하위 클래스를 모두 같은 프로그래머가 개발하면 안전하지만 다른 패키지의 구체 클래스를 상속하는 것은 
위험하다. 이는 캡슐화를 무력화하는 방법 중 하나다. 또, 상위 클래스가 어떻게 구현되느냐에 따라 하위 클래스에 이상 동작을 일으킬 수 있다.  예시로 상위 클래스가 자기 사용을 할 경우
내부 구현이 언제 바뀔지 몰라서를 들 수 있다. 

아니면 아예 재정의를 해서 상위 메소드 내용을 배제하는 방법도 있다. 이러면 상위 구현을 완전 다시 구현해야 해서 난이도가 급격하게 올라간다. 또한, 상위 메소드가
상위 private 필드를 사용하면 하위에서 접근할 방법이 없다는 것도 문제다. 결국 이러면 아예 새로 만드는 게 나을 수 있다.

우회로 비슷한 기능을 다른 이름 메소드로 만들었다고 쳐도 운 없에 상위에서 같은 시그니쳐로 메소드를 만들면 결국 override가 되어버린다.
결국 어떻게 해도 상위 클래스를 상속 받는 것은 문제의 소지가 있다. 추가적으로 상속은 하위에서도 그 결함을 승계하는 문제도 있다.

차라리 새로운 클래스를 만들고 상위 클래스를 새로 만든 클래스의 private 필드로 두는게 나을 수도 있다. 이런 클래스를 래퍼 클래스, 기능을 덧씌운다고 해서 
데코레이터 패턴(DecoratorPattern), 넓게는 위임(Delegate)패턴이라고 부른다. (참고로 내부 객체에 자신의 참조를 넘기는 경우 위임에 해당한다.)

래퍼클래스라고 아예 단점이 없는건 아니다 콜백 처리를 할 수 없다는 것이 문제다. 상위는 래퍼 객체의 this를 알 수 없다. 