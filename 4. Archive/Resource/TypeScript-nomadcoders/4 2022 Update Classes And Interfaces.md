> [!note]+ # #4.0 Classes
> 프로토타입이라는 무언가를 사용하는 언어인 주제에
> class를 지원하다???
> class가 객체지향 그 자체인 것은 아니지만 뭐 그렇단 말이죠
> 
> 심지어 여기 class는 프로토타입 상속의 문법 설탕 위치에 해당하구요
> 씨
> 
> 추상 클래스
> 제네릭
> 다형성
> 
> 이 모든 것들을 TypeScript로 구현할 수 있구요
> 이건 좋은가
> 
> ```typescript
> class Player {
>     constructor(
>         private firstName:string,
>         private lastName:string
>     ) {}
> }
> ```
> 
> 생성자 내부에서 명시 및 초기화를 자동으로 해주구요
> 
> JS는 심지어 class 구현이 정상적이지 않고 동적 특유의 무언가가 private public 구분까지 안 해두어서
> 엿 같은 무언가가 되었습니다만
> 
> TS는 그래도 컴파일 타임에서 private public 접근 제한자를 추가하여 끼얏호우할 수 있구요
> 좋네요
> 
> ![[image 118.png]]
> 
> 아주좋았어
> 
> abstract class도 있구요
> 
> ```typescript
> abstract class User {
> 		constructor(
>         private firstName:string,
>         private lastName:string
>     ) {}
> }
> ```
> 
> abstract class는 직접 생성자를 호출하여 인스턴스를 만들 수 없구요
> 당연한 소리잖아용
> ㅇㅇ
> 
> ![[image 119.png]]
> 
> 잘 잡아주고 있구요
> 아주좋았어
> 
> 아무튼
> 기존의 객체를 {}로 만들던 무언가가 class에도 섞여서
> var나 function이 없어도 알아서 잘 만들어지는 것이구요
> 
> ![[image 120.png]]
> 
> 어디어디 다른 세계의 class는 기본 protected라서 명시를 안 하면 본인과 자식에 대하여만 사용 가능하단 말이죠???
> 
> 하지만 여기는 명시하지 않으면 기본 public이라는 괴상한 설정이구요
> 
> abstract class의 꽃 중 하나인 일부 메서드 구현 미루기 기능도 있구요
> 
> ```typescript
> abstract class User {
>     constructor(
>         private readonly firstName:string,
>         private readonly lastName:string
>     ) {};
> 
>     abstract getFullName():string;
> }
> ```
> 
> ![[image 121.png]]
> 
> 아주 좋죠
> 이거지
> 
> Player는 저 getFullName을 구현해야만 하는 제약을 받습니다
> interface의 느낌이 나는게 맞구요
> 
> 아무튼
> private로 만들었으면 그 밑의 모든 자식도 사용하지 못 하구요
> 
> protected를 붙이면 자식도 사용 가능해지겠죠
> 
> ```typescript
> abstract class User {
>     constructor(
>         protected readonly firstName:string,
>         protected readonly lastName:string
>     ) {};
> 
>     abstract getFullName():string;
> }
> 
> class Player extends User {
>     getFullName():string {
>         return `${this.firstName} ${this.lastName}`;
>     }
> }
> 
> const player = new Player("수리", "독");
> 
> player.getFullName();
> ```
> 
> 아주좋았어

> [!note]+ # #4.1 Recap
> 복습의 시간이구요
> 
> 실전-연습으로 사전을 만들어볼 것이구요
> 아주좋았어
> 
> 새 단어 추가
> 찾기
> 삭제
> 위와 같은 메서드를 구현해볼 예정이구요
> 
> words를 private로 선언하는데
> 생성자에서 선언하지 않고 필드로 선언해주도록 합시다
> 
> 그 전에 타입 먼저 선언해줄 예정이구요
> 
> ```typescript
> type Words = {
> 	[key:string]:string
> };
> ```
> 
> 이를 이용하여 다음과 같이 만들 수 있구요
> 
> ```typescript
> class Dict {
> 	private words:Words;
> 	
> 	constructor() {
> 		this.words = {};
> 	}
> }
> ```
> 
> 근데 저 정도는 Record<string, string>으로 해결이 가능하긴 함
> ㅇㅇ
> 
> Word class도 만들어 봅시다
> 
> 아주좋았어
> 
> ```typescript
> class Word {
>     constructor(
>         public term:string,
>         public def:string
>     ) {}
> }
> ```
> 
> 그런 후 Dict에 여러 메서드를 추가해보다
> 
> ```typescript
> class Dict {
>     private words:Words;
> 
>     constructor() {
>         this.words = {};
>     }
> 
>     add(word:Word):void {
>         if(this.words[word.term] === undefined) {
>             this.words[word.term] = word.def;
>         }
>     }
> 
>     getWord(term:string):string | undefined {
>         return this.words[term];
>     }
> }
> ```
> 
> 아주좋았어

