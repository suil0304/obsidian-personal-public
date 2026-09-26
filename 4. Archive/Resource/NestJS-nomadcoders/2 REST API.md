> [!note]+ # #2.0 Movies Controller
> 우리는 Re: 제로 어쩌구의 AppModule에 영화 REST API를 만들어 import 시킬 계획인
> 
> 어째서 REST API를 영화로 만드냐구요???
> 강의하시는 분이 영화를 좋아하신다고 하네요
> 이러언
> 
> 우리들의 뒤틀린 Re: 제로의 모듈: AppModule을 소환하여 소환하기에 소환하다
> 뭣
> 
> ```typescript
> import { Module } from '@nestjs/common';
> 
> @Module({
>     imports: [],
>     controllers: [],
>     providers: [],
> })
> export class AppModule {}
> ```
> 
> 텅 비었다
> 
> 근데 우리는 아까 전에 전역으로 Great한 CLI: @nestjs/cli를 전역-설치하였기 때문에
> 역시나 nest 딸-깍 코딩을 해볼까 하구요
> 
> 아무튼
> 
> Great한 CLI는 우리가 이용 가능한 무언가가 Great하게 많이 있어야 한다고 하구요
> 이러언
> 
> 그 중 하나는
> 
> ```bash
> nest generate
> ```
> 
> 라는 명령어구요
> 
> 매우 스바라시한 명령어라고 하네요
> CMD만으로도 NesJS의 거의 모든 것을 생성 가능하기 때문이라고 하구요
> 
> 당연하게도 우리는 Controller를 생성해야 하구요
> 
> ```bash
> nest generate controller movies /
> ```
> 
> 근데 이걸 극한으로 짧게 쓸 수 있었구요
> 
> 나중에 다 입력한다는 가정 하에
> 
> ```bash
> nest g co
> ```
> 
> 끝
> 
> 이러면 디렉터리 구조가 이렇게 됩니다
> 
> 디렉터리:
> 
> - /src
>     - /movies
>         - movies.controller.ts
>         - movies.controller.spec.ts
>     - app.module.ts
>     - main.ts
> 
> 이런 것도 딸깍으로 생성해주고
> 아주칭찬해
> 
> 심지어 자동으로 app.module.ts에 controllers: []를 controllers: [MoviesController]로 딸-깍 추가해줬음
> 아주훌륭해아주칭찬해아주마음에들어
> 
> spec이 붙어 있는 파일은 테스트 파일임을 저번에도 말했었는데
> 
> 일단 지우다
> 
> 이제 첫 번째 API 라우터를 만들어 볼게용???
> 
> ## Get 데코레이터(HTTP GET 요청)
> 
> ```typescript
> // /src/movies/movies.controller.ts
> import { Controller, Get } from '@nestjs/common';
> 
> @Controller('movies')
> export class MoviesController {
>     @Get()
>     getAll() { // any
>         return "This will return all movies";
>     }
> }
> ```
> 
> // any는 제가 달아둔 것이구요
> 
> Get 데코레이터에 아무 것도 넘기지 않았는데
> 
> 이러면 라우터(→ /movies/)를 가리키게 됩니다
> 
> ![[image 21.png]]
> 
> 아주좋았어
> 
> 근데 사실 강의에서는 127.0.0.1:3000을 가리키고 있어야 했던게 맞긴 함
> ㅇㅇ
> 
> ![[image 22.png]]
> 
> 예습은중요합니다
> 
> 이게 아니라
> 
> 우리가 만든 MoviesController는 매우 당연하게도 Controller 데코레이터에 “movies”를 넘겼기 때문이구요
> Controller 데코레이터는 URL의 엔트리 포인트
> 그러니까 진입점을 만들어 주는 고노야로 고노야로
> 컨트롤해준다 하네요
> 이러언
> 
> 그래서 이게 기본적으로 라우터다 이 말이구요
> 
> Get 데코레이터와 같은 것은
> Express 어플리케이션을 사용할 때의 그 라우터가 될 예정이라 하구요
> 
> 이제 다음을 추가하다:
> 
> ```typescript
> @Get("/:id")
> getOne() {
>     return "This will return one of movies";
> }
> ```
> 
> Express를 사용해본 경험이 있다면???
> 매우 익숙할 사용 방법이구요
> 가장 많이 쓰이는 이름은 경로 매개변수이라고 하구요
> NestJS에서 사용하는 이름이 따로 있을 수도 있으니 일단 넘겨보는게 좋을 것 같구요
> 이러언
> 
> 이제 Chrome을 변기에 넣고 내려
> 
> Insomnia를 키다
> 
> ![[image 23.png]]
> 
> /movies/1에 GET 요청을 넣다
> 
> 예상하는 결과가 나온
> 
> 아주좋았어
> 
> ## Param 데코레이터(req.params.id)
> 
> 근데 :id는 어떻게 가져옴???
> 
> 강의하는 분이 말씀하시기로는 우리 같은 개발자가 NestJS에서 이전에 시도해본 적이 없는 아주 낯선 것이라고 하네요
> 
> 이러언
> 
> 근데 일단 NestJS에서는 무언가가 필요하다???
> 요청해야 하는 거잖아요???
> 
> 거잖아요가 아니라 그렇죠
> 그러하다고 합니다
> 
> 이러언
> 
> 아니 그냥
> 무엇이 되었든
> 필요하면
> 요청을
> 해야
> 한다
> i understand
> 
> 예를 들어서 설명하자면
> getOne에서 요청하는 방법은 parameter를 요청하는 것이구요
> 
> parameter
> 네
> 매개변수였구요
> 이러언
> 
> 이걸 이제 id라는 argument에 넣고 내려
> 네
> 매개인자였구요
> 이러언
> 
> 이것을 이렇게 사용할 수 있는:
> 
> ```typescript
> @Get("/:id")
> getOne(@Param("id") id:string) {
>     return id;
> }
> ```
> 
> Param 데코레이터에 “id”를 넣었습니다
> id는 경로 매개변수 :id가 맞구요
> 그 가지고 온 경로 매개변수 :id를 id:string에 넣고 내려
> 
> 이제 다음과 같이 작성하다:
> 
> ```typescript
> @Get("/:id")
> getOne(@Param("id") id:string) {
>     return `This will return one of movies with the id: ${id}`;
> }
> ```
> 
> ![[image 24.png]]
> 
> 아주좋았어
> 
> 하지만
> NestJS에서는 Param 데코레이터를 사용하여 요청하지 않으면
> id:string이 :id 경로 매개변수를 원하는 거로구나 하고 바로 알 수 없음
> 다른 곳에서도 이는 똑같을 것이라 예상하구요
> 이러언
> 
> 아무튼
> 
> 그냥 id:string이라 적으면
> 이건 메서드의 매개변수일 뿐이지
> NestJS가 id라는 식별자를 읽고 경로 매개변수의 :id이겠거니 하지 않는다는 이야기가 되는 것이구요
> 
> 이러언
> 
> ## Post 데코레이터(HTTP POST)
> 
> Post 데코레이터는 매우 당연하게도 HTTP POST 요청이구요
> 
> REST API를 공부하다 보면 당연하게 배우는 사실이지만
> 
> POST 요청은 DB에 무언가를 생성하라 하는 것이구요
> *근데 뭐 대부분이 그러하다는 뜻이구요
> *이러언
> 
> ```typescript
> @Post()
> createMovie() {
>     return "This will create a movie";
> }
> ```
> 
> ![[image 25.png]]
> 
> ## Delete 데코레이터(HTTP DELETE)
> 
> Delete 데코레이터는 매우 당연하게도 HTTP DELETE 요청이구요
> 
> 마찬가지로 REST API를 공부하다 보면 당연하게 배우는 사실이지만
> 
> DELETE 요청은 DB에 무언가를 삭제하라는 것이구요
> *근데 뭐 대부분이 그러하다는 뜻이구요
> *이러언
> 
> ```typescript
> @Delete("/:id")
> deleteMovie(@Param("id") id:string) {
>     return `This will delete a movie with the id: ${id}`;
> }
> ```
> 
> /:id 없이 그냥 넣어 버리면
> 
> ```sql
> DROP TABLE movies;
> ```
> 
> 이것과 다를 바가 없는 핵이기 때문에
> id는 필수이구요
> 
> ![[image 26.png]]
> 
> ## Put 데코레이터(HTTP PUT)
> 
> Put 데코레이터는 매우 당연하게도 HTTP PUT 요청이구요
> 
> 마찬가지로 REST API를 공부하다 보면 당연하게 배우는 사실이지만
> 
> PUT 요청은 DB에 무언가를 수정(업데이트)하라는 것이구요
> *근데 뭐 대부분이 그러하다는 뜻이구요
> *이러언
> 
> 근데 사람들은 PUT 요청을 필요 없다고 이야기하기도 함
> 
> PUT 요청은 모든 리소스를 업데이트하기 때문이라고 하네요
> *보통의 경우 그렇게 구현됨*
> 
> \*crys\* why…
> 
> ## Patch 데코레이터(HTTP PATCH)
> 
> 그러한 여러분들을 위해 준비했습니다
> 
> Patch 데코레이터는 매우 당연하게도 HTTP PATCH 요청이구요
> 
> 저는 근데 야매로 제대로 배우지도 않아서 PATCH 요청은 처음 보구요
> 이게뭐야
> 
> PATCH 요청은 DB에 무언가를 수정하긴 하는데 리소스의 일부분만 업데이트하구요
> 이러언
> 
> 그래서 여기에서는 전체 영화 업데이트: PUT
> 영화의 일부분을 업데이트할 때는: PATCH
> 
> 이렇게 할 것이구요
> 
> ```sql
> @Patch("/:id")
> patchMovie(@Param("id") id:string) {
>     return `This will patch a movie with the id: ${id}`;
> }
> ```
> 

