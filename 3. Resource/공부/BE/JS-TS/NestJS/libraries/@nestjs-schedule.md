---
노트 생성 시각: "2026년 11월 13일 22시 34분"
tags:
  - BE
---

[[node-cron|node-cron]] 등을 통합한 NestJS 공식 작업 스케줄링 라이브러리입니다

# 등록
기본적으로 ScheduleModule.forRoot()만 호출해도 바로 초기화되기는 합니다
근데 얘도 옵션이 있기는 함

```TypeScript
import { Module } from "@nestjs/common";
import { ScheduleModule } from "@nestjs/schedule";

@Module({
	imports: [
		ScheduleModule.forRoot({
			cronJobs: true,
		    intervals: true,
		    timeouts: true
		})
	]
})
```

전부 사용할 것인지 묻고 있는 것입니다
명시적으로 꺼줄 수 있어요

cronJobs는 @Cron으로 등록하는 것들이구요
intervals는 @Interval로 등록하는 것들이구요
timeouts는 @Timeout으로 등록하는 것들이구요

# Cron
옵션이 많아서 직접 알아보셔야 할 것 같구요

서비스에다 두고 이렇게 사용하시면 됩니다
```TypeScript
import { Injectable } from "@nestjs/common";
import { Cron } from "@nestjs/schedule";

@Injectable()
class AppService {
	@Cron("* * * * * *", { name: "test" })
	test() {
		console.log("test");
	}
}
```

매 초마다 반복하겠다는 소리입니다

[[node-cron#cron expression|cron expression]] 없이 사용하고 싶다 하시면
이렇게 사용할 수도 있습니다

```TypeScript
import { Injectable } from "@nestjs/common";
import { Cron } from "@nestjs/schedule";

@Injectable()
class AppService {
	@Cron(new Date(Date.now() + 3000), { name: "test" })
	test() {
		console.log("test");
	}
}
```

이러면 앱이 실행되고 난 후 3초 뒤에 실행됩니다

# Interval
대충 JS의 setInterval을 생각하시면 되겠는데요

```TypeScript
import { Injectable } from "@nestjs/common";
import { Interval } from "@nestjs/schedule";

@Injectable()
class AppService {
	@Interval("test", 1000)
	test() {
		console.log("test");
	}
}
```

# Timeout
JS setTimeout

```TypeScript
import { Injectable } from "@nestjs/common";
import { Timeout } from "@nestjs/schedule";

@Injectable()
class AppService {
	@Timeout("test", 1000)
	test() {
		console.log("test");
	}
}
```

# 동적으로
얘네들 전부 데코레이터 붙인 후 정적으로 해주세요 하는 것들이잖아요?
동적으로는 어떻게 할까요

import { CronJob }
```TypeScript
import { Injectable } from "@nestjs/common";
import { CronJob } from "@nestjs/schedule";

@Injectable()
class AppService {
	constructor(
		private readonly __schedulerRegistry:SchedulerRegistry
	) {}
	
	addCronJob() {
		const name = "test";
		
		const job = new CronJob("* * * * * *", () => {
			console.log("test");
		});
		
		this.__schedulerRegistry.addCronJob(name, job);
	}
}
```

이러면 등록까지 된 것 같잖아요?
근데 추가만 완료된 것이었구요
이러언

getCronJob으로 가져와서 job.start, job.end를 호출해야 합니다