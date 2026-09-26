> [!note]+ # #3.0 Introdution to Testing in Nest
> package.json에 가보다
> 
> ```json
> // package.json
> {
> 	// ...
> 	"scripts": {
> 		"test": "jest",
>     "test:watch": "jest --watch",
>     "test:cov": "jest --coverage",
>     "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
>     "test:e2e": "jest --config ./test/jest-e2e.json"
> 	}
> 	// ...
> }
> ```
> 
> 각각
> 
> test
> test:watch
> test:cov
> test:debug
> test:e2e
> 
> 이렇게 있는데
> 
> test:debug 제외하고는 전부 Jest를 사용하네요
> 
> Jest가 무엇인지 알아볼 필요가 있어졌구요
> 이러언
> 
> Jest는 JS를 아주 쉽게 테스팅할 수 있는 npm package라고 하구요
> 
> NestJS가 다 해줬잖아이기 때문에 우리는 딸ㅋㅋ깍ㅋㅋ으로 사용할 수 있구요
> 
> 지금까지 @nestjs/cli로 Controller, Service 등을 생성했을 때
> name.~~.spec.ts 이렇게 되어 있는 파일도 함께 생성되었죠?
> 
> spec은 테스팅 기능이 들어 있는 파일이구요
> 
> name.controller.ts가 있을 때
> name.controller.spec.ts는 name.controller를 테스트하는 파일이라는 뜻이 된다고 하네요
> 이러언
> 
> 근데 싹 다 지웠잖아
> DROP TABLE spec_files;
> 
> 아무튼 Jest가 .spec.ts으로 끝나는 것을 자동으로 찾아볼 수 있도록 설정되어 있구요
> 
> 그래서 우리는 실행하다 스크립트를
> 
> ```bash
> npm run test:cov
> ```
> 
> 여기에서 cov라고 하는 것은???
> coverage를 줄인 것으로써???
> 한국어로 대충 번역하자면
> 범위라고 하네요
> 이러언
> 
> 그래서 이것을 실행하면
> 얼마나 코드가 테스팅 되었는지
> 또는 안 되었는지 등을 보여준다고 하구요
> 
> ![[image 102.png]]
> 
> 당연하게도 모든 .spec.ts 파일을 지워버렸기 때문에 찾지를 못 하고 있구요
> 
> 그러면 어떡함???
> 
> 다음을 추가하여 일단 다시 테스트해보다
> 
> ```typescript
> // /src/movies/movies.service.spec.ts
> import { Test, TestingModule } from "@nestjs/testing";
> import { MoviesService } from "./movies.service";
> 
> describe("MoviesService", () => {
>     let service:MoviesService;
> 
>     beforeEach(async () => {
>         const module:TestingModule = await Test.createTestingModule({
>             providers: [MoviesService]
>         }).compile();
> 
>         service = module.get<MoviesService>(MoviesService);
>     });
> 
>     it("should be defined", () => {
>         expect(service).toBeDefined();
>     });
> });
> ```
> 
> ![[image 103.png]]
> 
> 오
> 
> 저기에서 나오는 Stmts, Branch, Funcs, Lines, Uncovered Line에 대하여
> 
> AI said:
> 
> | **항목** | **의미** | **설명** |
> | --- | --- | --- |
> | `**% Stmts**` | **구문(문장) 커버리지** | 코드 내의 모든 개별 명령문(Statement)이 실행된 비율. |
> | `**% Branch**` | **분기 커버리지** | `if`, `switch` 등 조건문의 모든 선택지(True/False)가 실행된 비율. |
> | `**% Funcs**` | **함수 커버리지** | 선언된 전체 함수 중 최소 한 번 이상 호출된 함수의 비율. |
> | `**% Lines**` | **라인 커버리지** | 소스 코드의 실제 줄(Line) 단위로 실행 여부를 측정한 비율. |
> | `**Uncovered Line #s**` | **미실행 라인 번호** | 테스트 중에 **실행되지 않고 누락된 실제 코드의 줄 번호**. |
> 
> 그렇다고 하네요
> 이러언
> 
> 이번엔 test:watch를 실행시켜보다
> 
> ```bash
> npm run test:watch
> ```
> 
> ![[image 104.png]]
> 
> a를 누르면 전체 테스트(.spec.ts)를 돌려본다고 하네용
> 
> ![[image 105.png]]
> 
> 오
> 
> 지금 있는 .spec.ts는 movies.service.spec.ts가 유일하기 때문에
> 이것만 테스트된 모습을 볼 수 있었구요
> 
> 이제 몇 가지 테스트를 추가해보다
> 
> 두 가지 테스팅이 있는데
> 
> > [!note]+ 하나는 유닛 테스팅
> > 서비스에서 분리된 유닛을 테스팅하는 것이구요
> > 그래서 함수를 따로 테스트한다 생각하면 될 것 같구요
> > 
> > 그래서 예를 들어
> > getAll 메서드 단일 테스팅을 한다던가
> > getOne 메서드 단일 테스팅 등을 수행할 때 유용할 것이라 하구요
> 
> > [!note]+ 또 하나는 end-to-end 테스팅(e2e)이구요
> > 이건 모든 시스템을 테스팅하는 것이구요
> > 
> > e2e 테스팅은 이 페이지로 가면 특정 페이지가 나와야 하는 경우 사용한다 하는데
> > 
> > 간단하게 사용자 입장에서 생각해보다:
> > 
> > 특정 링크 클릭 → 이 링크의 내용물을 볼 수 있어야 함
> > 
> > 그런 것을 테스트하는 것이라 하네용
> > 
> > 사용자가 취할만한 행동 하나 하나를 Brute Force마냥 처음부터 끝까지 테스트하는 무언가라 생각할 수 있구요
> > 
> > 마침 e2e는 package.json의 scripts에 이미 있구요
> > 
> > ```bash
> > npm run test:e2e
> > ```
> 
> 유닛 테스팅을 이용하여 MoviesService를 테스트해보다
> 
> 아까 전에 해본 것 아니었냐구요?
> 
> 다르죠 그거와는
> ㅇㅇ
> 
> 유닛 테스팅을 이용하겠다는 것은 MoviesService의 메서드 하나 하나를 뜯고 맛보고 즐기는 방식으로 테스트하겠다는 소리구요