> [!note]+ # #2.1 More Routes
> 데코레이터를 조금 더 알아보다
> 
> 기분이가좋아지는
> 
> ## Body 데코레이터
> 
> 왔구나… 나의 보디…
> 
> res.body구요
> 
> 뭐 그러하구요
> 
> ```sql
> @Post()
> createMovie(@Body() movieData:object) {
>     console.log(movieData);
>     return "This will create a movie";
> }
> ```
> 
> 이러면 이제 movieData:object에 body가 담기게 되는 것이구요
> 
> ```typescript
> // interface MovieData {
> //     "name":string;
> //     "director":string;
> // }
> 
> @Post()
> createMovie(@Body() movieData:/* MovieData */object) {
>     console.log(movieData);
>     return "This will create a movie";
> }
> ```
> 
> 이러면 이제
> 
> ![[image 27.png]]
> 
> 아주좋았어
> 
> 이것을 patchMovie에도 적용시키다
> 
> ```typescript
> @Patch("/:id")
> patchMovie(@Param("id") id:string, @Body() movieData:MovieData) {
>     return {
>         updatedMovieID: id,
>         ...movieData
>     };
> }
> ```
> 
> ![[image 28.png]]
> 
> 근데 여기에서???
> 
> object로 리턴했는데 JSON으로 값을 받았음
> 
> 오
> 
> Express는 body를 JSON로 보내기 위해서 설정을 좀 만지거나 했었어야 했음
> 
> 근데???
> 
> 딸ㅋㅋ깍ㅋㅋ
> 
> 근데 사실 /는 없어도 됨
> ㅇㅇ
> 
> 하지만 명시적으로 하기 위해 저는 /를 붙이다
> 
> ## Query 데코레이터
> 
> ```typescript
> @Get("/search")
> searchMovie() {
>     return "We are searching for a movie with a title";
> }
> ```
> 
> 오
> 
> 근데 위에 이미 @Get(”/:id”)를 붙여둔 메서드가 있었구요
> 
> ![[image 29.png]]
> 
> 씨
> 
> 이거는 :id와 같은 경로 매개변수보다 위에 둬야 하는 것이었구요
> 
> ```typescript
> @Get()
> getAll() { // any
>     return "This will return all movies";
> }
> 
> @Get("/search")
> searchMovie() {
>     return "We are searching for a movie with a title: ";
> }
> 
> @Get("/:id")
> getOne(@Param("id") id:string) {
>     return `This will return one of movies with the id: ${id}`;
> }
> ```
> 
> 이렇게 뒀어야 했구요
> 
> Express나 NestJS나 어쨌든 이런 문제가 생길 수 있어서
> 
> 서순 이슈를 신경 써야 한다고 하구요
> 
> 이러언
> 
> 아무튼 쿼리 매개인자를 받아서 메서드 매개변수로 받고 싶구요
> 
> 그럴 때 사용하다
> Query 데코레이터를
> 
> ```typescript
> @Get("/search")
> searchMovie(@Query("year") year:string) {
>     return `We are searching for a movie made after: ${year}`;
> }
> ```
> 
> 이제 URL에 year 쿼리 매개인자를 집어 넣으면???
> 
> 127.0.0.1:3000/movies/search?year=2000
> 
> ![[image 30.png]]
> 
> 아주좋았어
> 
> 이것은 이제 req.query를 받아오는 것과 같구요

