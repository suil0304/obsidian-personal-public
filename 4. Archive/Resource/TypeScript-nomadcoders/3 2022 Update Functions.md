> [!note]+ # #3.0 Call Signatures
> 이제부터 호출 시그니처를 만들 것이구요
> 
> ![[image 66.png]]
> 
> 이것을 화살표 함수로 만들면
> 
> ```typescript
> const add = (a:number, b:number):number => a + b;
> ```
> 
> 가 되구요
> 
> ![[image 67.png]]
> 
> 이러면 타입이 다음과 같이 나오구요
> 
> 저기에서 저 타입이 호출 시그니처인 것이구요
> 이러언
> 
> ```typescript
> type Add = (a:number, b:number) => number;
> ```
> 
> 이렇게 하면 인자로 number형 2개 받아서 number형을 반환하겠다는 것이 되구요
> 
> 이것을 타입으로 달아두면???
> 
> ![[image 68.png]]
> 
> 이렇게 함수 구성하는 것까지 도움을 받아서 구현할 수 있구요
> 아주좋았어

> [!note]+ # #3.1 Overloading
> Overloading에 대하여 배워보도록 하다
> 
> 저 호출 시그니처라는 것이
> 
> ```typescript
> type Add = {
> 	(a:number, b:number):number
> };
> ```
> 
> 로도 구현이 가능한
> 
> 그리고 또한
> 
> ```typescript
> type Add = {
> 	(a:number, b:number):number,
> 	(a:number, b:string):number
> };
> ```
> 
> 이렇게도 될 수 있는
> 
> 이게 바로 Overloading이구요
> 
> 저기에서 저래버리면 b에 대하여 number와 string의 유니온 타입을 지니게 됩니다
> 
> 타입을 typeof로 체크하며 사용해야 하구요
> 
> Next.js를 예로 들어보자면
> 
> ```typescript
> Router.push();
> ```
> 
> 이런 것이 있다고 하는데
> 
> 이게 path:string과 config:Config 둘 중 하나만 첫 번째 인자에 넣어도 동작해요
> Overloading이죠???
> 
> 이것도 타입 좁혀서 사용하는 것이구요
> 
> 아니면 매개변수 개수가 다를 수도 있구요
> 
> ```typescript
> type Add = {
> 	(a:number, b:number):number,
> 	(a:number, b:number, c:number):number
> };
> ```
> 
> 이런 것이 있는데
> 
> 이것을 타입으로 만들어 변수를 만들면
> 
> ![[image 69.png]]
> 
> 이딴 식으로 에러가 나구요
> 
> 여기에서 c는 undefined일 수도 있고 number일 수도 있는 상태인데
> 
> c는 정작 Add를 구현하는 화살표 함수에서 optional도 아니고 nullish하지 않은 값을 기대하고 있으니 터지는 것이구요
> 
> ![[image 70.png]]
> 
> 가장 간단하게는 c에 ?만 달아주는 것이지만
> 이러면 c가 무엇이 들어오는지 알 수 없다고 표현하고 있구요
> 
> ![[image 71.png]]
> 
> 명시를 해줘야 optional 의미까지 같이 붙어서 number | undefined가 되구요
> 
> 그래서 저것도 c가 undefined가 아닌 경우에 대하여 if를 돌리고 나눠버릴 수 있구요
> 크하하

> [!note]+ # #3.2 Polymorpism
> 다형성이구요
> 
> 다형성의 정의부터 알아보자면
> 
> poly + morphos +-ism이죠???
> 
> ![[image 72.png]]
> 
> ![[image 73.png]]
> 
> -ism은 뭐 그렇다고 치고
> 
> 그래서 다형성은 여러 가지 다른 형태를 가지고 있는 -성 이렇게 이해할 수 있겠네용
> 
> Overloading도 여기에 들어갈 수 있을 것 같구요
> 
> 그래서 제네릭이 어떻게 도움을 주는지 알아볼 예정이구요
> 
> 배열을 받아 그 내용물을 돌리고 출력하는 함수를 사용해볼 예정인데
> 그렇다고 any[]를 사용해버리면 아무 것이나 받아 다 출력하겠다는 소리고
> 무엇보다 any이면 모든 타입을 허용해버리는데요
> 배열 안 요소의 타입은 고정하면서 각기 다른 타입의 배열을 집어 넣을 수 있는 방법이 있을까 하면
> 그런 것이 제네릭 사용하라 있는 것이구요
> 
> 사실 이러한 종류에 대하여 제네릭 안 써도 구현은 가능함
> 
> ```typescript
> type SuperPrint = {
> 	(arr:number[]):void,
> 	(arr:boolean[]):void,
> 	(arr:string[]):void,
> 	// ...
> };
> ```
> 
> 근데 이걸 언제까지 다 나열하면서 구현해요
> 이게뭐야
> 
> 그래서 이럴 때 제네릭을 사용하는 것이구요
> 
> 아까와 같이 type에 담아두면
> 
> ```typescript
> type SuperPrint = {
> 	<T>(arr:Array<T>):void
> };
> ```
> 
> 라 명시할 수 있겠구요
> 
> 이러면 TS도 제네릭 사용하는구나 하고 알아서 추론 가능하니 무엇을 넣든 그 값으로 맞춰주니
> 아주좋았어
> 
> 그리고 이런 것이 바로 다형성이구요
> 
> 저 T 타입 매개변수는 반환 타입에도 사용할 수 있으니 이러언하여 이러언하기를 바라구요
> 크하하

> [!note]+ # #3.3 Generics Recap
> 다시 정리하며 복습하는 시간
> 
> 쉽잖아용
> 아마도

> [!note]+ # #3.4 **Conclusions **
> 그래서 결론적으로는 이런 것도 사용하기 나름이구요
> 
> 제네릭은 또한 아예 변수에 달아서 이러언시킬 수도 있으니까요
> 좋잖아용
> 이-히히
> 
> 아주 쓸만하니 꼭 알아두면 좋을 것 같구요