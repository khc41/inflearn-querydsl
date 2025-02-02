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
- 결과 조회
- 정렬
- 페이징
- 집합
- 조인 - 기본 조인
- 조인 - on절
- 조인 - 페치 조인
- 서브 쿼리
- Case 문
- 상수, 문자 더하기
---
### 섹션 5. 중급 문법
- 프로젝션과 결과 반환 - 기본
- 프로젝션과 결과 반환 - DTO 조회
- 프로젝션과 결과 반환 - @QueryProjection
- 동적 쿼리 - BooleanBuilder 사용
- 동적 쿼리 - Where 다중 파라미터 사용
- 수정, 삭제 벌크 연산
- SQL function 호출하기
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