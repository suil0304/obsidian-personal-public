---
노트 생성 시각: "2026년 11월 11일 21시 45분"
tags:
  - BE
---

말 그대로 JWT를 서명하고 검증하며, 해석하는 패키지입니다

# sign
말 그대로입니다

```TypeScript
export function sign(
    payload: string | Buffer | object,
    secretOrPrivateKey: Secret | PrivateKey,
    options?: SignOptions,
): string;
```

이것 말고도 따로 callback을 받는 버전도 있는데
그것은 sign 함수 반환값이 void가 되기 때문에 잘 사용하셔야 할 것 같구요

직접 반환되지 않고 callback으로 받아 온다는 것이 직관적이지는 않잖아요

# verify
말 그대로입니다

```TypeScript
export function verify(
    token: string,
    secretOrPublicKey: Secret | PublicKey,
    options: VerifyOptions & { complete: true },
): Jwt;
export function verify(
    token: string,
    secretOrPublicKey: Secret | PublicKey,
    options?: VerifyOptions & { complete?: false },
): JwtPayload | string;
export function verify(
    token: string,
    secretOrPublicKey: Secret | PublicKey,
    options?: VerifyOptions,
): Jwt | JwtPayload | string;
```

# decode
verify하지 않고 바로 풀어버립니다
내부 값에 바로 접근해야 한다면 사용하세요
그게 아니라면 아예 안 보셔도 괜찮습니다