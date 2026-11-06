---
노트 생성 시각: "2026년 11월 01일 21시 40분"
tags:
  - BE
  - 도구
---

# 어디서든
## 보안
### uuid
UUID 생성하는 라이브러리구요
여러 버전을 지원합니다

UUID는 Universally Unique Identifier의 약자라고 하네요

버전마다 생성 방식이 달라지는데
요즘에는 v4와 v7을 많이 고려한다고 하네요

v1과 v4, v7만 간단하게 적어보다

v1은 시간에 MAC을 기반으로 한 노드 정보로 생성합니다
v4는 난수구요
v7은 UNIX + 난수입니다

## 검증
### class-validator
DTO 검증 용도로 써먹기 아주 좋습니다

## ORM
### kysely
사실 이 친구는 ORM이 아니라 Query Builder입니다
근데 맛있어요
조금 더 로우 레벨이라 다루고 싶은 만큼 다룰 수 있습니다

### prisma
v7이었나 기준으로 많은 것이 바뀌었는데
Prisma v7을 추천합니다
이전 버전을 굳이 사용할 필요는 없다고 생각하구요

## 변환
### zod
요즘에 많이 뜨는 것 같기도 한데

### joi
근본이라고 하네요
오래되었고 풍부하다

### class-transformer
struct처럼 사용하는 클래스의 값을 변환해주는 것입니다

## 기타
### nodemailer
무료로 이메일 발송해주는 녀석입니다
테스트용으로 쓰기 좋겠네요
이러언

# NestJS
## [[@nestjs-config|@nestjs/config]]
ConfigModule 등을 추가합니다

## @nestjs/mapped-types
가장 대표적으로 쓰이는 것이 생성 DTO를 수정 DTO로 재사용하는데에 쓰이는 PartialType 함수구요
원래 Utility Type으로만 쓰였던 Omit이나 그런 것들을 클래스 변환 등으로 런타임에 직접 영향을 미치도록 만든 라이브러리라 생각하시면 좋을 것 같네요

# Express 계열