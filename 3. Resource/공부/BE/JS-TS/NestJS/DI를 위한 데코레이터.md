# [[클래스 데코레이터#Injectable|Injectable]]
참고하세요

# Inject
*field/property*
*param*

가정을 하나 해봅시다

```TypeScript
@Injectable()
class ServiceA {
	doSomething() {
		return "Hello from A";
	}
}

class BaseService {
	constructor(protected readonly _serviceA:ServiceA) {}
	
	getHello() {
		return "Hello, world!";
	}
	
	doSomethingFromServiceA() {
		return _serviceA.doSomething();
	}
}
```

이런 기본 서비스를 정의한 후 상속 받게 함으로서 구현할 수도 있는 거잖아요?

```TypeScript
@Injectable()
class ServiceB extends BaseService {
	override getHello() {
		return this.doSomethingFromServiceA();
	}
}
```

이제 ServiceB를 Controller에서 주입 받도록 하면
저희가 생각하는 DI 그래프는 Controller가 루트에 있고 ServiceB가 중간, ServiceA가 가장 밑으로 오는 그림일 것이란 말이죠?

근데 여기에서 BaseService는 하다 못 해 Injectable을 달아 두지도 않아서 NestJS에 등록되어 있지를 않기 때문에 DI 대상에서 벗어나게 되구요
그래서 이대로 실행하면 \_serviceA가 정의되어 있지 않다고 에러가 납니다

해결 방안 1
모든 자식들이 알아서 DI를 받은 후 super로 넘긴다
fun하고 cool하고 sexy하지 않습니다

해결 방안 2
Inject 사용하기
그렇습니다

```TypeScript
class BaseService {
	@Inject(ServiceA) protected readonly _serviceA:ServiceA;
	
	getHello() {
		return "Hello, world!";
	}
	
	doSomethingFromServiceA() {
		return _serviceA.doSomething();
	}
}
```

아주 좋았어

이 친구는 매개변수에도 사용 가능한 것 같구요

받는 값은 InjectionToken | FowardReference로 되어 있네요

```TypeScript
/**
 * @publicApi
 */
export type InjectionToken<T = any> = string | symbol | Type<T> | Abstract<T> | Function;

export interface ForwardReference<T = any> {
    forwardRef: T;
}
```

그렇습니다
ForwardReference는 forwardRef 함수 반환값 사용하세요
괜히 따로 구현해보겠다 하지 마시고
아이고야

# Global
*class*

Module에 붙여 사용합니다
전역으로 만들어주구요

루트에서 딱 한 번만 등록하면 됩니다