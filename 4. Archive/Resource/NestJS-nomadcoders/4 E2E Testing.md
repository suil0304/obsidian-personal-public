> [!note]+ # #4.0 Testing movies
> 코노 테스트 세카이에는
> 유닛 테스트을 좋아하는 사람도 있지만???
> e2e 테스트을 좋아하는 사람도 있다
> 
> 다시 정리하자면 e2e는 end-to-end의 줄임말이구요
> 
> 아무튼 e2e 테스트을 좋아하는 사람들은
> 아무래도 e2e 테스트가 좀 더 생각하기 쉬워서 그런 것 같구요
> 
> 유닛 테스트라고 하는 것은 아무래도 하나 하나 테스트해야 하잖아용
> 하지만 e2e는 테스트를 넣고 내려
> 
> 아무튼 비밀번호를 넣고 내려야 하는 함수가 있어야 한다 하자면
> 비밀번호를 암호화하고 내리는 함수
> 비밀번호를 저장하는 함수
> 또는 둘 다가 필요할 수 있는
> 
> 이럴 때는 유닛 테스트가 아무래도 힘들죠
> ㅇㅇ
> 
> 어떤 녀석은 1개만 테스트하고
> 또 다른 건 2개 다 동시에 테스트해야 하고
> 이게 뭐야
> 
> e2e 테스트는 이럴 때 혜성 같이 등장해 모두를 즐겁게 해주는
> 크하하
> 
> 특정한 한 부분에 대해 모든 부분을 테스트해야 할 때 즐거워지는 테스트 방법이라고 하구요
> 
> ```typescript
> // /test/app.e2e-spec.ts
> import { Test, TestingModule } from '@nestjs/testing';
> import { INestApplication } from '@nestjs/common';
> import request from 'supertest';
> import { App } from 'supertest/types';
> import { AppModule } from './../src/app.module';
> 
> describe('AppController (e2e)', () => {
>   let app: INestApplication<App>;
> 
>   beforeEach(async () => {
>     const moduleFixture: TestingModule = await Test.createTestingModule({
>       imports: [AppModule],
>     }).compile();
> 
>     app = moduleFixture.createNestApplication();
>     await app.init();
>   });
> 
>   it('/ (GET)', () => {
>     return request(app.getHttpServer())
>       .get('/')
>       .expect(200)
>       .expect('Hello World!');
>   });
> 
>   afterEach(async () => {
>     await app.close();
>   });
> });
> 
> ```
> 
> 이거 유닛 테스트 파일 작성할 때 많이 봤죠???
> 
> describe부터 해서 beforeEach, it
> 다 익숙하잖아용
> 
> ```typescript
> import request from 'supertest';
> ```
> 
> 근데 이것은 무엇인?
> 
> supertest에서 export default로 함수를 내보내고 있나 보구요
> 
> ```typescript
> it('/ (GET)', () => {
>   return request(app.getHttpServer())
>     .get('/')
>     .expect(200)
>     .expect('Hello World!');
> });
> ```
> 
> ![[image 124.png]]
> 
> ![[image 125.png]]
> 
> ![[image 126.png]]
> 
> ![[image 127.png]]
> 
> 어째서 이름까지 같으면서 매개변수 이름이 다른 건데
> 
> 오버로딩인가
> 
> 그러면됐음
> ㅇㅇ
> 
> 그래서 request라고 가지고 온 정체 불명의 함수에 app.getHttpServer를 호출하여 넣고 내려
> 
> 그런 다음 root에 GET 요청을 넣으면 아무튼 무언가를 반환할 텐데
> 
> ```typescript
> // /src/app.controller.ts
> import { Controller, Get } from '@nestjs/common';
> 
> @Controller()
> export class AppController {
>     @Get()
>     getHome():string {
>         return "Welcome to my Movie API";
>     }
> }
> ```
> 
> 일단 AppService로 분리하지 않은 건 둘째 쳐보기로 하고
> 
> GET 요청이 오면 “Welcome to my Movie API”라는 문자열을 반환한단 말이죠???
> 근데 “Hello World”라는 문자열이 돌아오기를 기대하고 있는 상태인 거구요
> 
> 어찌 되었든 GET 요청 자체는 성공될 테니 200 OK가 나와 200 상태 코드를 기대하는 것에 대하여 통과하겠지만
> body랍시고 온 것이 “Hello World”가 아닌 “Welcome to my Movie API”기 때문에 실패할 것이구요
> 
> ![[image 128.png]]
> 
> 당연하구요
> 
> 아무튼 이것을 통해 Controller(POST, GET, PUT, DELETE 등)와 Service(body와 서비스 로직 등), Pipe(지나가는 길에 잘못된 값을 넣었을 경우 등) 이 모든 것을 테스트할 수 있음을 알 수 있구요
> 
> ```typescript
> it('/ (GET)', () => {
>   return request(app.getHttpServer())
>     .get('/')
>     .expect(200)
>     .expect('Welcome to my Movie API');
> });
> ```
> 
> ![[image 129.png]]
> 
> 아주좋았어
> 
> 그래서 이제 무엇을 테스트할 수 있지???
> 
> movies.controller.ts로 가보다
> 
> ```typescript
> // /src/movies/movies.controller.ts
> import { Body, Controller, Delete, Get, Param, Patch, Post } from '@nestjs/common';
> import { MoviesService } from './movies.service';
> import { Movie } from './entities/Movie';
> import { CreateMovieDTO } from './dto/create-movie.dto';
> import { UpdateMovieDTO } from './dto/update-movie.dto';
> 
> @Controller('movies')
> export class MoviesController {
>     constructor(private readonly moviesService:MoviesService) {}
> 
>     @Get()
>     getAll():Movie[] {
>         return this.moviesService.getAll();
>     }
> 
>     @Get("/:id")
>     getOne(@Param("id") id:number):Movie {
>         console.log(typeof id);
>         return this.moviesService.getOne(id);
>     }
> 
>     @Post()
>     createMovie(@Body() movieData:CreateMovieDTO):number {
>         return this.moviesService.createMovie(movieData);
>     }
> 
>     @Delete("/:id")
>     deleteMovie(@Param("id") id:number) {
>         this.moviesService.deleteMovie(id);
>     }
> 
>     @Patch("/:id")
>     patchMovie(@Param("id") id:number, @Body() updateData:UpdateMovieDTO) {
>         return this.moviesService.patchMovie(id, updateData);
>     }
> }
> ```
> 
> getOne으로 예시를 들었을 때
> 
> 1. 정상적인 id로 GET 요청을 넣었을 때 200 상태 코드와 함께 POST로 넣었던 값이 나오는가
> 2. 정상적이지 못 한 id로 GET 요청을 넣었을 때 404 상태 코드와 함께 NotFoundException을 던지는가
> 
> 이렇게 테스트 가능함
> 
> 바로 한 번 작성해보다
> 
> 아맞다
> 
> 그래서 app.getHttpServer는 http://localhost:3000/를 계속 적지 않도록 하기 위해 가져오는 것이라고 하구요
> 
> ```typescript
> it("/movies (GET)", () => {
> return request(app.getHttpServer())
>   .get("/movies")
>   .expect(200)
>   .expect([]);
> });
> ```
> 
> ```typescript
> .expect([]);
> ```
> 
> 이게 되네
> 왜 되는 걸까용
> 
> NestJS에서는 string으로 온 값을 바로 변환해주나 봅니다
> 
> *crys* why…
> 
> 보통 개발자는 2개의 DB를 가지고 있는
> 
> 하나는 테스팅을 위해
> 또 하나는 실사용 DB
> 그러하구요
> 
> 우리는 가짜 테무산 배열 DB를 사용하기 때문에
> 하나 하나 해야 하구요
> 
> 근데 movies를 하는데
> /movies (GET)
> /movies (POST)
> /movies (PUT)
> …
> 
> 이렇게 묶어두지도 않고 나열할 것은 아니잖아요???
> 
> describe를 사용하다
> 
> ```typescript
> describe("/movies", () => {
>   it("GET", () => {
>     return request(app.getHttpServer())
>       .get("/movies")
>       .expect(200)
>       .expect([]);
>   });
> });
> ```
> 
> 아주좋았어
> 
> 다음은 POST 요청에 대하여 테스트를 진행해보다
> 
> ```typescript
> it("POST", () => {
>   const data:CreateMovieDTO = {
>       title: "Test",
>       year: 2000,
>       genres: []
>     };
> 
>   return request(app.getHttpServer())
>     .post("/movies")
>     .send(data)
>     .expect(201);
> });
> ```
> 
> 당연하지만 POST 요청에는 data를 같이 보내야 합니다
> 
> 아쉬운
> 
> 그래서 값을 넣었을 때 201 Created가 상태 코드로써 도착하는지를 체크해보면
> 
> ![[image 130.png]]
> 
> 아주 좋았어
> 
> 근데 /가 좀 많이 불편한
> 
> ```typescript
> describe("/", () => {
>   it("GET", () => {
>     return request(app.getHttpServer())
>       .get('/')
>       .expect(200)
>       .expect('Welcome to my Movie API');
>   });
> });
> ```
> 
> 미식이네용
> 
> 아주좋았어
> 
> 원한다면(거의 반필수로) DELETE 요청에 대하여 테스트도 가능한
> 
> 우리가 뭐
> deleteMovie에 return을 넣은 것 같지는 않으니 204 No Content를 기대해도 좋을 것 같구요
> 
> ```typescript
> it("DELETE", () => {
>   return request(app.getHttpServer())
>     .delete("/movies/1")
>     .expect(204);
> });
> ```
> 
> 근데 그 전에 값 자체를 넣은 게 없기 때문에
> 
> 404 Not Found를 기대하는 것이 더 좋을 것 같구요
> 
> ```typescript
> it("DELETE", () => {
>   return request(app.getHttpServer())
>     .delete("/movies/1")
>     .expect(404);
> });
> ```
> 
> ![[image 131.png]]
> 
> 아주좋았어
> 
> 근데 강의에서는 DELETE /movies를 테스트하여 Not Found가 오는지 확인하고 싶었다 하구요
> 이러언
> 
> ```typescript
> it("DELETE", () => {
>   return request(app.getHttpServer())
>     .delete("/movies")
>     .expect(404);
> });
> ```