> [!note]+ # #2.2 Movies Service part One
> Single-Responsibility Priniple라는 것이 있습니다
> 네
> 단일책임 원칙이죠???
> 
> 언제나 중요한 원칙이기에 그냥 계속해서 알고 계셔야 하구요
> 
> 아무튼
> 
> 이번에는 만들다 Service
> Service는 movies의 비즈니스 로직을 담당할 예정이구요
> 
> 다음을 CMD에 입력하다:
> 
> ```bash
> nest generate service movies /
> ```
> 
> 이를 매우 간단히 줄이면 다음과 같은
> 
> ```bash
> nest g s
> ```
> 
> 이제 입력하면 디렉터리 구조가 다음과 같아지는
> 
> 디렉터리:
> 
> - /src
>     - /movies
>         - movies.controller.ts
>         - movies.service.ts
>         - movies.service.spec.ts
>     - app.module.ts
>     - main.ts
> 
> movies.service.spec.ts는 마찬가지로 서비스 테스트 파일이기 때문에 지금은 지워주겠습니다
> 이러언
> 
> ```typescript
> // /src/movies/movies.service.ts
> import { Injectable } from '@nestjs/common';
> 
> @Injectable()
> export class MoviesService {}
> ```
> 
> ```typescript
> // /src/app.module.ts
> import { Module } from '@nestjs/common';
> import { MoviesController } from './movies/movies.controller';
> import { MoviesService } from './movies/movies.service';
> 
> @Module({
>     imports: [],
>     controllers: [MoviesController],
>     providers: [MoviesService],
> })
> export class AppModule {}
> ```
> 
> 아주좋았어
> 
> 우리는 movies.service.ts에 데이터베이스를 추가할 예정인
> 그렇다고 진짜 데이터베이스를 추가할 것은 아니구요
> 
> ```typescript
> private movies:Array<> = [];
> ```
> 
> 오 근데 그러면
> 
> ![[image 31.png]]
> 
> 당연한 소리구요
> 
> 새로운 클래스를 선언하다
> 
> 그러기 위해 새로운 폴더와 파일을 만들다
> 
> /src/movies/entities/Movie.ts
> 
> 오
> 근데
> 
> 기존 컨벤션 안 따르는 것 같구요
> 기존 건벤션이라 하면
> {이름}.{용도}.ts이 되겠구요
> 
> 변경하다:
> 
> /src/movies/entities/movie.entity.ts
> 
> ```typescript
> // /src/movies/entities/movie.entity.ts
> export class Movie {
>     id!:number;
>     title!:string;
>     year!:number;
>     genres!:string[];
> }
> ```
> 
> ```typescript
> private movies:Movie[] = [];
> ```
> 
> 이제 원래 movies.controller.ts에 정의해두었던 내용을 movies.service.ts에 이사시키다
> 
> ```typescript
> // /src/movies/movies.service.ts
> import { Injectable } from '@nestjs/common';
> import { Movie } from './entities/Movie';
> 
> @Injectable()
> export class MoviesService {
>     private movies:Movie[] = [];
> 
>     getAll():Movie[] {
>         return this.movies;
>     }
> 
>     getOne(id:string):Movie {
>         return this.movies.find((movie) => {
>             return movie.id === Number.parseInt(id);
>         });
>     }
> }
> ```
> 
> 근데 MoviesService를 만들어서 뭐 함??
> 
> MoviesController를 MoviesService에 연결시켜야 하는
> 
> ```typescript
> constructor(private readonly moviesService:MoviesService) {}
> ```
> 
> 생성자에서 받다
> 
> ```typescript
> @Get()
> getAll():Movie[] {
>     return this.moviesService.getAll();
> }
> 
> @Get("/:id")
> getOne(@Param("id") id:string):Movie {
>     return this.moviesService.getOne(id);
> }
> ```
> 
> 아주좋았어
> 
> 이어서 작업하다
> 
> deleteMovie:
> 
> ```typescript
> // /src/movies/movies.service.ts
> deleteMovie(id:string):boolean {
>     this.movies.filter((movie) => {
>         return movie.id !== Number.parseInt(id);
>     });
>     return true;
> }
> ```
> 
> ```typescript
> // /src/movies/movies.controller.ts
> @Delete("/:id")
> deleteMovie(@Param("id") id:string):boolean {
>     return this.moviesService.deleteMovie(id);
> }
> ```
> 
> createMovie:
> 
> ```typescript
> // /src/movies/movies.service.ts
> createMovie(movieData:any):number {
>     return this.movies.push({
>         id: this.movies.length + 1,
>         ...movieData
>     });
> }
> ```
> 
> ```typescript
> // /src/movies/movies.controller.ts
> @Post()
> createMovie(@Body() movieData:any):number {
>     return this.moviesService.createMovie(movieData);
> }
> ```
> 
> POST 요청을 7번 넣었을 때 GET으로 전체 조회를 해보면:
> 
> ![[image 32.png]]
> 
> 아주좋았어

