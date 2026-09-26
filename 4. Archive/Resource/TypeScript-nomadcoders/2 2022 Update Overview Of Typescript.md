> [!note]+ # #2.0 How Typescript Works
> 어떻게 동작하는가
> 
> JS로 넘어가기 전에 벌어질 수 있는 모든 컴파일 타임 에러를 제거하는 것을 목표로 하고 있구요
> 생산성이 매우 올라가죠
> 당연함
> ㅇㅇ

> [!note]+ # #2.1 Implict Types  vs Explict Types
> 사람에 따라 강박증으로 타입을 적어줄 수 있겠으나
> 일단은 타입을 명시하지 않아도 추론해주구요
> 좋잖아용
> 
> 하지만 명시적으로 적어야 하는 경우도 많으니 그 부분을 신경 썼으면 좋겠구요
> 이러언

> [!note]+ # #2.2 Types of TS part One
> TS에는 JS의 기본적인 원시 타입들
> 
> ```typescript
> string;
> number;
> boolean;
> object;
> Array;
> undefined;
> null
> ```
> 
> 에 추가적인 타입을 정의하여 사용할 수 있구요
> 이러언
> 
> TS는 타입 추론 기능이 존재하기 때문에
> 
> ```typescript
> const player = {
> 	name: "수리",
> 	role: "프로그래머"
> };
> ```
> 
> 와 같은 객체를 선언하여 자동 완성을 보면???
> 
> ![[image 6.png]]
> 
> 아주좋았어
> 
> 타입 정해주면서 어떤 프로퍼티는 optional로 가게 할 수도 있구요
> 크하하
> 
> 만약 코드를 이따구로 짰다고 한다면
> 
> ```typescript
> const player:{
> 	name:string,
> 	age?:number
> } = {
> 	name: "수리"
> }
> ```
> 
> age는 optional이 되구요
> 
> ```typescript
> if(player.age > 10) {}
> ```
> 
> 와 같이 비교하려 시도했을 때
> 
> age는 optional이라 undefined가 될 수도 있는 것이구요
> 
> 그래서 이렇게 되는 것이구요
> 
> ![[image 7.png]]
> 
> 적어도 컴파일 타임에서 벌어질 수 있는 모든 것들을 걸러주기 때문에
> 아주 좋구요
> 
> 근데 player 관련 변수를 선언할 때마다 저따구로 쓰면 더 길어질 것임을 알고 있구요
> 
> type을 선언해볼 때가 온 것 같구요
> 크하하
> 
> ```typescript
> type Player = {
> 	name:string,
> 	age?:number
> };
> ```
> 
> 이러면 Player 타입을 선언했구요
> 
> ```typescript
> const player:Player = { /* ... */ };
> ```
> 
> 이렇게 타입을 사용할 수도 있구요
> 
> 당연하지만 TypeAlias로써 다음과 같이 작성할 수 있구요
> 
> ```typescript
> type Age = number;
> ```
> 
> 물론 이것은 상당한 낭비에 지옥이 될 수 있기 때문에
> 
> 적어도 유니온 타입에서 사용하는게 좋을 것이구요
> 이러언
> 
> 함수의 매개변수와 리턴 타입도 명시할 수 있구요
> 
> ```typescript
> function playerMaker(name:string, age?:number):Player { /* ... */ }
> ```
> 
> 다음과 같이 작성하는 것이 가능하구요
> 크하하
> 
> 화살표 함수도 동일하구요
> 
> ```typescript
> const playerMaker = (name:string, age?:number):Player => { /* ... */ };
> ```

> [!note]+ # #2.3 Types of TS part Two
> TS는 이보다 더 많은 기능을 지원하고 있구요
> 
> readonly도 그 중 하나구요
> 
> ```typescript
> type Player = {
> 	readonly name:string,
> 	age?:number
> };
> ```
> 
> name은 이러면 readonly가 되어 처음 한 번만 값을 설정할 수 있는 const 비스무리한 무언가가 되는 것이구요
> 크하하
> 
> 저런 것은 Array에도 붙일 수 있구요
> 
> ```typescript
> const numbers:readonly number[] = [1, 2, 3, 4];
> ```
> 
> ![[image 8.png]]
> 
> 다음과 같구요
> 
> ReadonlyArray였나 해서 따로 타입이 있던 것으로 기억하고 있구요
> 
> readonly를 빼면
> 
> ![[image 9.png]]
> 
> 다음과 같이 나오구요
> 이러언
> 
> 요소 개수와 타입을 튜플처럼 맞춰 타입으로 지정할 수 있구요
> 크하하
> 
> 만약 아래와 같이 작성하게 된다면
> 
> ```typescript
> const elements:[string, number, boolean] = [];
> ```
> 
> ![[image 10.png]]
> 
> 다음과 같이 에러를 내주고 있구요
> 
> ![[image 11.png]]
> 
> 이러면 이제 잘 되네용
> 아주좋았어
> 
> 심지어 어디 위치에 어떠한 타입이 있을지 TS가 아는 상태이기 때문에
> 
> ![[image 12.png]]
> 
> 인덱스 접근으로 값을 넣으려 해도 잘 막아준다고 하네용
> 오우
> 
> any라는 것도 있는데
> 
> 이것은 더 무거운 뭣 같은 JS니 그렇게 생각해주시길 바라구요
> 이러언

> [!note]+ # #2.4 Types of TS part Three
> 이번에는 void와 unknown, never를 알아볼 예정이구요
> 
> ## unknown
> 
> any와 무엇이 다른가 싶죠???
> 
> 이 친구는 값이 어떠한 타입으로 들어올지 모를 때 사용하는 타입이구요
> 
> any는 다 통과라면
> unknown은 일단 막고 해당 방향으로 사용 가능한 타입으로 좁혀야 하는 그런 타입이구요
> 
> ![[image 13.png]]
> 
> ![[image 14.png]]
> 
> 그래서 다음과 같이 사용해야 하구요
> any를 사용해야 할 것 같은 거의 모든 상황 속에서
> unknown도 충분히 쓸모가 있으니
> 제발 any는 웬만하면 사용하지 말았으면 하구요
> 씨
> 
> ## void
> 
> C나 뭐 그런 쪽에서 왔으면 알만 하잖아용
> 
> 반환값이 없는 형태
> 
> Python 같은 어디어디의 어디 개 같은 언어는 기본 None 반환이라 이러언이지만
> 
> TS에서는 반환값을 명시하지 않는 한 기본 void구요
> 
> 실제 JS에서는 값을 반환하지 않는 모든 함수 = undefined 반환이기 때문에
> 반환 타입 void의 함수 또한 JS에서는 undefined를 반환하구요
> 
> ![[image 15.png]]
> 
> 흐음
> 이게 되네
> 
> ## never
> 
> 이것은 에러가 나 절대 정상적으로 종료되면 안 되는 함수의 반환 타입으로 명시할 수 있구요
> 
> 그게 아닌 변수 등에 달아두면 그 변수는 아무 것도 담지 못 하는 잉여 변수가 되는 것이구요
> 
> 나중 이야기입니다만
> 
> string & number와 같이 해두면 string과 number가 겹치는 구석이 하나도 없기 때문에 never가 되어 아무 것도 넣을 수 없게 되구요
> 이러언
> 
> ## Union Type
> 
> 유니온입니다
> 
> 예를 들어
> 
> ```typescript
> let value:string | number;
> ```
> 
> 이렇게 했다면 string일 수도 number일 수도 있는 변수라는 뜻이 되구요
> 
> typeof 등으로 좁혀 사용이 가능하구요
> 이러언
> 