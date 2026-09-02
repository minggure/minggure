# 전민규 | Backend Developer

안녕하세요. Java와 Spring Boot로 백엔드를 개발하고 있습니다.  
기능을 만드는 데서 끝내지 않고, 요청이 몰릴 때도 데이터가 어긋나지 않는지, 장애가 생긴 뒤에는 어떻게 안전하게 복구할지를 함께 고민합니다.
## 기술 스택
<img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white"> <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
## Projects

### [CLUTCH](https://github.com/seok-cess/Clutch-BE) | 경기 이벤트 기반 선착순 쿠폰 서비스

LoL 경기 중 특정 장면이 발생하면 한정 수량의 쿠폰이 열리는 서비스입니다.  
저는 쿠폰 발급 백엔드를 맡아 Redis Lua로 재고 차감과 중복 신청을 한 번에 처리하고, 실제 발급 결과는 MySQL에 안전하게 남기도록 구현했습니다. Redis 장애 시 MySQL을 기준으로 재고를 복구하는 기능과, 요청이 몰릴 때 발생하던 DB 병목을 줄이는 작업도 진행했습니다.

- **담당:** 선착순 발급, 중복 방지, 실제 쿠폰 생성과 보상 처리, Redis 장애 복구, 실시간 재고, 관리자 쿠폰 통계
- **검증:** 20,000건 K6 테스트에서 성공 10,000건·품절 10,000건·초과 발급 0건, p95 951.19ms
- **기술:** Java 21, Spring Boot, MySQL, Redis Lua, Kafka, SSE, k6
- **기여 내역:** [작성한 Pull Request 보기](https://github.com/seok-cess/Clutch-BE/pulls?q=is%3Apr+author%3Aminggure)

### [Daenggo](https://github.com/meongkk/daenggo-BE) | 반려견 동반 생활 플랫폼

반려견과 함께 갈 수 있는 장소를 찾고, 산책 기록과 커뮤니티를 이용할 수 있는 팀 프로젝트입니다.  
저는 게시글과 댓글, 이미지 등록 기능을 구현하고 작성자만 글을 수정하거나 삭제할 수 있도록 권한을 검증했습니다. 팀원들이 같은 환경에서 서비스를 실행할 수 있도록 Docker 기반 실행 환경도 구성했습니다.

- **담당:** 게시글·댓글 API, 이미지 등록, 조회수, 작성자 권한 검증, Docker 실행 환경
- **기술:** Java 21, Spring Boot, Spring Security, JPA, MySQL, Docker Compose
- **기여 내역:** [작성한 Pull Request 보기](https://github.com/meongkk/daenggo-BE/pulls?q=is%3Apr+author%3Aminggure)

## What I care about

- 동시에 요청이 들어와도 깨지지 않는 데이터
- 장애를 숨기지 않고 안전하게 멈추고 복구하는 방법
- 느낌이 아닌 테스트 결과로 설명할 수 있는 개선

## Contribution Animation

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake.svg" />
  <img alt="GitHub contribution snake animation" src="https://raw.githubusercontent.com/minggure/minggure/output/dist/github-contribution-grid-snake.svg" />
</picture>