> [!note]+ # #4.1 Testing GET movies id
> 그래서 개발하며 생길 법한 에러에 대하여 원인이 무엇인지 탐구해보다
> 
> ```typescript
> beforeEach(async () => {
>   const moduleFixture: TestingModule = await Test.createTestingModule({
>     imports: [AppModule],
>   }).compile();
> 
>   app = moduleFixture.createNestApplication();
>   await app.init();
> });
> ```
> 
> 당연한 소리지만
> 
> 매 테스트 전에 계속해서 앱을 새로 생성하고 있구요
> 
> 당연한 소리지만 이 Test.createTestingModule로 생성한 모듈로 만든 앱은 실제 서버 앱과는 다른 것임을 알아두어야 하구요
> 
> 브라우저에서도 확인 가능한 진짜 어플리케이션이 아니라는 소리였구요
> 
> 거의 다 만들고 테스트를 브라우저에서 실시간으로 하는 수일과 같은 빡빡이 청년과는 다르게 테스트 온리로 존재하는 것이 저것이구요
> 
> *crys* why…
> 
> 이번에는 경로 매개변수를 포함한 /movies/:id를 테스트해볼 예정인
> 
> 아주 다행스럽게도 Jest에는 todo라는 기능이 포함되어 있다고 하네용
> 
> ```typescript
> describe("/movies/:id", () => {
>   it.todo("GET");
>   it.todo("PATCH");
>   it.todo("DELETE");
> });
> ```
> 
> 그래서 todo가 뭔데
> 
> > [!note]+ ## todo
> > ![[image 132.png]]
> > 
> > 오
> > 
> > 음
> > 어
> > 아
> > 음
> > 음
> > 어
> > 음
> > 어
> > 어
> > 
> > 그렇군요
> > 
> > 말 그대로 todo였습니다
> > 
> > 해야 함
> > ㅇㅇ
> 
> 우리는 안타깝게도 앱을 매 테스트마다 생성하고 싶지 않다고 하네요
> 어째서
> 
> 그래서 모든 테스트 전에 앱을 생성하여 눌러 터트리다
> 
> 안 그래도 POST /movies에 대하여 지금 생성한 것을 전부 사용하고 싶음
> ㅇㅇ
> 
> 근데 이걸 그대로 냅둬버리면???
> 매 테스트마다 계속 새로운 앱을 생성할 것임이 분명하기 때문에
> 조치를 지금 당장 눌러 터트려버리다
> 
> ```typescript
> beforeAll(async () => {
>   const moduleFixture: TestingModule = await Test.createTestingModule({
>     imports: [AppModule],
>   }).compile();
> 
>   app = moduleFixture.createNestApplication();
>   await app.init();
> });
> ```
> 
> ```typescript
> afterAll(async () => {
>   await app.close();
> });
> ```
> 
> 이것으로 전체를 모두 수행하기 전 한 번
> 수행한 후 한 번
> 이렇게 실행되는
> 
> 이제 todo로 테스트해야 한다 했던 것을 빼고
> 다시 실제 테스트로 채워버리다
> 
> ```typescript
> it("GET 200", () => {
>   return request(app.getHttpServer())
>     .get("/movies/1")
>     .expect(200);
> });
> ```
> 
> 이전 테스트에서 생성했기 때문에 GET 요청을 넣었을 때 있을 것이니 200 OK가 나올 것이구요
> 
> 당장 실험해보다
> 
> ![[image 133.png]]
> 
> ???
> 
> 근데 MoviesController.getOne에서 string이라는 출력이 나오다???
> 
> ```typescript
> @Get("/:id")
> getOne(@Param("id") id:number):Movie {
>     console.log(typeof id);
>     return this.moviesService.getOne(id);
> }
> ```
> 
> ?
> 
> transform을 설정해서 number가 나와야 하는데
> 이게 무슨
> 
> 아
> 설마
> 
> 우리는 진짜 앱을 여는 것이 아닌
> 테스트 앱을 main.ts의 그 useGlobalPipes가 아닌 그냥 생성하고 있었던 것인
> 
> 이는 유닛 테스트도 마찬가지가 될 수 있는
> 
> ```typescript
> beforeAll(async () => {
>   const moduleFixture: TestingModule = await Test.createTestingModule({
>     imports: [AppModule],
>   }).compile();
> 
>   app = moduleFixture.createNestApplication();
>   app.useGlobalPipes(new ValidationPipe({
>       whitelist: true,
>       forbidNonWhitelisted: true,
>       transform: true
>   }));
>   await app.init();
> });
> ```
> 
> 이러면 아마도 될 것이구요
> 
> ![[image 134.png]]
> 
> number로 뜨면서 드디어 통과가 되네용
> 
> 마찬가지로 GET 404에 대하여 테스트를 진행해보면
> 
> ```typescript
> it("GET 404", () => {
>   return request(app.getHttpServer())
>     .get("/movies/9999")
>     .expect(404);
> });
> ```
> 
> ![[image 135.png]]
> 
> 잘 되고 있구요
> 아주좋았어

