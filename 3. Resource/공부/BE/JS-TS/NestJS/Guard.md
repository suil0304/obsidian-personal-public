---
노트 생성 시각: "2026년 11월 10일 21시 21분"
tags:
  - BE
---

가장 단순하게 보자면 [[3. Resource/공부/BE/용어/미들웨어|미들웨어]] 중 하나라 볼 수 있겠습니다

주로 인증/인가에 많이 쓰이기는 합니다만
그렇다고 여기에서만 쓰이는 것도 아니에요

이름값을 적당히 아주 잘 하는 친구라고도 부를 수 있겠는데
현재 요청이 다음으로 넘어가도 되는지 검사하는 친구라 생각하시면 됩니다

벽이 5개가 있고
문이 다 달려 있는데
그 앞에 가드가 있는 그러한 느낌

맨 앞의 가드가 막으면 뒤도 자연스럽게 막힌 것처럼 볼 수 있겠고
뭐 아무튼

# CanActivate
Guard는 CanActivate를 구현함으로서 만들 수 있습니다

```TypeScript
import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";
import { Observable } from "rxjs";
  
@Injectable()
export class AuthGuard implements CanActivate {
    canActivate(context:ExecutionContext):boolean | Promise<boolean> | Observable<boolean> {
	    const httpContext = context.switchToHttp();
	    return this.__validateRequest(httpContext.getRequest());
    }
      
    private __validateRequest(request:any):boolean { // CanActivate에는 없는 함수입니다
        return true;
    }
}
```

return에서 true일 때 넘기고 false면 막는다는 흐름이 보이는 것 같구요
좋네요

# ExecutionContext
미들웨어와 가장 다른 점 중 하나가 바로
실행 문맥을 직접 가져올 수 있다는 것입니다
그것도 플랫폼에 종속되지 않으면서

```TypeScript
/**
 * Interface describing details about the current request pipeline.
 *
 * @see [Execution Context](https://docs.nestjs.com/guards#execution-context)
 *
 * @publicApi
 */
export interface ExecutionContext extends ArgumentsHost {
    /**
     * Returns the *type* of the controller class which the current handler belongs to.
     */
    getClass<T = any>(): Type<T>;
    /**
     * Returns a reference to the handler (method) that will be invoked next in the
     * request pipeline.
     */
    getHandler(): Function;
}

/**
 * Provides methods for retrieving the arguments being passed to a handler.
 * Allows choosing the appropriate execution context (e.g., Http, RPC, or
 * WebSockets) to retrieve the arguments from.
 *
 * @publicApi
 */
export interface ArgumentsHost {
    /**
     * Returns the array of arguments being passed to the handler.
     */
    getArgs<T extends Array<any> = any[]>(): T;
    /**
     * Returns a particular argument by index.
     * @param index index of argument to retrieve
     */
    getArgByIndex<T = any>(index: number): T;
    /**
     * Switch context to RPC.
     * @returns interface with methods to retrieve RPC arguments
     */
    switchToRpc(): RpcArgumentsHost;
    /**
     * Switch context to HTTP.
     * @returns interface with methods to retrieve HTTP arguments
     */
    switchToHttp(): HttpArgumentsHost;
    /**
     * Switch context to WebSockets.
     * @returns interface with methods to retrieve WebSockets arguments
     */
    switchToWs(): WsArgumentsHost;
    /**
     * Returns the current execution context type (string)
     */
    getType<TContext extends string = ContextType>(): TContext;
}
```

저희는 switchToHttp로 http의 context를 가져올 수 있겠구요
context에서 request, response, next를 가져올 수 있습니다

# 상태 코드
기본적으로는 403 Forbidden입니다
인가 없음을 나타내는 것을 반환하고 있으니 인증 자체를 실패했다면 UnauthorizedException을 던지면 되겠죠
다른 경우에도 마찬가지가 될 수 있겠구요

API 요청 한도에 다다랐다 하면 뭐 그런 Exception 내뱉고 하는 거구요

# 사용
Controller의 Get 붙는 쪽에 UseGuards를 붙이면 됩니다
순서대로 적용되구요

## provider로 사용
다른 곳에서도 인스턴스를 재사용해야 하거나
의존성을 주입 받을 때 사용합니다

간단합니다
모듈 파일의 providers에 Guard를 추가하고 UseGuards에 추가하시면 됩니다

## 전역
글로벌의 경우에도 간단합니다

```TypeScript
import { testMiddleware } from "./middlewares/test.middleware.ts";
import { AuthGuard } from "./guards/auth.guard.ts";

async function bootstrap() {
	const app = await NestFactory.create(AppModule);
	
	app.useGlobalGuards(new AuthGuard());
	
	await app.listen(process.env["PORT"] ?? 3000);
}

void bootstrap();
```

## APP_GUARD
@nestjs/core에는 APP_GUARD라는 것이 존재합니다

```TypeScript
import { Module } from "@nestjs/common";
import { APP_GUARD } from "@nestjs/core";
import { AuthGuard } from "./guards/auth.guard.ts";

@Module({
	providers: [
		{
			provide: APP_GUARD,
			useClass: AuthGuard
		}
	]
})
class AppModule {}
```

이러면 앱 전체로 가드가 적용되는데
app.useGlobalGuards와의 차이점으로는 DI까지 알아서 해줍니다