# 전민규 | Backend Engineer

> **트래픽이 몰리고 장애가 발생해도 데이터의 의미를 지키는 백엔드 개발자입니다.**<br>
> 동시성 제어, 데이터 정합성, 장애 복구를 코드와 검증 결과로 설명하는 것을 중요하게 생각합니다.

[![Portfolio](https://img.shields.io/badge/PDF_Portfolio-문제_해결_과정-0B7A75?style=for-the-badge)](portfolio/jeon-mingyu-backend-portfolio.pdf)
[![GitHub](https://img.shields.io/badge/GitHub-minggure-181717?style=for-the-badge&logo=github)](https://github.com/minggure)

<p>
  <img src="https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring%20Boot-4.1-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/MySQL-8.4-4479A1?logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Apache%20Kafka-231F20?logo=apachekafka&logoColor=white" alt="Apache Kafka" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker" />
</p>

## Featured Project | [Clutch-BE](https://github.com/seok-cess/Clutch-BE)

LoL 경기 이벤트에 맞춰 열리는 선착순 쿠폰의 **발급 요청부터 실제 쿠폰 생성, 실시간 재고, Redis 장애 복구와 대량 데이터 검증까지** 담당했습니다.

### 제가 해결한 문제

| 문제 | 설계와 구현 | 검증 결과 |
|---|---|---|
| 동시 요청의 초과·중복 발급 | Redis Lua로 재고 차감과 회차별 중복 검사를 원자화 | 동시성 통합 테스트에서 재고 상한과 사용자별 1회 발급 확인 |
| 성공 응답과 실제 쿠폰의 불일치 | `user_coupon` 생성을 최종 성공으로 정의하고 발급 요청·실제 쿠폰·결과 Outbox를 하나의 MySQL transaction으로 저장 | 성공 응답에서 실제 쿠폰 ID 반환, DB 실패 시 Redis 보상 후 재참여 가능 |
| Redis 데이터 유실 | 불확실한 상태에서는 발급을 중단하는 Fail Closed 정책과 MySQL 기준 자동 재구축 구현 | 재고 100장 장애 실험에서 장애 중 503, 복구 후 총 100장 발급, 초과·중복 0건 |
| 공통 집계 행의 DB 병목 | 요청 transaction에서 `success_count` 갱신을 분리하고 5초 주기 GROUP BY 집계·전용 인덱스·MySQL named lock 적용 | 모든 성공 요청이 한 행을 기다리던 X-lock 병목의 구조적 원인 제거 |
| 대량 데이터 정합성 | 개인정보를 출력하지 않는 읽기 전용 일관 스냅샷 검증 SQL 작성 | 사용자 1,000,003명·요청 3,517,209건·실제 쿠폰 797,209건에서 핵심 위반 0건 |

### 발급 흐름

```text
요청
→ Redis 컨텍스트 조회
→ Lua: 중복 확인 + 재고 차감
  ├─ 중복 / 품절: MySQL 접근 없이 409
  └─ 당첨: 짧은 MySQL transaction
      → 발급 요청 + user_coupon + 결과 Outbox 저장
      → commit 후 HTTP 201 + couponId, SSE 재고 알림
      → rollback 시 Redis 재고·당첨자 기록 보상
```

### 판단의 근거

- Redis 차감 성공이 아니라 **실제 쿠폰의 DB 생성**을 사용자 성공 응답의 기준으로 삼았습니다.
- Redis 상태가 불확실할 때 MySQL로 우회 발급하지 않고 **초과 발급보다 안전한 중단과 복구**를 선택했습니다.
- 조회용 성공 수량은 최대 5초의 최종 일관성을 허용하고, 발급 transaction에서 공통 행 잠금을 제거했습니다.
- 20,000 VU 시험의 TCP 연결 실패는 서버 처리량으로 과장하지 않고 배포 버전·부하 발생기·네트워크를 분리할 재검증 과제로 기록했습니다.

`Java 21` · `Spring Boot` · `JPA` · `MySQL` · `Redis Lua` · `Kafka Outbox` · `SSE` · `Micrometer` · `k6`

> 상세한 문제 분석, 설계 대안과 검증 수치는 [PDF 포트폴리오](portfolio/jeon-mingyu-backend-portfolio.pdf)에 정리했습니다.

## Project | [Daenggo-BE](https://github.com/meongkk/daenggo-BE)

반려견 동반 장소 탐색·산책 기록·커뮤니티를 제공하는 반려생활 플랫폼 백엔드입니다.

- 게시글·댓글·이미지 API와 작성자 권한 검증을 구현했습니다.
- Docker Compose와 Nginx 기반 실행 환경을 구성해 프론트엔드·백엔드·DB의 로컬 실행을 표준화했습니다.
- 장소 검색, 산책 기록, 그룹, 인증 등 팀 기능이 하나의 REST API 서비스로 동작하도록 통합했습니다.

`Java 21` · `Spring Boot` · `Spring Security` · `JPA` · `MySQL` · `Docker Compose`

## Engineering Principles

- 동시 요청에서도 깨지지 않는 **데이터 정합성**
- 장애를 숨기지 않고 안전하게 멈추고 복구하는 **운영 설계**
- 수치를 만들기보다 조건과 한계를 함께 기록하는 **정직한 성능 검증**
- 팀이 같은 방법으로 실행하고 판단할 수 있게 하는 **테스트와 문서화**

## Contribution Animation

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake.svg" />
  <img alt="GitHub contribution snake animation" src="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake.svg" />
</picture>
