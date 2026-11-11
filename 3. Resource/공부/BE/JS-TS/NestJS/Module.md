---
노트 생성 시각: "2026년 11월 10일 16시 57분"
tags:
  - BE
---

데코레이터에 대한 내용은 [[클래스 데코레이터#Module|여기]]를 참고합시다

# NestModule
*interface*

원래였으면

```TypeScript
import { Module } from "@nestjs/common";

@Module({ /* ... */ })
class AppModule {}
```

이렇게 작성하잖아요?
그런데 이 모듈이 다른 곳으로 사용되면서 설정될 때 configure를 찾고 없다면 넘긴단 말이죠?

이와 관련된 interface를 구현하도록 하면 더 좋지 않을까 싶구요

```TypeScript
import { Module, NestModule, MiddlewareConsumer } from "@nestjs/common";

@Module({ /* ... */ })
class AppModule implements NestModule {
	configure(consumer:MiddlewareConsumer) {
		console.log("test");
	}
}
```

이러면 `test`를 출력 받을 수 있겠습니다

NestModule은 아주 간단합니다
```TypeScript
/**
 * @publicApi
 */
export interface NestModule {
    configure(consumer: MiddlewareConsumer): any;
}
```
로 구성되어 있습니다

# MiddlewareConsumer
```TypeScript
/**
 * Interface defining method for applying user defined middleware to routes.
 *
 * @see [MiddlewareConsumer](https://docs.nestjs.com/middleware#middleware-consumer)
 *
 * @publicApi
 */
export interface MiddlewareConsumer {
    /**
     * @param {...(Type | Function)} middleware middleware class/function or array of classes/functions
     * to be attached to the passed routes.
     *
     * @returns {MiddlewareConfigProxy}
     */
    apply(...middleware: (Type<any> | Function)[]): MiddlewareConfigProxy;
}
```

[[3. Resource/공부/BE/JS-TS/NestJS/미들웨어|여기]]에서 미들웨어를 만들었다면
그것을 그대로 넘겨주시면 되겠습니다

직관적이게도 미들웨어는 넣은 순서대로 동작합니다

# MiddlewareConfigProxy
```TypeScript
/**
 * @publicApi
 */
export interface MiddlewareConfigProxy {
    /**
     * Routes to exclude from the current middleware.
     *
     * A route given with a `version` is only excluded for the requests for that
     * version: with URI versioning, through the version segment of its path,
     * and with header, media type or custom versioning, by the version the
     * request asks for.
     *
     * @param {(string | RouteInfo)[]} routes
     * @returns {MiddlewareConfigProxy}
     */
    exclude(...routes: (string | RouteInfo)[]): MiddlewareConfigProxy;
    /**
     * Attaches either routes or controllers to the current middleware.
     * If you pass a controller class, Nest will attach the current middleware to every path
     * defined within it.
     *
     * @param {(string | Type | RouteInfo)[]} routes
     * @returns {MiddlewareConsumer}
     */
    forRoutes(...routes: (string | Type<any> | RouteInfo)[]): MiddlewareConsumer;
}
```

알만 하잖아요

여기에서 RouteInfo 다음과 같습니다
```TypeScript
export interface RouteInfo {
    path: string;
    method: RequestMethod;
    version?: VersionValue;
}
```

직접 설정할 수도 있는 거고
@Controller를 붙인 클래스를 넣을 수도 있습니다