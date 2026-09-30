---
노트 생성 시각: "2026년 09월 30일 17시 36분"
tags:  
  - DevOps
  - 용어
---

# CI
*Continuous Integration*
*지속적 통합*

여러 개발자가 각자 작업한 코드를 하나의 코드베이스에 계속 통합하는 과정에서 문제가 생기지 않도록 자동으로 검사하는 것이라고 하네요

AI 피셜 자동으로 통합하는 과정에서 다음과 같은 과정을 자동으로 수행하도록 할 수 있다고 하구요
```plain text
checkout
 ↓
Node 설치
 ↓
pnpm install
 ↓
lint
 ↓
typecheck
 ↓
test
 ↓
build
```

처음 보면 자동 테스트로 생각하기 쉬운데
얘는 코드를 가져와서 환경 설정, 의존성 설치, 정적 검사, 빌드, 테스트, 결과 보고까지 다 해줬잖아구요

GitHub Actions는 이럴 때 등장하는 대표적인 것 중 하나구요
GItHub에 보통 코드 베이스를 구축하지 다른 데에 올리는 경우는 잘 없잖아요?

[[GitHub Actions#GitHub Actions에서의 CI 이해]]에서 자세한 것을 살펴보면 되겠네요

# CD
*Continuous Delivery / Continuous Deployment*
*지속적 제공 / 지속적 배포*

코드를 실제 환경에 반영하는 것이구요

이렇게 될 수 있다고 하네요
```plain text
CD ↓ Docker image 생성 ↓ Registry push ↓ 서버 배포
```

그런데 CD에는 2가지 의미가 있다 위에도 명시했어요

## Continuous Delivery
제공만 하기 때문에 배포는 사람이 직접 승인해야 하구요

## Continuous Deployment
배포까지 자동으로 해주구요

# Artifact
dist/와 같은 빌드 결과물을 이것이라 생각할 수 있구요

CI가 테스트하면서 빌드하면?
CD는 이 빌드 결과물을 바탕으로 배포하는 거죠 뭐

# 좋은 CI/CD란?

# CI/CD에서 자주 사용되는 Docker
Docker가 자주 사용되기도 합니다

이런 구조가 흔하다고도 하구요
```plain text
Docker build
↓ Docker Image
↓ Container Registry
↓ Production Server
```

이런 이미지를 만들었다고 하면
```plain text
ghcr.io/suil0304/eaglebot:latest
```

CI/CD가 자동으로 이런 것들을 수행하는 것이구요
```plain text
git push
 ↓
test
 ↓
docker build
 ↓
docker push
 ↓
server pull
 ↓
container restart
```

Docker를 사용하는 경우 CD에서 Docker Image를 Artifact 대신 전달한다고도 하네요