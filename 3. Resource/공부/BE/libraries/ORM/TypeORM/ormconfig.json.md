---
노트 생성 시각: "2026년 11월 09일 20시 04분"
tags:
  - BE
---

TypeORM은 0.3 이전까지 json에서 작성하도록 하는 방법도 지원했었다고 하네요
0.3으로 올라오면서 제거했다고는 하는데
구버전을 사용하는 경우도 가끔씩 있잖아요

예시는 전부 NestJS로 들겠습니다
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

NestJS에서는 차라리 forRootAsync로 [[@nestjs-config|ConfigService]]와 섞어 DI하며 초기화하도록 유도하는 것이 좋다네요
흐음

동적으로 ormconfig.json을 다루는 방법도 있다고는 하는데
그렇게 추천하지는 않을게요