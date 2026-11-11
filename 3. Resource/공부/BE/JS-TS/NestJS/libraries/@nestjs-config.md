---
노트 생성 시각: "2026년 11월 03일 19시 46분"
tags:
  - BE
---

# ConfigModule
대충 src 내부에 \*.config.ts를 만들고

```TypeScript
import { registerAs } from "@nestjs/config";

export default registerAs("test", () => {
	return {
		"test": process.env["TEST"]!
	};
});
```

이것을 AppModule에 이렇게 추가합시다

```TypeScript
@Module({
	imports: [
		ConfigModule.forRoot({
			isGlobal: true,
			load: [testConfig]
		})
	]
})
export class AppModule {}
```

이러면 ConfigService를 DI해주구요

보통 configService.getOrThrow를 많이 사용하긴 합니다
설정에서 undefined 등을 고려할 일이 웬만하면 없어서

기능에 따라 config를 추가하고 싶다면 ConfigModule.forFeature를 사용하는 것도 좋을 것 같구요

# ConditionalModule
동적으로 모듈을 추가하는 것이 가능합니다

```TypeScript
@Module({
	imports: [
		ConditionalModule.registerWhen(TestModule, "ENV_VARIABLE")
	]
})
// ...
```

ENV_VARIABLE이 false가 아니라면 추가하는 것이구요

```TypeScript
(env:NodeJS.ProcessEnv) => {
	return false;
}
```

등등의 함수를 넣을 수도 있습니다

# config.KEY로 DI
```TypeScript
imports: [
	ConfigModule.forFeature(emailConfig)
],
```
이게 사실은 [[커스텀 프로바이더#FactoryProvider|FactoryProvider]]로 변환해주는 느낌도 겸하는데

그래서 constructor에다 이렇게 해도 됩니다

```TypeScript
constructor(@Inject(emailConfig.KEY) private readonly __config:ConfigType<typeof emailConfig>) {
    this.__transporter = createTransport({
        service: this.__config.service,
        auth: {
            user: this.__config.auth.name,
			pass: this.__config.auth.password
		}
	});
}
```