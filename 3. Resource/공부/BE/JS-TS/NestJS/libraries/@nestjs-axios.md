---
노트 생성 시각: "2026년 11월 13일 23시 22분"
tags:
  - BE
---

백엔드라고 그 거지 같은 fetch를 그대로 사용할 수는 없잖아요
그래서 사용합니다
NestJS스럽게 DI해서

# 등록
얘네는 forRoot와 같은 이름이 아닌 다른 이름을 채용했습니다

```TypeScript
import { Module } from "@nestjs/common";
import { HttpModule } from "@nestjs/axios";

@Module({
	imports: [
		HttpModule.register()
	]
})
class AppModule {}
```

옵션에 뭐가 많아서 따로 찾아 보시는 것을 추천 드리구요

# 사용
```TypeScript
import { Injectable } from "@nestjs/common";
import { HttpService } from "@nestjs/axios";

@Injectable()
class AppService {
	constructor(
		private readonly __axios:HttpService
	) {}
}
```

끝

# 참고
get 등등 가져올 때 그 반환값이 rxjs의 Observable이라서 관련 그것을 사용할 수 있다고 하네요
이러언