> [!note]+ # #3.1 Your first Unit Test
> Service 파일을 실컷 만들어 놓고는 어떻게 테스트 파일을 작성하는지 조차도 모르고 있는 상태죠???
> 
> 테스트 파일
> 그러니까 .spec.ts 파일을 작성하는 방법에 대해 Learning With Pibby
> 씨
> 
> 그래서 우리는 아까 봤던 Jest를 사용하다
> 이-히히
> 
> ```typescript
> // /src/movies/movies.service.spec.ts
> import { Test, TestingModule } from "@nestjs/testing";
> import { MoviesService } from "./movies.service";
> 
> describe("MoviesService", () => {
>     let service:MoviesService;
> 
>     beforeEach(async () => {
>         const module:TestingModule = await Test.createTestingModule({
>             providers: [MoviesService]
>         }).compile();
> 
>         service = module.get<MoviesService>(MoviesService);
>     });
> 
>     it("should be defined", () => {
>         expect(service).toBeDefined();
>     });
> });
> ```
> 
> 이것을 바탕으로 코드를 뜯어 흡수하다
> 아주좋았어
> 
> > [!note]+ ## describe
> > 테스트를 묘사하다
> > 
> > describe(말하다, 묘사하다)는 흔히 쓰는 영단어이니 알아둬야 했구요
> > 이러언
> 
> > [!note]+ ## beforeEach
> > 테스트하기 전에 실행하는 문이구요
> > 
> > 무언가를 정의하기 좋을 듯
> > ㅇㅇ
> > 
> > 그래서 이것은 각 테스트 전에 매번 실행한다는 소리가 되는 것이구요
> 
> > [!note]+ ## it
> > 안에 문자열과 함수를 넣고 있는
> > 
> > 보기에 따라
> > it “should be defined”라는 간단한 문장과
> > Individual Test(개별 테스트)의 줄임말로 볼 수 있을 듯
> > 
> > 차라리 직접 써보는게 이해하기 더 수월할 것이니 직접 적어보다
> > 
> > ```typescript
> > it("", () => {});
> > ```
> > 
> > 가장 기본적인 형태는 다음과 같을 것인데
> > 
> > 당연한 소리지만 it에서 문자열 매개인수는 마음대로 넣어도 되는 것이구요
> > 
> > 하지만 그럴싸한 이름을 넣어 내려야만 보기 좋고 크하하일 것이니
> > 
> > “banana 4” 이딴 것 넣어서 내리면 죽을 것이구요
> > 
> > 가장 기본적인 예시 테스트로 다음과 같은 코드를 만들어보다
> > 
> > ```typescript
> > it("should be 4", () => {...});
> > ```
> > 
> > 본문에 들어가는 테스트 부분에는 2+2라던가 1+3 이런 것들이 들어갈 것이구요
> > 
> > ### expect
> > 
> > 그래서 expect를 사용할 것이구요
> > 
> > ![[image 106.png]]
> > 
> > 안에 옵션이 굉장히 많네용
> > 
> > ```typescript
> > it("should be 4", () => {
> >     expect(2+2).toEqual(4);
> > });
> > ```
> > 
> > 다음을 눌러 터트려 테스트를 수행하다
> > 
> > 영어 직독직해로 가보자면
> > 
> > 2+2가 4와 같기를(toEqual) 기대하고(expect) 있는 것이구요
> > 
> > ![[image 107.png]]
> > 
> > should be 4가 통과한 모습을 볼 수 있구요
> > 
> > 근데 2+5가 4이기를 기대하게 되면???
> > 
> > ![[image 108.png]]
> > 
> > 실패했다고 이렇게 나와주네용
> > 
> > 이-히히
> > 
> > 바로 이렇게 테스트를 하는 거에요
> > 운동 많이 될 거야

