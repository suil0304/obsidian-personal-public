---
노트 생성 시각: "2026년 11월 14일 20시 15분"
tags:
  - BE
---

RxJS는 Reactive Extensions for JavaScript의 줄임입니다
반응형 프로그래밍 구현하고 싶어서 만들어진 라이브러리에요

# Promise와의 비교
Promise는 기본적으로 하나의 비동기 처리에 대해 적합합니다

지속적으로 가져온다던가
여러 비동기 결과를 조합한다던가
들어오는 값을 조건에 맞게 다른 곳으로 전달 등등

이런 것들을 Promise로 표현하기에는 좀 그렇잖아요

이런 상황들을 추상화하기 위해 Observable이라는 것을 제공합니다
interface 아니구요

# 데이터 흐름
Observable이 데이터 스트림
원천입니다

여러 데이터를 따라서 Observer(소비자)에게 닿는 그러한 느낌이구요

# Observable
이 패키지의 존재 의의

이름이 되게 고능하게 생겨서 어려워 보이는 것이지
사실 되게 쉽습니다

```TypeScript
import { Observable } from "rxjs";

const observable = new Observable<number>((subscriber) => { // subscriber.next에 넘길 때 등의 타입이 제네릭입니다
	subscriber.next(0);
	subscriber.next(0);
	subscriber.next(0);
	subscriber.next(1);
	
	subscriber.complete();
});

observable.subscribe(); // 구독이라는 도메인 관점에서 바라보는 execute라 생각해도 좋습니다
```

이러면 아무 것도 실행되지 않구요

사실 실행되기는 했는데
로그를 안 찍게 해서 안 보이는 것이네요
이러언

## observable.subscribe
1번째 인수는 오버로드되어 있습니다
함수만 넘기면 subscriber.next를 덮어 씌우는 함수가 되구요

옵션을 넘길 수도 있는데
next, error, complete 총 3개를 넘길 수 있어요
```TypeScript
export interface Observer<T>
{
    next: (value: T) => void;
    error: (err: any) => void;
    complete: () => void;
}
```

그냥 호출해도 됩니다

반환값은 Subscription 객체입니다

## observable.pipe
자세한 것은 [[rxjs#Operators|Operators]]에서 알아보세요

## Cold/Hot Observable
갑자기 차갑고 따뜻한게 왜 나오냐 싶으실 수도 있겠구요

구독자와 독립이냐 아니냐 그런 느낌이에요

### Cold Observable
구독할 때마다 값을 생산하는(subscribe, 실행 등등) 녀석입니다

### Hot Observable
데이터 원천은 그대로 있고
공통된 스트림에서 우리 쪽으로 데이터가 날라오는 방식입니다

대표적으로 Subject를 이용해 구현 가능하다고 하구요

```TypeScript
import { Subject } from "rxjs";

const subject = new Subject<number>();

subject.subscribe();

subject.next(1);
subject.next(1);
```

## 고차 Observable
고차 함수처럼 똑같습니다
Observable이 next로 넘기는 값이 Observable이에요

# Subscription
구독 정보를 관리하는 객체입니다
Observable의 subscribe 반환값으로 획득할 수 있구요

## subscription.unsubscribe
대충 구독 취소할 수 있습니다

## subscription.add
하면 윗 Observable을 구독 취소했을 때 넣은 Observable도 함께 구독 취소됩니다

```TypeScript
const subscription = observable.subscribe(console.log);

subscription.add(
    anotherObservable.subscribe(console.log)
);

subscription.unsubscribe();
```

## subscription.remove
알만 하잖아요

# Operators
그리고 Observable에 이러한 연산자(함수)들을 넣어 돌릴 수 있습니다

예시는 이런 느낌이구요
```TypeScript
import { from } from "rxjs";
import { filter, map } from "rxjs/operators";

from([1, 2, 3, 4, 5]).pipe(
    filter(value => value % 2 === 0),
    map(value => value * 10)
).subscribe(console.log);
```

pipe는 pipe에 들어간 operators를 포함하도록 새로운 Observable을 생성해 반환합니다
대충 이런 느낌이구요
```TypeScript
const source = new Observable<number>(subscriber => {
    subscriber.next(10);
});

const mapped = new Observable<number>(subscriber => {
    source.subscribe({
        next(value) {
            subscriber.next(value * 2);
        }
    });
});
```

## 고차 Operators
### mergeMap
내부 Observable를 구독한 후 결과를 병합합니다

### concatMap
내부 Observable을 순서대로 구독해놓습니다

### switchMap
새로운 Observable이 오면 기존 Observable을 버리고 갈아 끼웁니다

### exhaustMap
새로운 Observable이 와도 기존 Observable이 있으면 무시합니다