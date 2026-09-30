---
노트 생성 시각: "2026년 09월 30일 18시 39분"
tags:  
  - DevOps
  - 도구
---

# 구조
.github/workflows 디렉터리를 만들어서 구성하구요

CI의 경우에는 ci.yml을 생성하면 되네요
CD의 경우에는 deploy.yml을 생성하시면 되겠구요
yml은 관습이지 yaml도 허용은 됩니다

# GitHub Actions에서의 CI 이해
GItHub Actions에서 CI를 이해하려면 이 구조를 잡으면 될 것 같구요

```plain text
Workflow
 └── Job
      ├── Step
      ├── Step
      └── Step
```

예로는 다음이 있을 수 있다네요
AI like:
```plain text
CI
└── test
    ├── Checkout
    ├── Setup Node
    ├── Install dependencies
    ├── Lint
    ├── Typecheck
    └── Test
```

여기에서의 Job은 test 한 개구요
Job에 대한 Step은 아시잖아용

Job도 여러 개가 될 수 있습니다

이런 의존 관계도 구현 가능하구요
AI like:
```plain text
lint ────────┐
typecheck ───┼──→ build
test ────────┘
```