> [!note]+ # #3.2 Testing getAll and getOne
> MoviesService.getAll과 MoviesService.getOne을 우선 테스트해볼 것이구요
> 
> Controller를 테스트하지 않고 Service를 테스트하는 이유는
> 
> 아마 비즈니스 로직만을 테스트해야 하는 경우이기 때문이라 말할 수 있을 것이구요
> 
> 비즈니스 로직을 테스트할 때 Controller를 테스트하면
> 라우터가 잘 받고 있는가?
> 잘 연결이 되어 있는가? 등등
> 주제에 맞지 않는 것까지 함께 테스트하게 되면서 복잡해질 예정이니 그럴 것이라 생각하기도 하구요
> 
> 그래서
> 
> ```typescript
> // /src/movies/movies.service.spec.ts
> import { Test, TestingModule } from "@nestjs/testing";
> import { MoviesService } from "./movies.service";
> 
> describe("MoviesService", () => {
>     let service:MoviesService;
> 
>     beforeEach(async () => {
>         const module:TestingModule = await Test.createTestingModule({
>             providers: [MoviesService]
>         }).compile();
> 
>         service = module.get<MoviesService>(MoviesService);
>     });
> 
>     it("should be defined", () => {
>         expect(service).toBeDefined();
>     });
> 
>     it("should be 4", () => {
>         expect(2+5).toEqual(4);
>     });
> });
> ```
> 
> should be 4는 지워버리다
> 
> 저게 필요한 건 아니잖아요???
> 
> 그리고 우리는 MoviesService를 테스트해야 하는데
> MoviesService는 매우 당연하지만 여러 메서드들로 이루어져 있기 때문에
> 텍스트를 새로 추가해야 할 필요가 있습니다
> 
> ```typescript
> describe("getAll()", () => {
> 
> });
> 
> describe("getOne()", () => {
> 
> });
> ```
> 
> 이제 무엇을 체크해야 하는지 생각해보다
> 
> > [!note]+ ## describe “getAll()”
> > getAll은 구현이
> > 
> > ```typescript
> > getAll():Movie[] {
> >     return this.movies;
> > }
> > ```
> > 
> > 이렇게 되어 있었음을 기억해야 합니다
> > 
> > 그리고 여기에서 this.movies는 다음과 같았구요
> > 
> > ```typescript
> > private movies:Movie[] = [];
> > ```
> > 
> > getAll은 그래서 우리가 예상하는 것이
> > 
> > > “Movies[]를 반환한다”
> > 
> > 인 것이네용
> > 
> > 빈 배열을 반환할 때가 있습니다만 어찌 되었든 배열이라는 사실에 대하여 변함이 없을 것이라 생각하구요
> > 
> > ```typescript
> > describe("getAll()", () => {
> >     it("should return an array", () => {
> >         const result = service.getAll();
> >         expect(result).toBeInstanceOf(Array);
> >     });
> > });
> > ```
> > 
> > 이걸로 getAll이 배열을 반환하는지 확인할 수 있구요
> > 
> > ![[image 109.png]]
> > 
> > 아주좋았어
> > 
> > 뭐
> > 
> > movies가 nullable한 뭔 이상한 말 같지도 않은 소리를 적어두었다고 하더라도 체크할 수 있게 된 것이구요
> 
> > [!note]+ ## describe “getOne()”
> > 근데 getAll은 사실 테스트할 부분이 많이 없구요
> > 
> > 그러한 것이
> > getAll은 그냥 반환하기만 합니다
> > 
> > 별 다를 것도 없음
> > ㅇㅇ
> > 
> > 하지만???
> > 
> > getOne은 id를 넣는다는 점에서 수많은 테스트가 추가로 더 생겼다고 할 수 있겠구요
> > 
> > ```typescript
> > describe("getOne()", () => {
> >     it("should return an Movie", () => {
> >         service.createMovie({
> >             title: "Test",
> >             year: 0,
> >             genres: []
> >         });
> > 
> >         const movie = service.getOne(1);
> >         expect(movie).toBeDefined();
> >         expect(movie.id).toEqual(1);
> >     });
> > });
> > ```
> > 
> > ![[image 110.png]]
> > 
> > 또 다른 테스트로는 다음과 같을 수 있는
> > 
> > ```typescript
> > describe("getOne()", () => {
> >     it("should return an Movie", () => {
> >         service.createMovie({
> >             title: "Test",
> >             year: 0,
> >             genres: []
> >         });
> > 
> >         const movie = service.getOne(1);
> >         expect(movie).toBeDefined();
> >         expect(movie.id).toEqual(1);
> >     });
> > 
> >     it("should throw 404 error", () => {
> >         const id = 111111111111111111;
> >         try {
> >             service.getOne(id);
> >         }
> >         catch(error:any) {
> >             expect(error).toBeInstanceOf(NotFoundException);
> >             expect(error.message).toEqual(`Movie with ID ${id}: not found`);
> >         }
> >     });
> > });
> > ```
> > 
> > 이러면 이제 getOne 메서드에 대하여
> > 
> > 1. 맞는 id로 GET 요청을 넣었을 때 올바르게 값을 리턴하는가
> > 2. 맞지 않는 이상한 id로 GET 요청을 넣었을 때 원하는 에러를 던지는가
> >     - 특히, 에러 메시지가 우리가 원하는 형태의 메시지가 맞는가
> > 
> > 에 대하여 테스트를 진행해주는
> > 
> > ![[image 111.png]]
> > 
> > 아주좋았어
> > 
> > 그래서 npm run test:cov를 실행했을 때
> > 
> > ![[image 112.png]]
> > 
> > 에 대하여
> > 
> > 기존 coverage:
> > 
> > ![[스크린샷_2026-06-14_140954.png]]
> > 
> > movies.service.ts의 Stmts, Branch 등 전체적으로 증가한 모습을 볼 수 있었구요
> > 
> > 세세하게 테스트해서 그런 것이라 말할 수 있겠네요
> > 
> > 아주 좋았어
> 

