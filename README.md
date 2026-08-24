# 전민규 · Backend Engineer

> **정합성과 장애 상황까지 설계하는 백엔드 개발자**  
> 동시성 제어, 데이터 일관성, 실시간 이벤트 흐름을 중심으로 서비스를 구현합니다.

<p>
  <img src="https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring%20Boot-4.1-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/MySQL-8.4-4479A1?logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Apache%20Kafka-231F20?logo=apachekafka&logoColor=white" alt="Apache Kafka" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker" />
</p>

## Featured Projects

### [Clutch-BE](https://github.com/seok-cess/Clutch-BE)

스포츠 플랫폼의 **고동시성 선착순 쿠폰 발급** 백엔드입니다.

- Redis Lua로 재고 차감과 중복 당첨을 원자적으로 제어하고, MySQL 트랜잭션으로 실제 쿠폰 발급을 확정했습니다.
- DB 저장 실패 시 Redis 재고와 당첨 기록을 보상해 사용자 재참여가 가능하도록 설계했습니다.
- Redis 장애·키 유실 시 MySQL의 실제 쿠폰 데이터를 검증한 뒤 재고와 당첨자 정보를 재구축하는 Fail Closed 복구 흐름을 구현했습니다.
- SSE 기반 실시간 잔여 재고 알림과 Kafka Outbox 기반 발급 결과 전달을 연결했습니다.

`Java 21` · `Spring Boot` · `MySQL` · `Redis` · `Kafka` · `Docker Compose`

### [Daenggo-BE](https://github.com/meongkk/daenggo-BE)

반려견 동반 장소 탐색·산책 기록·커뮤니티를 제공하는 반려생활 플랫폼 백엔드입니다.

- 게시글·댓글·이미지 API와 작성자 권한 검증을 구현했습니다.
- Docker Compose와 Nginx 기반 실행 환경을 구성해 프론트엔드·백엔드·DB의 로컬 실행을 표준화했습니다.
- 장소 검색, 산책 기록, 그룹, 인증 등 팀 기능이 하나의 REST API 서비스로 동작하도록 통합했습니다.

`Java 21` · `Spring Boot` · `Spring Security` · `JPA` · `MySQL` · `Docker Compose`

## What I care about

- 동시 요청에서도 깨지지 않는 **데이터 정합성**
- 장애를 숨기지 않고 안전하게 멈추고 복구하는 **운영 설계**
- 팀이 빠르게 실행하고 검증할 수 있는 **명확한 개발 환경과 문서**

## Contribution Animation

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/github-contribution-grid-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/github-contribution-grid-snake.svg" />
  <img alt="GitHub contribution snake animation" src="https://raw.githubusercontent.com/minggure/minggure/output/github-contribution-grid-snake.svg" />
</picture>
