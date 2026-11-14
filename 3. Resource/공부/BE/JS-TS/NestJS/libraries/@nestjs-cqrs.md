---
노트 생성 시각: "2026년 11월 14일 16시 40분"
tags:
  - BE
---

[[CQRS|CQRS]]를 NestJS에서 쉽게 구현하도록 만들어진 공식 라이브러리구요

# 등록
```TypeScript
import { Module } from "@nestjs/common";
import { CqrsModule } from "@nestjs/cqrs";

@Module({
	imports: [
		CqrsModule.forRoot()
	]
})
class AppModule {}
```

대충 하시면 됩니다

저기에도 옵션이 많아서 직접 찾아보시는 것을 추천드리구요

# Command
## ICommand
ICommand는 빈 interface입니다
TS가 이해하고 컴파일 타임에 검증하도록 하는 것 같은데
흐음

아무튼 이것을 구현하게 만드시면 됩니다

## CommandBus
CQRS의 Command와 관련된 버스입니다

여기에 태워서 실행시키면 @nestjs/cqrs가 알아 처리해줍니다

```TypeScript
import { CommandBus } from "@nestjs/cqrs";
import { Injectable } from "@nestjs/common";
import { TestCommand } from "./commands/test.command.ts";

@Injectable()
class AppService {
	constructor(
		private readonly __commandBus:CommandBus
	) {}
	
	test() {
		const command = new TestCommand();
		
		return this.__commandBus.execute(command);
	}
}
```

## CommandHandler
*class decorator*

사실 알아 처리하는 것은 아니구요
이것을 붙인 클래스에 추가로 ICommandHandler를 구현시키도록 구성해야 합니다

```TypeScript
import { Injectable } from "@nestjs/common";
import { CommandHandler, ICommandHandler } from "@nestjs/cqrs";
import { TestCommand } from "../commands/test.command.ts";

@Injectable()
@CommandHandler(TestCommand)
class TestCommandHandler implements ICommandHandler<TestCommand> {
	async execute(command:TestCommand) {
		// command 로직 구현
	}
}
```

한 번에 한 CommandHandler가 잡을 수 있구요
당연하잖아요

# Query
## IQuery
역시나 비어 있습니다

## QueryBus
얘도 execute 사용합니다

## QueryHandler
*class decorator*

마찬가지로 IQueryHandler를 받아서 구현해야 합니다

```TypeScript
import { Injectable } from "@nestjs/common";
import { QueryHandler, IQueryHandler } from "@nestjs/cqrs";
import { TestQuery } from "../queries/test.query.ts";

@Injectable()
@QueryHandler(TestQuery)
class TestQueryHandler implements IQueryHandler<TestQuery> {
	async execute(query:TestQuery) {
		// 쿼리 처리 로직
	}
}
```

# Event
## IEvent
이벤트도 구성할 수 있습니다

IEvent도 마찬가지로 빈 interface입니다

## EventBus
대충 있다고 치고 Command에서 이벤트를 등록해야 할 것 같으면

```TypeScript
// constructor(
//  	private readonly __eventBus:EventBus
// ) {}

async execute(command:TestCommand) {
	this.__eventBus.publish(new Event1());
	this.__eventBus.publish(new Event2());
}
```

이렇게 등록할 수 있습니다

## EventsHandler
*class decorator*

이것은 Command나 Query와는 다르게 여러 Handler가 잡을 수 있구요

데코레이터에 s가 들어가는 것처럼 이 친구는 여러 이벤트를 넣을 수 있습니다
*REST parameter*

이 또한 구현하고 싶다면 IEventHandler를 구현하도록 구성해야 합니다

```TypeScript
import { Injectable } from "@nestjs/common";
import { EventsHandler, IEventHandler } from "@nestjs/cqrs";
import { TestEvent } from "../events/test.event.ts";

@Injectable()
@EventsHandler(TestEvent)
class TestEventHandler implements IEventHandler<TestEvent> {
	async handle(event:TestEvent) {
		// 이벤트 처리 로직
	}
}
```

뭐 그렇습니다