> [!note]+ # #3.3 Testing delete and create
> 이번엔 deleteMovie와 createMovie에 대하여 테스트 코드를 작성해볼 것인
> 
> ```typescript
> describe("deleteMovie()", () => {
> 
> });
> 
> describe("createMovie()", () => {
>     
> });
> ```
> 
> > [!note]+ ## describe “deleteMovie()”
> > 이에 대하여 테스트해야 할 항목은 총 2가지
> > 
> > 1. 성공적으로 삭제하였는가
> > 2. 없는 id를 입력하여 성공적으로 NotFoundException을 던지는가
> > 
> > 그러기 위해 createMovie를 우선적으로 호출하다
> > 구린
> > 
> > ```typescript
> > it("should delete an Movie", () => {
> >     service.createMovie({
> >         title: "Test",
> >         year: 2000,
> >         genres: []
> >     });
> > 
> >     const beforeDelete = service.getAll();
> >     service.deleteMovie(1);
> >     const afterDelete = service.getAll();
> > 
> >     expect(afterDelete.length).toBeLessThan(beforeDelete.length);
> > });
> > ```
> > 
> > ![[image 113.png]]
> > 
> > deleteMovie()가 생겨났구요
> > 
> > 아주좋았어
> > 
> > 에러 체크도 해볼 것이구요
> > 
> > ```typescript
> > it("should throw 404 error", () => {
> >     const id = 111111111111111111;
> >     try {
> >         service.deleteMovie(id);
> >         fail("fail: not throw error");
> >     }
> >     catch(error:any) {
> >         expect(error).toBeInstanceOf(NotFoundException);
> >         expect(error.message).toEqual(`Movie with ID ${id}: not found`);
> >     }
> > });
> > ```
> > 
> > 추가를 했구요
> > 
> > ![[image 114.png]]
> > 
> > 아주좋았어
> 
> > [!note]+ ## describe “createMovie()”
> > 이건 볼 것이 많이 없긴 해용
> > 
> > 1. 잘 생성되었는가
> > 
> > 이게 끝이라서
> > 
> > ```typescript
> > describe("createMovie()", () => {
> >   it("should create an Movie", () => {
> >       const beforeCreate = service.getAll();
> >       service.createMovie({
> >           title: "Test",
> >           year: 2000,
> >           genres: []
> >       });
> >       const afterCreate = service.getAll();
> > 
> >       expect(afterCreate.length).toBeGreaterThan(beforeCreate.length);
> >   });
> > });
> > ```
> > 
> > ![[image 115.png]]
> > 
> > 아주 좋았어

> [!note]+ # #3.4 Testing update
> 마지막 테스트는 patchMovie입니다
> 
> 할 것이 많이 없긴 함
> ㅇㅇ
> 
> 간단하게
> 
> 1. 잘 수정되었는가
> 2. id를 못 찾았을 때 에러를 던지는가
> 
> 이게 끝이라서
> 
> ![[image 116.png]]
> 
> 일단 이렇게 하고 npm run test:cov를 실행해보다
> 
> ![[image 117.png]]
> 
> movies.service.ts에 대하여 모든 퍼센트가 100%를 찍고 있구요
> 
> 아주좋았어
> 
> 아주완벽해
> 
> 크하하
> 
> 다음에는 e2e 테스팅을 배워보다