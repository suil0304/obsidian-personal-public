---
노트 생성 시각: "2026년 11월 12일 16시 04분"
tags:
  - BE
---

[[winston|winston]]의 NestJS 래퍼 패키지이구요
유저들이 만들었습니다
좋네요

# 등록
```TypeScript
import { Module } from '@nestjs/common';
import { format, transports } from 'winston';
import { utilities, WinstonModule } from "nest-winston";

@Module({
    imports: [
        WinstonModule.forRoot({
            transports: [
                new transports.Console({
                    level: process.env["NODE_ENV"] === "production" ? "info" : "silly",
                    format: format.combine(
                        format.timestamp(),
                        utilities.format.nestLike("MyApp", {
                            prettyPrint: true
                        })
                    )
                })
            ]
        })
    ]
})
class AppModule {}
```

대충 이런 식으로 할 수 있습니다

# 사용
nest-winston에서 WINSTON_MODULE_PROVIDER를 가져올 수 있습니다
그것을 [[DI를 위한 데코레이터#Inject|Inject]]에 넣으면 Logger가 DI될 것이구요

이건 추가적이긴 하다만
Logger는 winston에서 가져옵니다

```TypeScript
import { Injectable, Inject } from "@nestjs/common";
import { Logger } from "winston";
import { WINSTON_MODULE_PROVIDER } from "nest-winston";

@Injectable()
class TestService {
	constructor(
		@Inject(WINSTON_MODULE_PROVIDER)
		private readonly __logger:Logger
	) {}
	
	async getTest() {
		this.__logger.debug("test");
		return "test";
	}
}
```

## 전역으로 Winston 로거 사용
[[로깅#전역으로 커스텀 로거 사용|이거]] 느낌으로 가능한데
logger에 WinstonModule.createLogger로 생성해 먹여주시면 됩니다
