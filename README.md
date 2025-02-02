# inflearn-querydsl
## 커리큘럼 
### 섹션 1. Querydsl 소개
- 소개
- 강의 자료
---
### 섹션 2. 프로젝트 환경설정
- 프로젝트 생성
- Querydsl 설정과 검증
  - setting 에서 intellij로 build 설정하면 Q클래스 못찾는 문제 있음
- 라이브러리 살펴보기
- H2 데이터베이스 설치
- 스프링 부트 설정 - JPA, DB
  - 테스트 시 @Transactional 이 설정되어있어 롤백이 되는데 데이터를 보고싶을 경우 @Commit 을 사용해 커밋처리
  - 로그를 남기는 경우 성능 상의 이유로 성능 테스트 해보고 도입하는 것 추천
---
### 섹션 3. 예제 도메인 모델
- 예제 도메인 모델과 동작확인
  - 실무에선 setter 가급적 사용 x
---
### 섹션 4. 기본 문법
- 시작 - JPQL vs Querydsl
  - JPQL은 런타임에 문법 에러 확인 가능, Querydsl은 컴파일 타임에 문법 에러 확인 가능
- 기본 Q-Type 활용
  - 같은 테이블을 조인하는 경우에만 alias 지정해서 사용
    ```java
    QMember m1 = new QMember("m1");
    ```
- 검색 조건 쿼리
  - .and() 생략가능
    ```java
    .where(
        member.username.eq("member1"),
        member.age.eq(10)
    )
    ```
- 결과 조회
- 정렬
- 페이징
- 집합
  - tuple 을 실무에서 잘 사용하지 않고 dto 방식으로 많이 씀
- 조인 - 기본 조인
- 조인 - on절
  - 내부 조인이면 where와 기능 동일이므로 where로 해결하고, 외부 조인이 필요하면 on절 사용
- 조인 - 페치 조인
  - SQL 조인을 활용해 연관된 엔티티를 한번에 조회하는 기능으로 성능 최적화에 사용
- 서브 쿼리
  - JPAExpressions로 사용
  - from절의 서브쿼리는 지원하지 않음
    - 해결 방안
      1. 서브쿼리를 join으로 변경한다.
      2. 애플리케이션에서 쿼리를 2번 분리해서 실행한다.
      3. nativeSQL을 사용한다.
- Case 문
  - 가급적이면 애플리케이션 로직에서 해결
- 상수, 문자 더하기
  - .stringValue() -> enum 타입일 때 유용함
---
### 섹션 5. 중급 문법
- 프로젝션과 결과 반환 - 기본
  - tuple은 querydsl 패키지 안에 있으므로 리포지토리 계층을 넘어서 서비스 계층까지 가져가는 것은 좋은 설계가 아님
    - 하위 기술을 핵심 로직에서 알 필요 없으므로
- 프로젝션과 결과 반환 - DTO 조회
  - Projections.beans() -> setter로 값 삽입
    - 이름이 다르면 .as() 등을 사용해서 맞춰줘야함
  - Projections.fields() -> 필드에 직접 삽입
    - 이름이 다르면 .as() 등을 사용해서 맞춰줘야함
  - Projections.constructor() -> 생성자로 값 삽입
    - 이름이 달라도 생성자로 들어가므로 안맞춰줘도 됨
  - select 절에 subQuery를 사용하는 경우 ExpressionUtils.as()로 별칭 가능
- 프로젝션과 결과 반환 - @QueryProjection
  - DTO를 Q클래스로 생성해줌 
  - Projections.constructor()와의 차이점 -> 이건 compile 오류를 못잡는다.
  - 단점
    1. QFile을 생성해줘야함.
    2. DTO가 Querydsl 의존성을 가지게 됨
       - DTO는 controller, service, repository 레이어등 다양한 곳에서 사용되므로 사용을 고려해봐야함.
- 동적 쿼리 - BooleanBuilder 사용
- 동적 쿼리 - Where 다중 파라미터 사용
  - BooleanExpression 으로 조합 가능
  - 다른 쿼리에서 재사용 가능 (isServiceable 등의 메소드)
  - null 체크만 주의해서 사용
- 수정, 삭제 벌크 연산
  - 디비에 직접 반영하므로 디비와 영속성 컨텍스트의 상태가 달라지게 됨
    - em.flush(), em.clear() 로 해결 가능
- SQL function 호출하기
  - 표준 함수들은 querydsl이 상당부분 내장하고 있다.
---
### 섹션 6. 실무 활용 - 순수 JPA와 Querydsl
- 순수 JPA 리포지토리와 Querydsl
- 동적 쿼리와 성능 최적화 조회 - Builder 사용
- 동적 쿼리와 성능 최적화 조회 - Where절 파라미터 사용
- 조회 API 컨트롤러 개발
---
### 섹션 7. 실무 활용 - 스프링 데이터 JPA와 Querydsl
- 스프링 데이터 JPA 리포지토리로 변경
- 사용자 정의 리포지토리
- 스프링 데이터 페이징 활용1 - Querydsl 페이징 연동
- 스프링 데이터 페이징 활용2 - CountQuery 최적화
- 스프링 데이터 페이징 활용3 - 컨트롤러 개발
---
### 섹션 8. 스프링 데이터 JPA가 제공하는 Querydsl 기능
- 인터페이스 지원 - QuerydslPredicateExecutor
- Querydsl Web 지원
- 리포지토리 지원 - QuerydslRepositorySupport
- Querydsl 지원 클래스 직접 만들기