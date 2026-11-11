---
노트 생성 시각: "2026년 11월 10일 22시 32분"
tags:
  - BE
---

NestJS에서 JWT를 구현하는 방법 중 하나구요
내부적으로는 [[jsonwebtoken|jsonwebtoken]]을 사용합니다

사용하는 수준이 아니라 래퍼 패키지라 불러도 될 정도라고 하네요

# Module에 추가
JwtModule도 기본적으로 DynamicModule을 반환하는 for~~ 시리즈가 있어요

여기에 넣은 옵션들은 jsonwebtoken에서 사용하던 것처럼 일일이 secret과 옵션 등을 넣지 않아도 알아서 해줍니다
\_\_jwtService.signAsync({ sub: id })만 해도 자동으로 적용된다는 소리인 것이구요

# 비동기
callback을 넣어야 옛 CommonJS 느낌으로 비동기를 처리할 수 있었던 jsonwebtoken과는 다르게 ESM의 await/async 기반 비동기를 지원합니다

이게 얼마나 좋은데요
직관적이게 되어 버린다구요

# 제네릭
verify\<T\>와 같이 이런 것들을 지원합니다
좋아요