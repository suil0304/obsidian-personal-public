---
노트 생성 시각: "2026년 11월 08일 14시 21분"
tags:
  - BE
  - 용어
---

*Inversion of Control*

어쨌든 SOLID 원칙은 중요합니다
근데 Spring이나 NestJS와 같은 DI를 해주는 녀석들은 이것을 어떻게 지켜주는 거죠

SOLID에서 D는 DIP(의존성 역전 원칙)입니다
IoC는 이것을 위해...

예를 들기 위한 NestJS 코드입니다

```TypeScript
import { Injectable, Module, Controller, Get } from "@nestjs/core";

@Injectable()
class AppService {
	getHello() {
		return "Hello, world!";
	}
}

@Controller()
class AppController {
	constructor(private readonly __appService:AppService) {}
	
	@Get()
	getHello() {
		return this.__appService.getHello();
	}
}

@Module({
	controllers: [AppController],
	providers: [AppService]
})
class AppModule {}
```

AppController가 AppService에 의존하고 있기는 합니다만
그렇다고 아예 직접 new로 생성하고 있는 것도 아니구요

이게 IoC에요
논리적으로는 AppController가 AppService를 원하고 있지만
실제로는 다른 곳에서 연결되기 때문에 제어 반전인 것이죠
*생명주기라 부릅시다
AppController가 직접 생성하지 않는다는 말이 생명주기에 관여하지 않는다고 말할 수 있는 것이기도 하구요*

# IoC 컨테이너
IoC를 수행해주는 컨테이너입니다
말 그대로에요

대충 내부 어딘가에서 AppService를 new로 생성한 다음 AppController로 꽂아줌으로서 제어의 역전을 일으키는 컨테이너라 읽을 수 있겠구요

# 그래서 DIP는 어떻게 하는 것일까요
다른 클래스 생성하기 귀찮아서 BaseService로 추상화된 서비스를 이용한 DIP를 적어둔 것이지
대부분의 Service와 Controller는 그렇게까지 추상화되는 것이 필요하지는 않기 때문에
*(정확히는 같은 이름을 가지는 Service와 Controller겠구요)*
다른 클래스 또는 다른 모듈에서 오는 provider에 대하여 DIP를 시도하는 것이 차라리 더 효율적일 수 있습니다

```TypeScript
import { Inject, Injectable, Module, Controller, Get } from "@nestjs/core";

interface BaseService {
	public getHello():string;
}

@Injectable()
class AppService implements BaseService {
	getHello() {
		return "Hello, world!";
	}
}

@Controller()
class AppController {
	constructor(
		@Inject("BaseService")
		private readonly __baseService:BaseService
	) {}
	
	@Get()
	getHello() {
		return this.__baseService.getHello();
	}
}

@Module({
	controllers: [AppController],
	providers: [
		{
			provide: "BaseService",
			useClass: AppService
		}
	]
})
class AppModule {}
```