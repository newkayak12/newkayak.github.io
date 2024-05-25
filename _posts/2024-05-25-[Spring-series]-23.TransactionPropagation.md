---
layout: post

categories: [SPRING]
---



from [Dictionary - Propagation](https://github.com/newkayak12/Dictionary/blob/master/spring/23.TransactionPropagation.md)


# Propagation

## 시작
트랜잭션은 하나의 Connection을 가져와 사용하다 닫는 사이에 일어난다. 
그러므로 JDBC에서 트랜잭션을 사용하려면 `auto-commit`을 `false`로 해야한다.

## 종료
`commit()`, `rollback()`을 호출할 때까지가 하나의 트랜잭션이 된다. 


## 전파
`@Transactional`의 장점은 여러 트랜잭션을 묶어서 커다란 하나의 트랜잭션 경계를 만들 수 있다. 이미 진행 중일 때 추가 트랜잭션을 어떻게 할지 결정하는 것이
`전파 속성(Propagation)`이라고 한다. 

## 물리/ 논리 트랜잭션
트랜잭션은 DB에서 제공하므로 커넥션 객체를 통해서 처리한다. 그래서 1개 트랜잭션 = 하나의 커넥션이라고 보며, 물리 트랜잭션이라고 부른다.
다만, 스프링 내부에서 트랜잭션 개념을 두고, 이를 하나의 논리 트랜잭션으로 보며 하나의 물리 트랜잭션 안에 여러 논리 트랜잭션이 있을 수도 있다. 

- 물리 트랜잭션 : 실제 DB에 적용되는 트랜잭션, 커넥션을 통해 커밋/롤백하는 단위
- 논리 트랜잭션 : 스프링이 트랜잭션 매니저를 통해서 처리하는 단위 

## 그래서
- 모든 논리 트랜잭션이 커밋되어야 물리 트랜잭션이 커밋됨
- 하나의 논리 트랜잭션이라도 롤백되면 물리 트랜잭션은 롤백


## 종류
1. REQUIRED
   - 의미 : 없으면 새로 만들어야 함 (기본 값)
   - 없다면 -> 새로 만듦
   - 있으면 -> 기존 트랜잭션에 참여
2. REQUIRED_NEW
   - 의미 : 항상 새로운 트랜잭션이 필요함
   - 없다면 -> 새로운 트랜잭션 생성
   - 있으면 -> 기존 트랜잭션 보류하고 새로운 트랜잭션 생성
3. SUPPORTS
   - 의미 : 트랜잭션이 있으면 지원 
   - 없다면 -> 트랜잭션이 없이 진행함
   - 있으면 -> 기존 트랜잭션에 참여
4. NOT_SUPPORTED
   - 의미 : 트랜잭션 지원하지 않음 
   - 없다면 -> 트랜잭션 없이 진행
   - 있으면 -> 기존 트랜잭션 보류시키고 트랜잭션 없이 진행함
5. MANDATORY
   - 의미 : 반드시 필요함
   - 없다면 -> throw IllegalTransactionStateException
   - 있으면 -> 기존 트랜잭션에 참여
6. NEVER
   - 의미 : 트랜잭션 사용하지 않음(기존 트랜잭션도 사용할 생각이 없음)
   - 없다면 -> 트랜잭션 없지 진행
   - 있으면 -> IllegalTransactionStateException 발생 
7. NESTED
   - 의미 : 중첩 트랜잭션 생성
   - 없다면 -> 새로운 트랜잭션 생성
   - 있으면 -> 중첩 트랜잭션 생성