> [!note]+ # #2.3 Movies Service part Two
> 매우 당연한 소리:
> 
> MoviesService에 만들어둔
> 
> ```typescript
> private movies:Movie[] = [];
> ```
> 
> 이것은 메모리 위에만 올려둔 것이기 때문에
> 서버를 닫는 순간 DROP TABLE movies CASCADE;
> 
> 몇 번이고 계속 강조하다
> NestJS의 멋진 점은 우리를 위해 만들어둔 것이 매우 많다는 사실인
> 
> 뭐 그래서
> 
> Express였으면 한 땀 한 땀 상태 코드 직접 정의해야 했던 기초 행동들은
> 
> ![[image 33.png]]
> 
> 딸ㅋㅋ깍ㅋㅋ
> 
> 다 해줬잖아
> 
> 이것 말고도 이미 준비된 것들이 더 있구요
> 
> 그래서 GET 요청과 매핑된 getOne 메서드의 비즈니스 로직 부분을 조금 더 손 보고 싶구요
> 
> 뭐
> 
> 예를 들어서
> 
> 누가 GET /movies/1111111111111 이따위로 날리면 못 찾을 때 못 찾는다고 Error를 날려야 할 것 아니겠습니까
> 근데 지금은 undefined를 급한 대로 날리고 있단 말이죠
> 어차피 TS는 컴파일될 때는 JS라 런타임 동적인 것이 똑같아서
> 암만 함수에 타입을 붙여 봤자 그러할 뿐이구요
> 씨
> 
> 거기에 다음과 같은 Exception을 던져주면???
> NestJS가 알아서 처리해줄 것입니다
> 다 해줬잖아
> 크하하
> 
> ```typescript
> throw new NotFoundException();
> ```
> 
> 이는 이렇게 구현되어 있구요
> 
> ```typescript
> // not-found.exception.d.ts
> import { HttpException, HttpExceptionOptions } from './http.exception';
> /**
>  * Defines an HTTP exception for *Not Found* type errors.
>  *
>  * @see [Built-in HTTP exceptions](https://docs.nestjs.com/exception-filters#built-in-http-exceptions)
>  *
>  * @publicApi
>  */
> export declare class NotFoundException extends HttpException {
>     /**
>      * Instantiate a `NotFoundException` Exception.
>      *
>      * @example
>      * `throw new NotFoundException()`
>      *
>      * @usageNotes
>      * The HTTP response status code will be 404.
>      * - The `objectOrError` argument defines the JSON response body or the message string.
>      * - The `descriptionOrOptions` argument contains either a short description of the HTTP error or an options object used to provide an underlying error cause.
>      *
>      * By default, the JSON response body contains two properties:
>      * - `statusCode`: this will be the value 404.
>      * - `message`: the string `'Not Found'` by default; override this by supplying
>      * a string in the `objectOrError` parameter.
>      *
>      * If the parameter `objectOrError` is a string, the response body will contain an
>      * additional property, `error`, with a short description of the HTTP error. To override the
>      * entire JSON response body, pass an object instead. Nest will serialize the object
>      * and return it as the JSON response body.
>      *
>      * @param objectOrError string or object describing the error condition.
>      * @param descriptionOrOptions either a short description of the HTTP error or an options object used to provide an underlying error cause
>      */
>     constructor(objectOrError?: any, descriptionOrOptions?: string | HttpExceptionOptions);
> }
> 
> ```
> 
> 근데 보면 HttpException이 기본형인 것 같네용
> 
> ```typescript
> // http.exception.d.ts
> import { HttpExceptionBody, HttpExceptionBodyMessage } from '../interfaces/http/http-exception-body.interface';
> import { IntrinsicException } from './intrinsic.exception';
> export interface HttpExceptionOptions {
>     /** original cause of the error */
>     cause?: unknown;
>     description?: string;
> }
> export interface DescriptionAndOptions {
>     description?: string;
>     httpExceptionOptions?: HttpExceptionOptions;
> }
> /**
>  * Defines the base Nest HTTP exception, which is handled by the default
>  * Exceptions Handler.
>  *
>  * @see [Built-in HTTP exceptions](https://docs.nestjs.com/exception-filters#built-in-http-exceptions)
>  *
>  * @publicApi
>  */
> export declare class HttpException extends IntrinsicException {
>     private readonly response;
>     private readonly status;
>     private readonly options?;
>     /**
>      * Exception cause. Indicates the specific original cause of the error.
>      * It is used when catching and re-throwing an error with a more-specific or useful error message in order to still have access to the original error.
>      */
>     cause: unknown;
>     /**
>      * Instantiate a plain HTTP Exception.
>      *
>      * @example
>      * throw new HttpException('message', HttpStatus.BAD_REQUEST)
>      * throw new HttpException('custom message', HttpStatus.BAD_REQUEST, {
>      *  cause: new Error('Cause Error'),
>      * })
>      *
>      *
>      * @usageNotes
>      * The constructor arguments define the response and the HTTP response status code.
>      * - The `response` argument (required) defines the JSON response body. alternatively, it can also be
>      *  an error object that is used to define an error [cause](https://nodejs.org/en/blog/release/v16.9.0/#error-cause).
>      * - The `status` argument (required) defines the HTTP Status Code.
>      * - The `options` argument (optional) defines additional error options. Currently, it supports the `cause` attribute,
>      *  and can be used as an alternative way to specify the error cause: `const error = new HttpException('description', 400, { cause: new Error() });`
>      *
>      * By default, the JSON response body contains two properties:
>      * - `statusCode`: the Http Status Code.
>      * - `message`: a short description of the HTTP error by default; override this
>      * by supplying a string in the `response` parameter.
>      *
>      * To override the entire JSON response body, pass an object to the `createBody`
>      * method. Nest will serialize the object and return it as the JSON response body.
>      *
>      * The `status` argument is required, and should be a valid HTTP status code.
>      * Best practice is to use the `HttpStatus` enum imported from `nestjs/common`.
>      *
>      * @param response string, object describing the error condition or the error cause.
>      * @param status HTTP response status code.
>      * @param options An object used to add an error cause.
>      */
>     constructor(response: string | Record<string, any>, status: number, options?: HttpExceptionOptions | undefined);
>     /**
>      * Configures error chaining support
>      *
>      * @see https://nodejs.org/en/blog/release/v16.9.0/#error-cause
>      * @see https://github.com/microsoft/TypeScript/issues/45167
>      */
>     initCause(): void;
>     initMessage(): void;
>     initName(): void;
>     getResponse(): string | object;
>     getStatus(): number;
>     static createBody(nil: null | '', message: HttpExceptionBodyMessage, statusCode: number): HttpExceptionBody;
>     static createBody(message: HttpExceptionBodyMessage, error: string, statusCode: number): HttpExceptionBody;
>     static createBody<Body extends Record<string, unknown>>(custom: Body): Body;
>     static getDescriptionFrom(descriptionOrOptions: string | HttpExceptionOptions): string;
>     static getHttpExceptionOptionsFrom(descriptionOrOptions: string | HttpExceptionOptions): HttpExceptionOptions;
>     /**
>      * Utility method used to extract the error description and httpExceptionOptions from the given argument.
>      * This is used by inheriting classes to correctly parse both options.
>      * @returns the error description and the httpExceptionOptions as an object.
>      */
>     static extractDescriptionAndOptionsFrom(descriptionOrOptions: string | HttpExceptionOptions): DescriptionAndOptions;
> }
> 
> ```
> 
> 이제 적용시켜보다
> 
> ```typescript
> getOne(id:string):Movie {
>     const movie:Movie | undefined = this.movies.find((movie) => {
>         return movie.id === Number.parseInt(id);
>     });
> 
>     if(!movie) {
>         throw new NotFoundException(`Movie with ID ${id}: not found`);
>     }
> 
>     return movie;
> }
> ```
> 
> 결과:
> 
> ![[image 34.png]]
> 
> Body에 담긴 JSON은 무시하시구요
> 
> POST 요청 넣다가 귀찮아서 제거 안 한 것이니 그러하구요
> 
> 이러언
> 
> 아무튼
> 
> 아주좋았어
> 
> 이제 DELETE 요청과 매핑된 deleteMovie 메서드의 비즈니스 로직을 개선해보다
> 
> 생각해보다
> 
> 이미 있는지 없는지 검증하는 로직을 getOne의 비즈니스 로직에서 만들어둔
> 
> ```typescript
> deleteMovie(id:string) {
>     this.getOne(id);
>     this.movies = this.movies.filter((movie) => {
>         return movie.id !== Number.parseInt(id);
>     });
> }
> ```
> 
> 아주좋았어
> 
> 결과:
> 
> ![[image 35.png]]
> 
> 다 해줬잖아
> 
> 근데 생각해보니 PATCH 요청과 매핑된 patchMovie 메서드의 비즈니스 로직을 분리해두지 않았구요
> 
> 이참에 만들면서 크하하하다
> 
> ```typescript
> // /src/movies/movies.service.ts
> patchMovie(id:string, updateData:object) {
>     const movie = this.getOne(id);
>     this.deleteMovie(id);
>     this.movies.push({ ...movie, ...updateData });
> }
> ```
> 
> ```typescript
> // /src/movies/movies.controller.ts
> @Patch("/:id")
> patchMovie(@Param("id") id:string, @Body() updateData:object) {
>     return this.moviesService.patchMovie(id, updateData);
> }
> ```
> 
> 아주좋았어
> 
> 근데 좀 많이 구린 듯
> ㅇㅇ
> 
> 가짜로 배열 기반 DB를 구현시킨 탓이 크긴 함
> ㅇㅇ
> 
> 테스트:
> 
> ![[image 36.png]]
> 
> 이제 /movies/2에 PATCH 요청을 넣어보다
> 
> ![[image 37.png]]
> 
> 이제 GET 요청을 넣어 확인해보다
> 
> ![[image 38.png]]
> 
> 아주좋았어
> 
> 근데
> 
> 지금 우리
> 
> updateData를 제대로 검증하고 있지는 않긴 함
> 
> 이게뭐야
> 
> 어쨌든 그 말은
> 
> ![[image 39.png]]
> 
> 이렇게 이상한 값을 추가로 달아 PATCH 요청을 날렸을 때
> 
> ![[image 40.png]]
> 
> 이를 전혀 막아주지 못 한다는 소리이구요
> 
> 이에 대한 것들은 다음에 보도록 하구요

