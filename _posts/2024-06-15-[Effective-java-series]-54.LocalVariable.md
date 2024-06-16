---
layout: post
title: Effective java
categories: [EFFECTIVE_JAVA]
---

# 지역변수 범위 최소화

지역 변수 범위를 줄이는 기법은 '가장 처음에 쓸 때 선언하기'가 있다. 그러나 미리 선언하면 코드가 어수선해지 쉽상이다. 또한 너무 고민 없이 선언하면 변수가 쓰이는
범위보다 너무 앞서 선언하게 되거나, 다 쓴 뒤에도 살아있게 될 수 있다. 또한, 지역변수는 대부분 선언과 동시에 초기화를 해야하는데 초기화 정보가 모자라도 선언을 하는
일을 맞닥뜨리게 될 수 있다.

## while vs for
for가 낫다. while은 안에서 사용하는 변수를 바깥에서 선언해야할 때가 있다. 그러면 그 이름의 변수를 다른 의미로 아래에서 또 사용해야 한다면?
실수하기 쉽다. for는 for 블록에서 선언하므로 크게 문제가 되지 않는다.

```java
Iterator<Integer> i1 = c1.iterator();
while( i1.hasNext() ) {...}


Iterator<Integer> i2 = c2.iterator();
while( i1.hasNext() ) {...} //이러면 안돌고 지나간다.

```


## 메소드를 잘게 쪼개기
메소드를 기능 단위로 단일 책임을 지우면 그게 최고다. 또한 이러면 메소드 단위가 작아져 지역 범위를 최소화할 수 있다.