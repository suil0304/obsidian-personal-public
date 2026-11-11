---
노트 생성 시각: "2026년 11월 09일 19시 59분"
tags:
  - BE
  - ORM
---

기본적인 내용은 [[TypeORM|TypeORM]]을 참고하는 것이 좋을 것 같구요
여기에 들어 있을 것은 좀 있어서

어쩔 수 없다고 해야 할까나
Data Mapper 방식으로 사용하는 것이 DI하기도 쉽고 의존성 나누기도 쉬워서 여기서도 웬만하면 Data Mapper로 사용한다고 하네요

# 추가
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

이 정도면 꽤 적당합니다

forFeature에서 Entity 몇 개 넣어주면 되구요

뭐
시그니처 좀 뜯어 보다 보면 뒤에 name이 더 들어갈 수도 있다는 것을 눈치챌 수 있습니다

해당 DataSource의 식별자입니다
여러 데이터베이스에서 커넥션이 올 수도 있잖아요
이 이름을 구별하기 위한 거죠

[[@nestjs-typeorm#TypeOrmModuleOptions|TypeOrmModuleOptions]]를 보면 name이 있는데
이것보다 2번째 인자의 우선순위가 더 높습니다
그렇다고 하네요

```TypeScript
@Module({
    imports: [
        TypeOrmModule.forRoot({
            type: 'mysql',
            host: 'localhost',
            database: 'users'
        }, 'usersConnection'),

        TypeOrmModule.forRoot({
            type: 'postgres',
            host: 'localhost',
            database: 'analytics'
        }, 'analyticsConnection')
    ]
})
class AppModule {}
```

name 인자는 이런 느낌으로

# 사용
```TypeScript
import { Injectable } from "@nestjs/common";
import { InjectRepository } from "@nestjs/typeorm";
import { User } from "./user.entity";
import { Repository } from "typeorm";

@Injectable()
class AppService {
    constructor(
        @InjectRepository(User)
        private readonly __userRepository:Repository<User>
    ) {}
}
```

사실 InjectRepository는 안 적어도 되는데
명시적으로 적으면 좋잖아요

# TypeOrmModuleOptions
한 번쯤 확인하고 가보세요
좋잖아요
이런 것

```TypeScript
/**
 * @publicApi
 */
export type TypeOrmModuleOptions = {
    /**
     * NestJS-level datasource identifier.
     * In TypeORM 0.3.x this also existed on DataSourceOptions; in 1.0 it was removed.
     */
     
    name?: string;
    /**
     * Maximum number of connection attempts, including the first one
     * Default: 10
     */
    retryAttempts?: number;
    
    /**
     * Delay between connection retry attempts (ms)
     * Default: 3000
     */
    retryDelay?: number;
    
    /**
     * Function that determines whether the module should
     * attempt to connect upon failure.
     *
     * @param err error that was thrown
     * @returns whether to retry connection or not
     */
    toRetry?: (err: any) => boolean;
    
    /**
     * If `true`, entities will be loaded automatically.
     */
    autoLoadEntities?: boolean;
    
    /**
     * If `true`, will show verbose error messages on each connection retry.
     */
    verboseRetryLog?: boolean;
    
    /**
     * If `true` database initialization will not be performed during module initialization.
     * This means that database connection will not be established and migrations will not run.
     * Database initialization will have to be performed manually using `DataSource.initialize`
     * and it will have to implement own retry mechanism (if necessary).
     */
    manualInitialization?: boolean;
} & Partial<DataSourceOptions>;
```

verbose는 로깅에서 자세하게 정보를 제공하겠다는 소리로 알아 들으시면 됩니다

이렇게만 적어놔도 이해할만 하잖아요