> [!note]+ # #2.4 DTOs and Validation part One
> 이 엿 같은 JS 런타임 동적 세계에서도 타입을 붙여야만 하기 때문에
> 
> 우리는 DTO라는 것을 만들어야 할 필요가 있구요
> 
> DTO라고 하는 것은 Data Transfer Object의 줄임말이구요
> 한국어로 대충 번역해보자면 데이터 전송 객체라고 하네요
> 이러언
> 
> 그래서 /movies 안에 /dto라는 폴더를 만들 것이구요
> 
> 거기 안에다가 create-movie.dto.ts라 이름 지은 파일을 생성해줄 것이구요
> 크하하
> 
> 그리고 이것은 기본적으로 클래스가 될 것이구요
> 
> 클래스 안에는 사람들이 보내야만 하는 것들을 interface마냥 명시해두다
> 어째서냐 하면 interface는 순 타입이기 때문에 JS로 컴파일되면 구라제거기마냥 싹 다 삭제시켜버리는
> 씨
> 
> 적어야 하는 것을 movie.entity.ts에 들어가 확인해보다
> 
> ```typescript
> // /src/movies/entities/movie.entity.ts
> export class Movie {
>     id!:number;
>     title!:string;
>     year!:number;
>     genres!:string[];
> }
> ```
> 
> 하지만 그렇다고 해서 진짜로 body에 id까지 포함시켜 보내야 하는 것은 아니구요
> 
> 이미 경로 매개변수에 id를 받으려 시도하고 있기 때문에
> 과할 뿐더러 구현에 따라 충돌이 불가피한 구조가 되기 때문일 것 같네용
> 
> ```typescript
> // /src/movies/dto/create-movie.dto.ts
> export class CreateMovieDTO {
>     readonly title!:string;
>     readonly year!:number;
>     readonly genres!:string[];
> }
> ```
> 
> 이제 MoviesController와 MoviesService에 가서
> createMovie의 body를 받는 매개변수에 타입을 달아주러 가보다
> 
> ```typescript
> // /src/movies/movies.controller.ts
> @Post()
> createMovie(@Body() movieData:CreateMovieDTO):number {
>     return this.moviesService.createMovie(movieData);
> }
> ```
> 
> ```typescript
> // /src/movies/movies.service.ts
> createMovie(movieData:CreateMovieDTO):number {
>     return this.movies.push({
>         id: this.movies.length + 1,
>         ...movieData
>     });
> }
> ```
> 
> 근데 사실 이래봤자 JS로 컴파일되면 하등 쓸모가 없을 것이구요
> 
> 눈으로 보이는 타입이 죄다 사라져서 동적이 되는데
> 
> 그러면 동적으로 JS에서도 확인할 수 있도록 Symbol을 추가하고 그렇게 복잡한 방식으로 해아만 하다???
> 
> 이제 드디어 main.ts를 건드려보는 날이 오다
> 
> main.ts에 pipe를 만들러 가는 것인
> 
> pipe가 무엇이냐고 하면 파이프입니다
> 코드가 지나가는 파이프
> ㅇㅇ
> 
> 일반적으로 pipe는 미들웨어라 생각할 수 있다고 하구요
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> import { ValidationPipe } from '@nestjs/common';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     app.useGlobalPipes(new ValidationPipe());
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> 이러면 이제 유효성 검사 pipe를 글로벌 pipe로 사용하게 되는 것인
> 
> 근데
> 
> ![[image 41.png]]
> 
> 네?
> 
> 무언가를 설치했어야 했나 봅니다
> 이게뭐야
> 
> 우리는 다음의 두 package를 설치할 예정인
> 
> 하나는 저기에 나와 있듯이
> class-validator
> 
> 또 하나는 class-transformer
> 
> 아래에 다음 커맨드를 입력하다
> 
> ```bash
> npm install class-validator
> npm install class-transformer
> ```
> 
> 그리고 아까 전에 정의해두었던 CreateMovieDTO에 새로운 데코레이터
> 네
> 뭐
> 새롭게 설치한 데코레이터죠???
> 를 달아주러 가보다
> 
> ```typescript
> // /src/movies/dto/create-movie.dto.ts
> import { IsNumber, IsString } from "class-validator";
> 
> export class CreateMovieDTO {
>     @IsString()
>     readonly title!:string;
>     @IsNumber()
>     readonly year!:number;
> 
>     readonly genres!:string[]; // ?
> }
> ```
> 
> 그러면 근데 readonly genres!:string[];은 어떻게 유효성 검사를 하다???
> 
> Is~~ 안에 들어가서 보면
> 
> ```typescript
> // IsString.d.ts
> import { ValidationOptions } from '../ValidationOptions';
> export declare const IS_STRING = "isString";
> /**
>  * Checks if a given value is a real string.
>  */
> export declare function isString(value: unknown): value is string;
> /**
>  * Checks if a given value is a real string.
>  */
> export declare function IsString(validationOptions?: ValidationOptions): PropertyDecorator;
> ```
> 
> 이는 이렇게 되어 있고
> 
> ValidationOptions 안에 들어가면
> 
> ```typescript
> // ValidationOptions.d.ts
> import { ValidationArguments } from '../validation/ValidationArguments';
> /**
>  * Options used to pass to validation decorators.
>  */
> export interface ValidationOptions {
>     /**
>      * Specifies if validated value is an array and each of its items must be validated.
>      */
>     each?: boolean;
>     /**
>      * Error message to be used on validation fail.
>      * Message can be either string or a function that returns a string.
>      */
>     message?: string | ((validationArguments: ValidationArguments) => string);
>     /**
>      * Validation groups used for this validation.
>      */
>     groups?: string[];
>     /**
>      * Indicates if validation must be performed always, no matter of validation groups used.
>      */
>     always?: boolean;
>     context?: any;
>     /**
>      * validation will be performed while the result is true
>      */
>     validateIf?: (object: any, value: any) => boolean;
> }
> export declare function isValidationOptions(val: any): val is ValidationOptions;
> ```
> 
> 이렇게 되어 있음
> 
> ```typescript
> /**
>  * Specifies if validated value is an array and each of its items must be validated.
>  */
> each?: boolean;
> ```
> 
> 호오
> 
> 약간 forEach마냥 전체 검사를 수행하게 하는 옵션인 듯
> ㅇㅇ
> 
> 그래서 다음과 같이 달아 완성시키다
> 
> ```typescript
> // /src/movies/dto/create-movie.dto.ts
> import { IsNumber, IsString } from "class-validator";
> 
> export class CreateMovieDTO {
>     @IsString()
>     readonly title!:string;
>     @IsNumber()
>     readonly year!:number;
> 		@IsString({ each: true })
>     readonly genres!:string[];
> }
> ```
> 
> 됐다
> 
> 결과:
> 
> ![[image 42.png]]
> 
> 이제는 적어도 이상한 값만 보내는 경우에 대하여 견제할 수 있게 된
> 
> 끼얏호우
> 
> 또한 이름이 같아도 값이 이상한 경우 또한 견제 가능해지는
> 
> ![[image 43.png]]
> 
> 아주좋았어
> 
> 근데 쟤네 다 맞추고 추가 값을 넣을 수 있을 것 같은데용
> 
> ![[image 44.png]]
> 
> 아잇
> 
> 런타임 동적의 한계를 넘을 듯 말듯 하는게 좀 많이 빡치네용
> 씨
> 
> 그래서 다시 main.ts에 심어둔 ValidationPipe를 유심히 관찰해보다
> 
> ```typescript
> // validation.pipe.d.ts
> import { ClassTransformOptions } from '../interfaces/external/class-transform-options.interface';
> import { TransformerPackage } from '../interfaces/external/transformer-package.interface';
> import { ValidationError } from '../interfaces/external/validation-error.interface';
> import { ValidatorOptions } from '../interfaces/external/validator-options.interface';
> import { ValidatorPackage } from '../interfaces/external/validator-package.interface';
> import { ArgumentMetadata, PipeTransform } from '../interfaces/features/pipe-transform.interface';
> import { Type } from '../interfaces/type.interface';
> import { ErrorHttpStatusCode } from '../utils/http-error-by-code.util';
> /**
>  * @publicApi
>  */
> export interface ValidationPipeOptions extends ValidatorOptions {
>     transform?: boolean;
>     disableErrorMessages?: boolean;
>     transformOptions?: ClassTransformOptions;
>     errorHttpStatusCode?: ErrorHttpStatusCode;
>     exceptionFactory?: (errors: ValidationError[]) => any;
>     validateCustomDecorators?: boolean;
>     expectedType?: Type<any>;
>     validatorPackage?: ValidatorPackage;
>     transformerPackage?: TransformerPackage;
> }
> /**
>  * @see [Validation](https://docs.nestjs.com/techniques/validation)
>  *
>  * @publicApi
>  */
> export declare class ValidationPipe implements PipeTransform<any> {
>     protected isTransformEnabled: boolean;
>     protected isDetailedOutputDisabled?: boolean;
>     protected validatorOptions: ValidatorOptions;
>     protected transformOptions: ClassTransformOptions | undefined;
>     protected errorHttpStatusCode: ErrorHttpStatusCode;
>     protected expectedType: Type<any> | undefined;
>     protected exceptionFactory: (errors: ValidationError[]) => any;
>     protected validateCustomDecorators: boolean;
>     constructor(options?: ValidationPipeOptions);
>     protected loadValidator(validatorPackage?: ValidatorPackage): ValidatorPackage;
>     protected loadTransformer(transformerPackage?: TransformerPackage): TransformerPackage;
>     transform(value: any, metadata: ArgumentMetadata): Promise<any>;
>     createExceptionFactory(): (validationErrors?: ValidationError[]) => unknown;
>     protected toValidate(metadata: ArgumentMetadata): boolean;
>     protected transformPrimitive(value: any, metadata: ArgumentMetadata): any;
>     protected toEmptyIfNil<T = any, R = T>(value: T, metatype: Type<unknown> | object): R | object | string;
>     protected stripProtoKeys(value: any): void;
>     protected isPrimitive(value: unknown): boolean;
>     protected validate(object: object, validatorOptions?: ValidatorOptions): Promise<ValidationError[]> | ValidationError[];
>     protected flattenValidationErrors(validationErrors: ValidationError[]): string[];
>     protected mapChildrenToValidationErrors(error: ValidationError, parentPath?: string): ValidationError[];
>     protected prependConstraintsWithParentProp(parentPath: string, error: ValidationError): ValidationError;
> }
> ```
> 
> ```typescript
> // validator-options.interface.d.ts
> /**
>  * Options passed to validator during validation.
>  * @see https://github.com/typestack/class-validator
>  *
>  * class-validator@0.13.0
>  *
>  * @publicApi
>  */
> export interface ValidatorOptions {
>     /**
>      * If set to true then class-validator will print extra warning messages to the console when something is not right.
>      */
>     enableDebugMessages?: boolean;
>     /**
>      * If set to true then validator will skip validation of all properties that are undefined in the validating object.
>      */
>     skipUndefinedProperties?: boolean;
>     /**
>      * If set to true then validator will skip validation of all properties that are null in the validating object.
>      */
>     skipNullProperties?: boolean;
>     /**
>      * If set to true then validator will skip validation of all properties that are null or undefined in the validating object.
>      */
>     skipMissingProperties?: boolean;
>     /**
>      * If set to true validator will strip validated object of any properties that do not have any decorators.
>      *
>      * Tip: if no other decorator is suitable for your property use @Allow decorator.
>      */
>     whitelist?: boolean;
>     /**
>      * If set to true, instead of stripping non-whitelisted properties validator will throw an error
>      */
>     forbidNonWhitelisted?: boolean;
>     /**
>      * Groups to be used during validation of the object.
>      */
>     groups?: string[];
>     /**
>      * Set default for `always` option of decorators. Default can be overridden in decorator options.
>      */
>     always?: boolean;
>     /**
>      * If [groups]{@link ValidatorOptions#groups} is not given or is empty,
>      * ignore decorators with at least one group.
>      */
>     strictGroups?: boolean;
>     /**
>      * If set to true, the validation will not use default messages.
>      * Error message always will be undefined if its not explicitly set.
>      */
>     dismissDefaultMessages?: boolean;
>     /**
>      * ValidationError special options.
>      */
>     validationError?: {
>         /**
>          * Indicates if target should be exposed in ValidationError.
>          */
>         target?: boolean;
>         /**
>          * Indicates if validated value should be exposed in ValidationError.
>          */
>         value?: boolean;
>     };
>     /**
>      * Settings true will cause fail validation of unknown objects.
>      */
>     forbidUnknownValues?: boolean;
>     /**
>      * When set to true, validation of the given property will stop after encountering the first error.
>      * This is enabled by default.
>      */
>     stopAtFirstError?: boolean;
> }
> ```
> 
> ```typescript
> /**
>  * If set to true validator will strip validated object of any properties that do not have any decorators.
>  *
>  * Tip: if no other decorator is suitable for your property use @Allow decorator.
>  */
> whitelist?: boolean;
> ```
> 
> 호오
> 
> class-validator에서 가져온 데코레이터도 안 붙이고 마구잡이로 값을 집어 넣으려 시도하다???
> 이런싸가지없는
> 즉결 처형인 것이다
> 
> 아주 좋은 옵션이네용
> 
> 당장 추가해보다
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> import { ValidationPipe } from '@nestjs/common';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     app.useGlobalPipes(new ValidationPipe({ whitelist: true }));
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> 테스트:
> 
> ![[image 45.png]]
> 
> ?
> 
> GET 요청을 보내 확인해야 하나
> 
> ![[image 46.png]]
> 
> 아
> 
> 오
> 
> 음
> 
> 어
> 
> 아
> 
> 아
> 
> 이해한
> 
> whitelist라는 옵션은 즉결 처형이 아닌
> 아 즉결 처형이 맞긴 한가
> 
> 등록되지 아니한 값을 싹 다 걸러버리고 남은 등록된 값만 통과시키는 무언가인
> 
> 그러면 올렸을 때 에러를 터트릴 수는 없는 것인?
> 
> ```typescript
> /**
>  * If set to true, instead of stripping non-whitelisted properties validator will throw an error
>  */
> forbidNonWhitelisted?: boolean;
> ```
> 
> 오
> 
> 바로 이거로구나
> 
> 당장 적용시키다
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> import { ValidationPipe } from '@nestjs/common';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     app.useGlobalPipes(new ValidationPipe({
>         whitelist: true,
>         forbidNonWhitelisted: true
>     }));
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> 테스트:
> 
> ![[image 47.png]]
> 
> 아주좋았어
> 
> 그래서
> 
> Param 데코레이터로 가져오던 id 있잖아요?
> 
> 예시로 들고 오다 MoviesController.getOne
> 
> ```typescript
> @Get("/:id")
> getOne(@Param("id") id:string):Movie {
>     return this.moviesService.getOne(id);
> }
> ```
> 
> Service라던가
> 
> id를 죄다 숫자로 가공해서 사용한단 말이죠?
> 
> 근데 이거는
> 씨
> 
> string으로 받고 있잖아요
> 
> 물론 URL으로 받는 경로 매개변수는 무조건 string으로 받아지기 때문이긴 합니다만
> 
> 그래도 아니꼬움
> ㅇㅇ
> 
> 그래서 ValidatorPipe에 다음 옵션을 추가로 덧붙이다
> 
> ```typescript
> transform?: boolean;
> ```
> 
> 이것은 사용자가 보낸 값을 실제 우리가 원하는 값으로 자동-변형시켜주는
> 
> 어찌 보자면 그 누구보다 JS스러운 옵션이긴 합니다만
> 
> 맛있으면 됐음
> ㅇㅇ
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> import { ValidationPipe } from '@nestjs/common';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     app.useGlobalPipes(new ValidationPipe({
>         whitelist: true,
>         forbidNonWhitelisted: true,
>         transform: true
>     }));
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> ```typescript
> // /src/movies/movies.controller.ts
> import { Body, Controller, Delete, Get, Param, Patch, Post, Put, Query } from '@nestjs/common';
> import { MoviesService } from './movies.service';
> import { Movie } from './entities/Movie';
> import { CreateMovieDTO } from './dto/create-movie.dto';
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
>     patchMovie(@Param("id") id:number, @Body() updateData:object) {
>         return this.moviesService.patchMovie(id, updateData);
>     }
> }
> ```
> 
> ```typescript
> // /src/movies/movies.service.ts
> import { Injectable, NotFoundException } from '@nestjs/common';
> import { Movie } from './entities/Movie';
> import { CreateMovieDTO } from './dto/create-movie.dto';
> 
> @Injectable()
> export class MoviesService {
>     private movies:Movie[] = [];
> 
>     getAll():Movie[] {
>         return this.movies;
>     }
> 
>     getOne(id:number):Movie {
>         const movie:Movie | undefined = this.movies.find((movie) => {
>             return movie.id === id;
>         });
> 
>         if(!movie) {
>             throw new NotFoundException(`Movie with ID ${id}: not found`);
>         }
> 
>         return movie;
>     }
> 
>     createMovie(movieData:CreateMovieDTO):number {
>         return this.movies.push({
>             id: this.movies.length + 1,
>             ...movieData
>         });
>     }
> 
>     deleteMovie(id:number) {
>         this.getOne(id);
>         this.movies = this.movies.filter((movie) => {
>             return movie.id !== id;
>         });
>     }
> 
>     patchMovie(id:number, updateData:object) {
>         const movie = this.getOne(id);
>         this.deleteMovie(id);
>         this.movies.push({ ...movie, ...updateData });
>     }
> }
> ```
> 
> 여기에 추가로 다음을 추가하다
> 
> ```typescript
> console.log(typeof id);
> ```
> 
> ![[image 48.png]]
> 
> 와
> 
> 진짜
> 
> 이거지
> ㅇㅇ
> 
> 근데
> 
> updateData에 타입 안 달아두긴 함
> 
> DTO를 추가하러 가보다

