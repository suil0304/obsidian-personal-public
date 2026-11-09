---
노트 생성 시각: "2026년 11월 09일 20시 04분"
tags:
  - BE
---

NestJS는 공식적으로 지원하는 다른 ORM의 Module에 대하여 이 방식으로 서술하는 것을 지원한다고 하네요

[[@nestjs-typeorm|NestJS의 공식 TypeORM 모듈 패키지]]에서는 원래 이렇게 작성했잖아요?
```TypeScript
import { Module } from "@nestjs/core";
import { TypeOrmModule } from "@nestjs/typeorm";

@Module({
	imports: [
		TypeOrmModule.forRoot({
			url: process.env["DATABASE_URL"]!, // connection string
			type: "mysql",
			entities: [
                import.meta.dirname + "**/*.entity.{ts,js}"
            ],
            synchronize: process.env["NODE_ENV"] === "development"
		})
	]
})
class AppModule {}
```

이렇게 작성할 수 있다는 것이구요
```JSON
{
	"url": "mysql://...",
	"type": "mysql",
	"entities": [
		"dist/**/*.entity.{ts,js}"
	],
	"synchronize": true
}
```

당연하지만 JSON은 환경변수를 못 읽기 때문에 조금 많이 문제가 생길 수 있겠구요
그렇다고 JS로 다시 감싸기에는 많이 귀찮잖아요
이러언

따라서 차라리 forRootAsync를 지원하는 경우 [[@nestjs-config|ConfigService]]와 섞어 DI하며 초기화하도록 유도하는 것이 좋다네요
흐음