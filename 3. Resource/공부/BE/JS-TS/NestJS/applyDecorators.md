---
노트 생성 시각: "2026년 11월 12일 14시 54분"
tags:
  - BE
---

여러 같은 종류의 데코레이터를 하나의 데코레이터로 합성합니다
다른 종류는 당연히 못 묶구요
당연하잖아요

ParameterDecorator는 그 특성상 NestJS에서 지원하지 않습니다
하고 싶다면 [[커스텀 매개변수 데코레이터|이 쪽]]으로

예시는 다음과 같습니다
```TypeScript
import { applyDecorators, Get, UseGuards } from "@nestjs/common";

export function AuthenticatedGet(path: string) {
    return applyDecorators(
        Get(path),
        UseGuards(AuthGuard)
    );
}
```