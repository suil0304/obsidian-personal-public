---
노트 생성 시각: "2026년 11월 01일 21시 40분"
tags:
  - BE
  - 도구
---

# 어디서든
## 인증
### [[jsonwebtoken|jsonwebtoken]]
이름만 봐도 알만 하죠

### [[passport|passport]]
그 전설의 인증 패키지

## 스키마 검증
### [[zod|zod]]
요즘에 많이 뜨는 것 같기도 한데

### joi
근본이라고 하네요
오래되었고 풍부하다

### class-validator
DTO 검증 용도로 써먹기 아주 좋습니다

## ORM
### [TypeORM|TypeORM]
유명한 친구죠

### [[타입|kysely]]
사실 이 친구는 ORM이 아니라 Query Builder입니다
근데 맛있어요
조금 더 로우 레벨이라 다루고 싶은 만큼 다룰 수 있습니다

### prisma
v7이었나 기준으로 많은 것이 바뀌었는데
Prisma v7을 추천합니다
이전 버전을 굳이 사용할 필요는 없다고 생각하구요

## 변환
### class-transformer
struct처럼 사용하는 클래스의 값을 변환해주는 것입니다

## 로깅
### [[winston|winston]]
유명한 로깅 패키지라 하네요

단순히 출력하는 것을 넘어 기록하고 관리할 수 있도록 지원하는 라이브러리입니다

## 기타
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

### ulid
긴 문자열을 id로 사용하고 싶은 경우 추천합니다

### nodemailer
무료로 이메일 발송해주는 녀석입니다
테스트용으로 쓰기 좋겠네요
이러언

사용하실 때 pass에 발급 받은 앱 패스워드를 넣어주세요
user에는 본인 이메일 넣으시면 됩니다
이러언

### [[reflect-metadata|reflect-metadata]]
가뜩이나 동적인 JS 세계에서 더욱 동적이고 혁신적인 것을 추구하기 위해 있는 라이브러리라 이해하시면 될 것 같아요
[[데코레이터#구버전 (TS Decorator)|구버전]] 사용하고 있는 라이브러리들은 거의 전부 이 라이브러리를 사용하고 있습니다

### [[node-cron|node-cron]]
특정 시간마다 처리되어야 하는 등의 작업 스케줄링을 등록하는 라이브러리입니다

# NestJS
## [[@nestjs-config|@nestjs/config]]
ConfigModule 등을 추가합니다

## [[@nestjs-jwt|@nestjs/jwt]]
JwtService를 DI하도록 지원하는 NestJS의 라이브러리입니다
좋구요

## [[@nestjs-authentication|@nestjs/authentication]]
[[@nestjs-jwt|@nestjs/jwt]] 가지고는 성이 안 찬다 싶으면 사용해보세요
프레임워크라 부를 수 있는 그러한 인증 라이브러리입니다

## [[@nestjs-typeorm|@nestjs/typeorm]]
[[TypeORM|TypeORM]]을 NestJS에서 공식적으로 지원해주는 라이브러리입니다
좋구요

## [[@nestjs-passport|@nestjs/passport]]
[[passport|passport]]의 NestJS 공식 라이브러리입니다

## [[nest-winston|nest-winston]]
winston의 NestJS 래퍼 패키지입니다
유저들이 만들었구요

## @nestjs/mapped-types
가장 대표적으로 쓰이는 것이 생성 DTO를 수정 DTO로 재사용하는데에 쓰이는 PartialType 함수구요
원래 Utility Type으로만 쓰였던 Omit이나 그런 것들을 클래스 변환 등으로 런타임에 직접 영향을 미치도록 만든 라이브러리라 생각하시면 좋을 것 같네요

## [[@nestjs-schedule|@nestjs/schedule]]
그리고 그 [[node-cron|node-cron]]의 NestJS 공식 라이브러리입니다

## [[@nestjs-terminus|@nestjs/terminus]]
health check를 위한 라이브러리입니다
외에도 정상적인 종료 등을 지원하게 만드는 역할도 포함한다 하네요

## [[@nestjs-axios|@nestjs/axios]]
HTTP 요청 보내기 클라이언트 라이브러리인 axios의 NestJS 공식 라이브러리구요

# Express 계열