> [!note]+ # #2.5 DTOs and Validation part Two
> 네
> 
> update-movie.dto.ts를 /dto 폴더 안에 만들어 정의해보다
> 
> 그리고 기본적으로는 CreateMovieDTO의 내용을 복사 붙여넣기할 예정인
> 
> ```typescript
> // /src/movies/dto/update-movie.dto.ts
> import { IsNumber, IsString } from "class-validator";
> 
> export class UpdateMovieDTO {
>     @IsString()
>     readonly title!:string;
>     @IsNumber()
>     readonly year!:number;
>     @IsString({ each: true })
>     readonly genres!:string[];
> }
> ```
> 
> 근데
> 씨
> 
> 업데이트한답시고 모든 필드를 꽉꽉 채워야만 하는 거에요???
> 
> 아니죠
> 
> 그래서 우리는 optional로 만들 것인
> 
> ```typescript
> // /src/movies/dto/update-movie.dto.ts
> import { IsNumber, IsString } from "class-validator";
> 
> export class UpdateMovieDTO {
>     @IsString()
>     readonly title!:string;
>     @IsNumber()
>     readonly year!:number;
>     @IsString({ each: true })
>     readonly genres!:string[];
> }
> ```
> 
> ```typescript
> // /src/movies/movies.controller.ts
> @Patch("/:id")
> patchMovie(@Param("id") id:number, @Body() updateData:UpdateMovieDTO) {
>     return this.moviesService.patchMovie(id, updateData);
> }
> ```
> 
> ```typescript
> // /src/movies/movies.service.ts
> patchMovie(id:number, updateData:UpdateMovieDTO) {
>     const movie = this.getOne(id);
>     this.deleteMovie(id);
>     this.movies.push({ ...movie, ...updateData });
> }
> ```
> 
> 테스트:
> 
> ![[image 49.png]]
> 
> ![[image 50.png]]
> 
> ???
> 
> 네
> 
> 뭐
> 
> 당연하게도
> 
> class-validator 때문이라고 할 수 있겠구요
> 
> 그래서 우리는 NestJS의 새로운 기능
> 
> 이름하야 Partial Types를 사용해볼 것입니다
> 
> 한국어로 대충 번역하면
> 부분 타입이라는 뜻이죠???
> 
> 근데 이를 위해서는 설치해야 하는
> 
> 커맨드에 다음을 입력하다:
> 
> ```bash
> npm install @nestjs/mapped-types
> ```
> 
> mapped-types라고 하자면
> 
> 타입을 변환, 사용할 수 있는 package구요
> 
> 공식 문서를 살펴보다:
> 
> [www.npmjs.com](https://www.npmjs.com/package/@nestjs/mapped-types)
> 
> 그래서 보면
> 
> ![[image 51.png]]
> 
> GraphQL과 Swagger NestJS package를 사용하였다고 되어 있구요
> 
> GraphQL은 검색해보니
> REST API처럼 API를 구성하는 방법인 것 같구요
> 
> Swagger는 검색해보니
> API 문서를 자동으로 작성해주는 무언가인 것 같구요
> 
> 잘은 모르겠네용
> 
> ```typescript
> // /src/movies/dto/update-movie.dto.ts
> import { PartialType } from "@nestjs/mapped-types";
> import { CreateMovieDTO } from "./create-movie.dto";
> 
> export class UpdateMovieDTO extends PartialType(CreateMovieDTO) {}
> ```
> 
> 극한의 단축 딸-깍이 가능해지구요
> 
> 약간
> 
> ```typescript
> type Partial<T> = { [P in keyof T]?: T[P] | undefined; }
> ```
> 
> 이거마냥 원래의 타입을 전체 optional로 변환시키는 느낌이구요
> 
> 그래서 CreateMovieDTO를 원형으로 두었다 치고
> UpdateMovieDTO를 전체 필드 optional로 변형시켜 타입 별칭 느낌으로 붙인 느낌이 강해진 것이구요
> 
> 아주 좋은 것이죠 저거
> 
> 이제 변경점이 있을 때
> UpdateMovieDTO까지 왔다 갔다 하면서 같이 변경해야 할 필요가 없어짐
> 
> ![[image 52.png]]
> 
> ![[image 53.png]]
> 
> ![[image 54.png]]
> 
> 아주좋았어
> 
> 아주완벽해
> 
> 아주행복해
> 
> 크하하하하하하하하하하하하하하하
> 
> 그러하구요
> 
> 근데 장르를 굳이 강제해야 할 필요는 딱히 없는 듯
> ㅇㅇ
> 
> ```typescript
> // /src/movies/dto/create-movie.dto.ts
> import { IsNumber, IsOptional, IsString } from "class-validator";
> 
> export class CreateMovieDTO {
>     @IsString()
>     readonly title!:string;
> 
>     @IsNumber()
>     readonly year!:number;
> 
>     @IsOptional()
>     @IsString({ each: true })
>     readonly genres!:string[];
> }
> ```
> 
> 딸ㅋㅋ깍ㅋㅋ
> 
> ![[image 55.png]]
> 
> ![[image 56.png]]
> 
> 와
> 
> 진짜
> 
> 맛있다
> 
> 크하하하하하하하하하하하하하하하하하하하하하하하하
> 
> 크하싸
> 
> 뭐 근데
> 
> 앞으로 직접 개발할 때도 그러하고 하지만
> 
> 문서를 봐야 할 필요가 있을 듯
> ㅇㅇ
> 
> class-validator 공식 문서를 확인해봅시다:
> 
> [www.npmjs.com](https://www.npmjs.com/package/class-validator)
> 
> ![[image 57.png]]
> 
> interesting
> 
> 길이도 제한 가능
> 무엇이 들어 있어야만 하는지도 강제 가능
> 숫자의 경우 최소 최대 설정 가능
> 이메일 강제 가능
> 
> 진짜 쩌는 라이브러리였구용
> 
> 크하하

> [!note]+ # #2.6 Modules and Dependency Injection
> 우리가 만든 API를 이대로 끝내기 전에
> 
> AppModule을 조금 더 좋은 구조로 만들어보다
> 
> ```typescript
> // /src/app.module.ts
> import { Module } from '@nestjs/common';
> import { MoviesController } from './movies/movies.controller';
> import { MoviesService } from './movies/movies.service';
> 
> @Module({
>     imports: [],
>     controllers: [MoviesController],
>     providers: [MoviesService],
> })
> export class AppModule {}
> ```
> 
> 물론 @nestjs/cli가 자동으로 추가해준 것들이긴 하다만
> 
> app.module.ts의 AppModule은
> app.controller.ts의 AppController
> app.service.ts의 AppService
> 이것들만 가지고 있었어야 했음
> 
> 그래서 MoviesController와 MoviesService를 movies.module.ts의 MoviesModule로 옮겨 분리시키다
> 
> NestJS의 앱은 여러 모듈로 구성됨
> 
> 저번에 들었던 예시처럼 AppModule이 트리 구조로 따지자면 root
> 그 밑에 달라 붙어 있는 다른 여러 Module들이 트리 구조로 따지자면 자식 노드가 되는 느낌임
> ㅇㅇ
> 
> ![[Modules.png]]
> 
> 그래서
> 
> CMD에 다음 커맨드를 작성하여 넣고 내려
> 
> ```bash
> nest generate module movies /
> ```
> 
> 극한으로 축약하자면 다음과 같아지는
> 
> ```bash
> nest g mo
> ```
> 
> 이러언
> 
> 그러면 디렉터리 구조는 다음과 같아지는
> 
> 디렉터리:
> 
> - /src
>     - /movies
>         - /dto
>             - create-movie.dto.ts
>             - update-movie.dto.ts
>         - /entities
>             - movie.entity.ts
>         - movies.module.ts
>         - movies.controller.ts
>         - movies.service.ts
>     - app.module.ts
>     - app.controller.ts
>     - app.service.ts
> 
> ```typescript
> // /src/movies/movies.module.ts
> import { Module } from '@nestjs/common';
> import { MoviesController } from './movies.controller';
> import { MoviesService } from './movies.service';
> 
> @Module({})
> export class MoviesModule {}
> ```
> 
> ?
> 
> 이미 AppModule에 다 되어 있는 상태이기 때문에
> 
> MoviesModule은 쉬었음 Module이 되어 버린
> 
> 씨
> 
> 고치다
> 
> ```typescript
> // /src/movies/movies.module.ts
> import { Module } from '@nestjs/common';
> import { MoviesController } from './movies.controller';
> import { MoviesService } from './movies.service';
> 
> @Module({
>     imports: [],
>     controllers: [MoviesController],
>     providers: [MoviesService]
> })
> export class MoviesModule {}
> ```
> 
> ```typescript
> // /src/app.module.ts
> import { Module } from '@nestjs/common';
> import { MoviesModule } from './movies/movies.module';
> 
> @Module({
>     imports: [MoviesModule],
>     controllers: [],
>     providers: [],
> })
> export class AppModule {}
> ```
> 
> 아주좋았어
> 
> 이제  app.controller.ts와 app.service.ts를 다시 생성할 것인
> 
> ```bash
> nest g co app /
> nest g s app /
> ```
> 
> 이 커맨드를 입력하게 되면 /app이 /src 안에 생기게 될 텐데
> 
> 밖(→ /src)에 꺼내 두고 /app을 지워도 된다고 하구요
> 
> 그래서 죽은 자의 소생을 시켜버린 AppController에게는 무엇을 맡겨버리다???
> 
> 그냥 홈페이지를 가져오게 하면 어떠한?
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
> 서버가 잘 살아 있는지 등으로 이렇게 반환하게 한다면 확인하기에도 좋을 듯
> 
> ![[image 58.png]]
> 
> 아주좋았어
> 
> 뭐
> 
> 또한
> NestJS에는 Dependency Injection이라 부르는 것이 존재함
> 
> 네
> DI죠???
> 
> 뭐
> 
> 할 말이 매우 많은 개념이라 할 수 있겠는데
> 
> 일단 Controller들 짜면서 constuctor에 private readonly ~~Service:~~Service 이렇게 받아오려 했던 것을 기억해야 하다
> 
> 실제로 우리가 new ~~Controller() 안에 ~~Service를 직접 집어 넣어본 적은 없을 것인
> 
> 그것이 바로 DI라 부를 수 있는 것이구요
> 
> 또한 Controller들에서 타입만 import하고 추가해둬도 잘 작동하는 것 또한 ~~Service가 잘 주입되어서 그런 것이잖아요?
> 
> 그래서 그러하구요
> 
> 이러언

> [!note]+ # #2.7 Express on NestJS
> 언제나 강조하는 것이지만
> 
> NestJS는 Express 위에서 돌아갑니다???
> 
> Controller에서 Request, Response가 필요한 순간이 생긴다고 한다면
> 
> 그냥 사용하면 되는 거임
> ㅇㅇ
> 
> ## Req 데코레이터
> 
> 네
> 
> 말 그대로 Request 객체를 받아오는 데코레이터구요
> 
> 보통 req를 req라 쓰지
> request라고 풀로 적지는 않잖아요???
> 
> 그래서 데코레이터 이름도 Req인 듯
> ㅇㅇ
> 
> ## Res 데코레이터
> 
> 마찬가지로
> 
> 말 그대로 Response 객체를 받아오는 데코레이터구요
> 
> 보통 res를 res라 쓰지
> response라고 풀로 적지는 않잖아요???
> 
> 그래서 데코레이터 이름도 Res인 듯
> ㅇㅇ
> 
> ```typescript
> // /src/app.controller.ts
> import { Controller, Get, Req, Res } from '@nestjs/common';
> import type { Request, Response } from 'express';
> 
> @Controller()
> export class AppController {
>     @Get()
>     getHome(@Req() req:Request, @Res() res:Response):string {
>         console.log(req.url);
>         return "Welcome to my Movie API";
>     }
> }
> ```
> 
> ![[image 59.png]]
> 
> 네
> Express구요
> 
> 근데 뭐
> 
> 그렇게까지 좋은 생각은 아니라고 하구요
> 
> 물론 저레벨의 세세한 구현을 할 때 용이하겠지만은
> 
> NestJS는 Express 말고도 Fastify라고 하는 라이브러리 위에서도 돌아갈 수 있기 때문에
> 
> 호환성 이슈가 될 수도 있을 것 같구요
> 
> 여기에서 Fastify라고 하는 것은 말 그대로 빠른 것에 중점을 두기 때문에
> 
> Express보다 2배 정도 이상 빠르다고 하구요
