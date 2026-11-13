---
노트 생성 시각: "2026년 11월 13일 23시 00분"
tags:
  - BE
---

health check를 위한 라이브러리입니다
외에도 다른 기능들이 많아요

# 등록
매우 간단합니다
기본적으로 TerminusModule.forRoot()로 호출해도 바로 사용할 수 있어요

```TypeScript
import { Module } from "@nestjs/common";
import { TerminusModule } from "@nestjs/terminus";

@Module({
	imports: [
		TerminusModule.forRoot()
	]
})
class AppModule {}
```

들어가는 옵션으로는 다음과 같습니다
```TypeScript
/**
 * The Terminus module options
 */
export interface TerminusModuleOptions {
    /**
     * The style of the error logger
     * @default 'json'
     */
    errorLogStyle?: ErrorLogStyle;
    /**
     * The logger to use. Either default logger or your own.
     */
    logger?: Type<LoggerService> | boolean;
    /**
     * The timeout to wait in ms before the application shuts down
     * @default 0
     */
    gracefulShutdownTimeoutMs?: number;
}
```

되게 알만 해요

# 사용
여기에서는 HttpHealthIndicator를 사용해보겠습니다

여러 Indicator들이 있긴 한데
대표적으로 들어보는 것이구요

HttpHealthIndicator를 사용한다면 [[@nestjs-axios|@nestjs/axios]]가 필수입니다
설치하시면 되구요

```TypeScript
import { Controller, Get } from "@nestjs/common";
import { HealthCheckService, HttpHealthIndicator, HealthCheck } from "@nestjs/terminus";

@Controller()
class AppController {
	constructor(
		private readonly __health:HealthCheckService,
		private readonly __http:HttpHealthIndicator
	) {}
	
	@Get()
	@HealthCheck()
	check() {
		return this.health.check([
			() => {
				return this.http.pingCheck("nestjs-docs", "https://docs.nestjs.com");
			}
		]);
	}
}
```

이런 느낌입니다

HealthCheck를 붙이는 이유로는 이것이 진짜 HealthCheck 라우트 핸들러임을 알리기 위해서이구요

# 커스텀
본인만의 그것을 만들고 싶다면 HealthIndicator 추상 클래스를 상속 받아 구현하시면 됩니다