> [!note]+ # #4.2 Interfaces
> 이유가 있어 public으로 term과 def를 선언하였지만
> 수정 불가능이 필요할 듯 하구요
> 
> readonly를 붙이면 읽기 전용이 되어 클래스 내부에서도 상수 느낌을 가져올 수 있게 되구요
> 이러언
> 
> 그리고 static도 있는데
> 이것은 의외로 JS에도 있는 문법이었구요
> 호오
> 
> static을 붙이면 메모리 정적이 되어 인스턴스를 생성하지 않아도 바로 사용할 수 있게 되구요
> 
> 이제 interface에 대하여 알아보도록 해보구요
> 
> type과는 약간 다른 것을 알아야 하구요
> 
> interface는 애초에 다른 대부분의 객체지향에 있는 interface를 상당 부분 가져온 무언가라서
> 
> 타입은 alias든 유니온이든 제한이든 다 가능하지만
> interface는 객체 형태만 제한하는 것이라 이해하면 좋구요
> 
> 그리고 또한 interface는 상속도 가능하구요
> 좋잖아요

> [!note]+ # #4.3 Interfaces part Two
> abstract class와 interface
> 상황마다 어떤 것이 더 좋고 어떤 것이 더 좋은지 선호할 수 있는 기능들이 나눠져 있음
> 
> ## abstract class
> 
> abstract class는 자기 자신은 구현하지 않지만
> 다른 class가 구현해야만 할 필드와 메서드를 직접 명시하는 행동이 가능하구요
> 
> 그러면서 기본 구현까지 넣을 수 있는 것이 abstract class의 본질이라 생각하면 편하구요
> 
> 근데 class라는 것은 어찌 되었든 JS에 넘어가고
> 더 무거워진다는 소리가 됩니다
> 
> ## interface
> 
> 반면 interface는 단순 타입이기 때문에
> JS로 넘어가면 사라지구요
> 
> 또한 어차피 JS라서 상관 없을지도 모르겠지만
> interface와 구현 관계인 것을 이용하여 뭐 그런 것도 가능하단 말이죠???
> 
> 그것도 불가능하구요
> 
> 이것은 interface 특유의 그것이지만
> 명세서로써 읽기 좋은 것이 interface잖아용???
> 
> private나 protected는 명시가 불가능합니다
> 
> 모든 것이 public해지는 마법이 되구요
> 
> 이런 것들 막고 싶으면 abstract class 사용하시면 되겠구요
> 이러언
> 
> 마지막으로
> 당연히 타입이기 때문에
> interface는 생성자도 못 만들구요
> 아쉬운 것이기 때문에
> 이러언
> 
> ## 상속과 구현
> 
> 대부분의 클래스를 가지고 있는 객체지향 언어는 다이아몬드 문제를 매우 경계하기 때문에
> 정상적인 방법으로 다중 상속을 만들 수는 없구요
> 
> 하지만 interface는 단순한 제약에 불과하지 구현 등 복잡한 것이 따라오는 것은 아니기 때문에
> 다중 구현이 가능하다는 매우 큰 장점이 있구요
> 
> 좋잖아요

> [!note]+ # #4.4 Recap
> 복습하는 시간이구요
> 이러언
> 
> type은 식별자 중복을 허용하지 않지만
> interface는 namespace처럼 융합이 가능해지구요

> [!note]+ # #4.5 Polymorphism
> 다형성
> 제네릭
> class
> interface
> 
> 모든 것을 다 합쳐볼 시간이구요
> 
> 이제부터 실제 브라우저에 쓰이는 Storage API를 따라 만들어 봅시다
> 
> 일단 해보면서 시작하는 것이 좋기 때문에
> 
> LocalStorage class를 먼저 구현하면서 시작해보자구요
> 
> ```typescript
> class LocalStorage {
> 	
> }
> ```
> 
> 그래서 무엇을 먼저 구현해보다???
> 
> private storage를 선언하는데
> 
> 그 전에 storage는 다음과 같이 정의된 interface가 타입인
> 하지만 이미 Storage interface는 정의되어 있기 때문에
> SStorage라 지어주도록 합시다
> 
> ```typescript
> interface SStorage {
> 
> }
> ```
> 
> 이제 제네릭으로 구현
> 
> ```typescript
> interface SStorage<T> {
>     [key:string]:T
> }
> 
> class LocalStorage<T> {
>     private storage:SStorage<T>;
> 
>     constructor() {
>         this.storage = {};
>     }
> }
> ```
> 
> 타입 매개변수 T는 당연하지만 다른 타입의 제네릭에 넘겨줄 수도 있구요
> 
> 그래서 다음과 같이 만들 수 있을 것 같구요
> 
> ```typescript
> interface SStorage<T> {
>     [key:string]:T
> }
> 
> class LocalStorage<T> {
>     private storage:SStorage<T>;
> 
>     constructor() {
>         this.storage = {};
>     }
> 
>     set(key:string, value:T):void {
>         this.storage[key] = value;
>     }
> 
>     remove(key:string):void {
>         delete this.storage[key];
>     }
> 
>     get(key:string):T | undefined {
>         return this.storage[key];
>     }
> }
> ```
> 
> 사용할 때는 다음과 같이 사용하면 되구요
> 
> ```typescript
> const localStorage = new LocalStorage<string>();
> ```
> 
> string을 저장하는 Storage가 탄생하게 된 것이구요
> 
> ```typescript
> localStorage.set("a", "b");
> ```
> 
> 이런 식으로 저장할 수 있겠구요
> 좋잖아요