> [!note]+ # #4.2 Testing PATCH and DELETE movies id
> 이번에는 DELETE /movies/:id에 대하여 테스트를 진행해보다
> 
> 그 전에 먼저 PATCH를 테스트해보는 것이 좋을 것 같구요
> 
> DELETE를 먼저 테스트하여 서순이 DELETE → PATCH가 되어버리면 남은 영화가 없잖아용
> 
> ```typescript
> it("PATCH", () => {
>   const data:UpdateMovieDTO = {
>     title: "Updated Test"
>   };
> 
>   return request(app.getHttpServer())
>     .patch("/movies/1")
>     .send(data)
>     .expect(200);
> })
> 
> it("DELETE", () => {
>   return request(app.getHttpServer())
>     .delete("/movies/1")
>     .expect(200);
> });
> ```
> 
> 둘 다 기본적으로는 200 OK를 상태 코드로 반환하는 것 같네용
> 
> ![[image 136.png]]
> 
> 아주좋았어
> 
> 시간이 좀 남은 김에 잘못된 데이터를 가진 data를 넘겨 POST 요청을 날렸을 때
> 제대로 처리해주는지 확인해보다
> 
> ```typescript
> describe("/movies", () => {
>   it("GET", () => {
>     return request(app.getHttpServer())
>       .get("/movies")
>       .expect(200)
>       .expect([]);
>   });
> 
>   it("POST 201", () => {
>     const data:CreateMovieDTO = {
>         title: "Test",
>         year: 2000,
>         genres: []
>     };
> 
>     return request(app.getHttpServer())
>       .post("/movies")
>       .send(data)
>       .expect(201);
>   });
> 
>   it("POST 400", () => {
>     const data:object = {
>         title: "Wrong",
>         year: 2000,
>         genres: [],
>         other: "yeah"
>     };
> 
>     return request(app.getHttpServer())
>       .post("/movies")
>       .send(data)
>       .expect(400);
>   });
> 
>   it("DELETE", () => {
>     return request(app.getHttpServer())
>       .delete("/movies")
>       .expect(404);
>   });
> });
> ```
> 
> 여기에서 ValidationPipe에 넘긴 forbidNonWhitelisted가 true이기 때문에 잘못된 응답 → Bad Request가 되는 것이니
> 이것을 기억해두어야 하구요
> 
> ![[image 137.png]]
> 
> 아주좋았어
> 
> 그래서 각자의 .spec.ts에서는 유닛 테스트를 담당하고 있구요
> 이번에 작성한 .e2e-spec.ts는 e2e 테스트를 담당하고 있구요
> 
> 끝

> [!note]+ # #4.3 Finishing Up
> 아주 다 끝났구요
> 
> 이어서 할 생각이라면???
> 
> 여기를 참조하다: [https://nomadcoders.co/nuber-eats](https://nomadcoders.co/nuber-eats)