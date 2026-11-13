---
노트 생성 시각: "2026년 11월 13일 20시 19분"
tags:
  - BE
---

DI를 받을 수 있는 모든 것들에 대해 삽입 가능합니다

그래서 이 친구가 무엇이냐 하면
플랫폼에 종속되지 않고 응답을 보낼 수 있습니다
그리고 플랫폼마다 조금씩 다른 일부 요청에 대해서도 추상화해줘요

정확히는 플랫폼에 종속되지 않고 접근할 수 있다는 것은 이 안에 있는 필드 httpAdapter에 대한 설명이기는 합니다만
그것을 포함해서라도 좋잖아요

httpAdapter의 타입은 AbstractHttpAdapter입니다
@nestjs/platform-express나 @nestjs/platform-fastify에 쓰이는 어댑터의 기본 추상 클래스라고 나와 있는 것 같구요