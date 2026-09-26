> [!note]+ # #1.0 Overview
> NestJS는 우리를 위해 이미 셋팅해둔 것들을 제공하다
> 
> > [!note]+ 예를 들어보다:
> > ```json
> > // nest-cli.json
> > {
> >   "$schema": "https://json.schemastore.org/nest-cli",
> >   "collection": "@nestjs/schematics",
> >   "sourceRoot": "src",
> >   "compilerOptions": {
> >     "deleteOutDir": true
> >   }
> > }
> > ```
> > 
> > 또는
> > 
> > ```json
> > // package.json
> > {
> >   // ...
> >   // 미리 정의된 스크립트들
> >   "scripts": {
> > 	  "build": "nest build",
> >     "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
> >     "start": "nest start",
> >     "start:dev": "nest start --watch",
> >     "start:debug": "nest start --debug --watch",
> >     "start:prod": "node dist/main",
> >     "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
> >     "test": "jest",
> >     "test:watch": "jest --watch",
> >     "test:cov": "jest --coverage",
> >     "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
> >     "test:e2e": "jest --config ./test/jest-e2e.json"
> >   },
> >   // 의존성들과
> >   "dependencies": {
> >     "@nestjs/common": "^11.0.1",
> >     "@nestjs/core": "^11.0.1",
> >     "@nestjs/platform-express": "^11.0.1",
> >     "reflect-metadata": "^0.2.2",
> >     "rxjs": "^7.8.1"
> >   },
> >   // 개발 의존성들까지
> >   "devDependencies": {
> >     "@eslint/eslintrc": "^3.2.0",
> >     "@eslint/js": "^9.18.0",
> >     "@nestjs/cli": "^11.0.0",
> >     "@nestjs/schematics": "^11.0.0",
> >     "@nestjs/testing": "^11.0.1",
> >     "@types/express": "^5.0.0",
> >     "@types/jest": "^30.0.0",
> >     "@types/mocha": "^10.0.10",
> >     "@types/node": "^24.0.0",
> >     "@types/supertest": "^7.0.0",
> >     "eslint": "^9.18.0",
> >     "eslint-config-prettier": "^10.0.1",
> >     "eslint-plugin-prettier": "^5.2.2",
> >     "globals": "^17.0.0",
> >     "jest": "^30.0.0",
> >     "prettier": "^3.4.2",
> >     "source-map-support": "^0.5.21",
> >     "supertest": "^7.0.0",
> >     "ts-jest": "^29.2.5",
> >     "ts-loader": "^9.5.2",
> >     "ts-node": "^10.9.2",
> >     "tsconfig-paths": "^4.2.0",
> >     "typescript": "^5.7.3",
> >     "typescript-eslint": "^8.20.0"
> >   },
> >   // ...
> > }
> > ```
> > 
> > 그리고 TS를 위한 컴파일러 설정과
> > 
> > ```json
> > // tsconfig.json
> > {
> >   "compilerOptions": {
> >     "module": "nodenext",
> >     "moduleResolution": "nodenext",
> >     "resolvePackageJsonExports": true,
> >     "esModuleInterop": true,
> >     "isolatedModules": true,
> >     "declaration": true,
> >     "removeComments": true,
> >     "emitDecoratorMetadata": true,
> >     "experimentalDecorators": true,
> >     "allowSyntheticDefaultImports": true,
> >     "target": "ES2023",
> >     "sourceMap": true,
> >     "outDir": "./dist",
> >     "baseUrl": "./",
> >     "incremental": true,
> >     "skipLibCheck": true,
> >     "strictNullChecks": true,
> >     "forceConsistentCasingInFileNames": true,
> >     "noImplicitAny": false,
> >     "strictBindCallApply": false,
> >     "noFallthroughCasesInSwitch": false,
> >   }
> > }
> > ```
> > 
> > 빌드 설정까지
> > 
> > ```json
> > // tsconfig.build.json
> > {
> >   "extends": "./tsconfig.json",
> >   "exclude": ["node_modules", "test", "dist", "**/*spec.ts"]
> > }
> > ```
> > 
> > 외에 /test, controller, spec, module, service와 main까지
> > 
> > 다 해줬잖아
> 
> spec이 붙어 있는 파일은 일단 지우다
> 나중에 다시 만들 예정인
> 직접 만들 수 있어야 써먹을 수도 있겠지
> 
> package.json의 scripts를 보면:
> 
> ```json
> // package.json
> {
> 	// ...
> 	"scripts": {
> 		// ...
> 		"start": "nest start",
>     "start:dev": "nest start --watch",
>     "start:debug": "nest start --debug --watch",
>     "start:prod": "node dist/main",
> 		// ...
> 	}
> 	// ...
> }
> ```
> 
> 이러한 것들이 존재하는데
> 
> 이 중에서 start:dev를 사용하다
> 
> ```bash
> npm run start:dev
> ```
> 
> TS가 7.0으로 올라가면서 baseUrl이 불필요하게 되었는데
> 주석처리하고 실행하면 됨
> ㅇㅇ
> 
> NestJS에는 main.ts가 무조건 존재함
> 근데 이건 당연한 소리구요
> 이름 바꿔버리면 큰 일은 아니고
> 실행이 안 되겠죠???
> 이러언
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> bootstrap 비동기 함수는 뭐
> await 없이 그냥 호출되어 값이 오기도 전에 Promise만 남기고 사라질 운명처럼 생기긴 했는데
> 아쉬운 것이라 부르기로 하고
> 
> > [!note]+ bootstrap 호출에 대한 고찰:
> > 근데 await 없이도 await app.listen(process.env.PORT ?? 3000); 덕분에 HTTP 서버가 생성된다고 하네요
> > 이 HTTP 서버는 이벤트 루프에 핸들을 등록하기에 Node 프로세스가 살아있게 된다고 합니다
> > 이러언
> > 
> > 근데 문제가 저래버리면 bootstrap에
> > 
> > ```typescript
> > throw new Error();
> > ```
> > 
> > 를 던져버렸을 때
> > 
> > 반환된 Promise를 처리하는 이가 아무도 없음
> > ㅇㅇ
> > 
> > 그래서 실무에서는
> > 
> > ```typescript
> > bootstrap().catch((err) => {
> > 	console.error(err);
> > 	process.exit();
> > });
> > ```
> > 
> > 로 보통 많이 쓴다고 하네요
> 
> ![[image.png]]
> 
> 아무튼 그래서 Hello World!라는 저 문자열은 어디에서 왔는가?
> 
> AppModule에 Ctrl + LClick을 하여 그 정체를 밝히다
> 
> ```typescript
> // /src/app.module.ts
> import { Module } from '@nestjs/common';
> import { AppController } from './app.controller';
> import { AppService } from './app.service';
> 
> @Module({
>     imports: [],
>     controllers: [AppController],
>     providers: [AppService],
> })
> export class AppModule {}
> ```
> 
> 무슨 Python마냥 @을 붙이고 있는데
> 
> 저것은 데코레이터 문법이라 부르다
> Python과 거의 완전히 비슷한;;;
> 
> NestJS는 데코레이터와 함께하는 프레임워크이기 때문에
> 익숙해져야 할 필요가 있다는데
> Python과 discord.py로 봇 개발을 끼요옷하다 보면 자연스레 익숙해지는 부분이니
> 봇 개발 한 번 정도는 괜찮을 것 같구요
> 이러언
> 
> 왜냐하면 데코레이터는 클래스에 함수 기능을 추가할 수 있기 때문이라 하네요
> 
> 그래서 AppModule은 비어 있는 클래스인데 어떻게 Hello World!를 반환하다?
> 
> 그 답은 이러한:
> 
> Module 데코레이터 안을 보면
> imports, controllers, providers가 있음
> 
> controllers를 보면 AppController가 있는데
> 들어가 보자면
> 
> ```typescript
> // /src/app.controller.ts
> import { Controller, Get } from '@nestjs/common';
> import { AppService } from './app.service';
> 
> @Controller()
> export class AppController {
>     constructor(private readonly appService:AppService) {}
> 
>     @Get()
>     getHello():string {
>         return this.appService.getHello();
>     }
> }
> ```
> 
> 그러면 또 Get 데코레이터가 보이는
> 
> 추론하다:
> 
> HTTP GET 요청인?
> 
> 아무튼 그래서 this.appService가 또 보이는???
> 
> ```typescript
> // /src/app.service.ts
> import { Injectable } from '@nestjs/common';
> 
> @Injectable()
> export class AppService {
>     getHello():string {
>         return 'Hello World!';
>     }
> }
> ```
> 
> 여기가 진짜로구나
> 고노야로
> 
> 그래서 이번에는 Injectable 데코레이터가 보이는
> 
> 추론하다:
> 
> 삽입 가능한을 interface로 하면 당연히 NestJS가 딸-깍하지 못 하겠죠???
> 그래서 데코레이터로 준비하여 다-해줬잖아
> 
> 그래서 getHello 메서드를 발견할 수 있는
> 
> 결론:
> 
> Hello World!라는 문자열은
> AppModule(Module 데코레이터의 Controller) → AppController(constructor의 appService:AppService) → AppService.getHello()에서 온 것인
> 
> 그래서 이것을 “안녕 못 해”라 변경하면
> 
> ![[image 1.png]]
> 
> 아주좋았어

> [!note]+ # #1.1 Controllers
> 당연한 소리:
> NestJS는 main.ts에서 모든게 시작한다
> 
> ```typescript
> // /src/main.ts
> import { NestFactory } from '@nestjs/core';
> import { AppModule } from './app.module';
> 
> async function bootstrap() {
>     const app = await NestFactory.create(AppModule);
>     await app.listen(process.env.PORT ?? 3000);
> }
> bootstrap();
> ```
> 
> await NestFactory.create(AppModule);을 app에 담고 있는데
> 상수 이름을 보아하니 앱을 생성한 듯 보임
> ㅇㅇ
> 
> 그래서 모듈로부터 앱을 생성한다고 하네요
> 근데 new AppModule();로 생성하는 것이 아니라 create에게 양도하는 느낌인 듯
> 
> > [!note]+ AI에게 물어보다
> > 1. AppModule은 설계도라 볼 수 있다
> >     보통 클래스를 설계도로 비유하는데 그것과 무슨 차이가 있나 생각할 수 있음
> > 그러나 이것은 진짜 설계도라 볼 수 있음
> >     왜냐하면 Module 데코레이터를 붙인 것 외에는 그냥 빈 클래스이기 때문
> > ![[image 2.png]]
> >     자동 완성으로도 뜨는게 없음
> > 2. 그럼 비어 있는 AppModule의 생성 책임을 create로 넘겨봤자 무슨 쓸모가 있지???
> >     아마 추론하기로는 다음과 같을 것인:
> >     create에는 Reflect로 동적 찾기
> > → Module 데코레이터가 붙여준 controllers, providers와 같은 메타데이터를 확인하여 DI(의존성 주입) 후 그대로 const app에 넘겨주기
> >     아주 좋았어
> >     이것으로 딸-깍 코딩이 가능해지는
> > 3. 당연한 소리: create에 생성 책임을 넘기는 이유
> >     그럼 뭐
> > DI는 직접 하세요???
> >     AI said:
> > > "이 모듈을 루트 모듈로 해서 DI 컨테이너를 만들고, 컨트롤러들을 등록하고, HTTP 서버를 구성한 Nest 애플리케이션을 생성해줘”
> > 4. 그러면 NestFactory.create가 반환하는 app은 무엇인?
> >     단순한 Express 객체가 아닌 INestApplication의 구현체
> > ![[image 3.png]]
> >     반환값은 다음과 같아버리는
> > ```typescript
> > app.listen(3000);
> > app.use(...);
> > app.enableCors();
> > ```
> >     이러한 NestJS 전용 기능들을 제공함
> >     물론 기본적으로 Express를 사용하지만
> >     다음과 같다고 함:
> > ```plain text
> > Nest Application
> >     ↓
> > Express Adapter
> >     ↓
> > Express Server
> > ```
> > 5. Module로부터 app을 생성한다란?
> >     무엇보다 NestJS에서 Module이라는 것은 단순한 파일 묶음이 아님
> > 애플리케이션 구조를 정의하는 루트 노드라고 함
> >     예:
> > ```typescript
> > @Module({
> >   imports: [
> >     UserModule,
> >     AuthModule,
> >     ProductModule,
> >   ],
> > })
> > export class AppModule {}
> > ```
> >     이러면 Nest는 AppModule을 루트로 트리를 탐색함
> > ```plain text
> > AppModule
> >  ├─ UserModule
> >  ├─ AuthModule
> >  └─ ProductModule
> > ```
> >     그리고 다음으로는
> >     - Controller 등록
> >     - Service 생성
> >     - DI 연결
> >     - Router 생성
> >     아주좋았어
> >     그래서
> > ```typescript
> > NestFactory.create(AppModule);
> > ```
> >     AI said:
> > > "AppModule을 루트로 하는 Nest 애플리케이션을 부트스트랩(bootstrap)해줘”
> > 
> >     그렇다고 하네요
> > 
> 
> App 모듈은 모든 것들의 루트 모듈이라고 함
> 
> 만약 우리가 Django를 사용한다면
> 모듈은 앱처럼 될 수 있다고 하네요
> 
> > [!note]+ 예를 들어보다:
> > 인증을 담당하는 어플리케이션이 있다면
> > 그것은 users 모듈이 될 것인
> > 
> > 그리고
> > 음
> > 어
> > 에
> > 어
> > 음
> > 
> > 인스타그램을 만든다고 치자면
> > photos 모듈 같은 무언가가 필요하겠구요
> > videos 모듈도 필요할 수 있겠네요
> > 
> > 그리고 우리는 이것을 이렇게 부르다
> > 
> > > ***”Module”***
> 
> 여기서 알아야 할 것들:
> 
> 1. Controller
> 2. Provider
> 
> ## Controller
> 
> Controller가 하는 일은 기본적으로
> URL을 가져오고 함수를 실행하는 것이라고 하네요
> 
> > [!note]+ Express 사용해본 사람들을 위한 설명:
> > Express의 라우터와 같은 존재라고 하네요
> 
> ```typescript
> // /src/app.controller.ts
> import { Controller, Get } from '@nestjs/common';
> import { AppService } from './app.service';
> 
> @Controller()
> export class AppController {
>     constructor(private readonly appService:AppService) {}
> 
>     @Get()
>     getHello():string {
>         return this.appService.getHello();
>     }
> }
> ```
> 
> 정확히는
> 
> ```typescript
> @Get()
> getHello():string {
>     return this.appService.getHello();
> }
> ```
> 
> 저번에 넘어갔던 Get 데코레이터가 보임
> 
> 그리고 이는 Express의 app.get()과 같은 역할을 함
> 
> 그러면 우리는 다음과 같은 것을 시도하다
> 
> ```typescript
> @Get("/hello")
> sayHello():string {
>     return "안녕한";
> }
> ```
> 
> 아까도 말했다시피 Controller는 URL을 가져오는 역할을 함
> 
> 그리고 path 매개변수에는 “/hello” 인자를 넘긴
> 
> URL: /hello
> 
> 사용자가 /hello에 대해 엑세스하면???
> Controller 안에 새로 추가한 sayHello를 호출한다고 하네요
> 
> 우리는 Get 데코레이터를 딸-깍 붙여두었기 때문에
> Nest도 딸-깍으로 누군가 /hello GET으로 요청을 보내었을 때 sayHello를 호출해야 한다는 사실을 알 수 있게 되었음
> 
> 아주좋았어
> 
> > [!note]+ 당연한 소리:
> > ```typescript
> > // 잘못된 코드
> > // @Get("/hello")
> > 
> > 
> > 
> > 
> > // sayHello():string {
> > //     return "안녕한";
> > // }
> > ```
> > 
> > 누가 데코레이터를 띄워서 작업해요
> > 이게뭐야
> 
> > [!note]+ 다시 한 번 Express로 예를 들다:
> > Controller는 Express의 controller/router 같은 것입니다
> > 이러언
> > 
> > Express에서는 app.get();을 사용하여 안에 함수를 넘겼죠
> > 
> > 여기에서 보자면
> > 
> > Get 데코레이터를 붙이는 것 제외하고는 비슷하다고 할 수 있음
> > 
> > 근데
> > 씨
> > 데코레이터가 가독성이 더 좋다고 생각함
> > ㅇㅇ
> > 
> > ```typescript
> > app.get("/hello", (req, res) => {
> > 		return res.send("안녕한");
> > });
> > ```
> > 
> > > [!note]+ 또는
> > > ```typescript
> > > function sayHello(req:Request, res:Response):void{
> > > 		return res.send("안녕한");
> > > }
> > > 
> > > app.get("/hello", sayHello);
> > > ```
> > 
> > 이런 것들보다
> > 
> > ```typescript
> > @Get("/hello")
> > sayHello():string {
> > 		return "안녕한";
> > }
> > ```
> > 
> > 이게 더 가독성이 좋지 않나 생각하고 있구요
> > 
> > 아
> > 근데
> > 
> > ```typescript
> > // /src/services/helloService.ts
> > export function sayHello():string {
> > 		return "안녕한";
> > }
> > ```
> > 
> > ```typescript
> > // /src/controllers/helloController.ts
> > import { sayHello } from "../services/helloService";
> > 
> > export function sayHello(req:Request, res:Response):void {
> > 		return res.send(sayHello());
> > }
> > ```
> > 
> > ```typescript
> > // /src/routers/helloRouters.ts
> > import { sayHello } from "../controllers/helloController";
> > 
> > const router = Router();
> > 
> > router.get("/hello", sayHello);
> > 
> > export default router;
> > ```
> > 
> > ```typescript
> > // src/app.ts
> > import express from "express";
> > import helloRouters from "./routers/helloRouters";
> > 
> > const app = express();
> > 
> > app.use(helloRoutes);
> > ```
> > 
> > 이렇게 분리하면 충분히 책임 분할도 되고
> > 은근 맛있을지도
> 
> 다시 한 번 요약하자면:
> 
> 코레가- Controller다-
> 
> URL을 가져와 함수로 매핑한다 생각해도 좋을 듯
> 
> ```typescript
> import { Request, Response } from "express";
> 
> type RESTCallback = () => any;
> 
> const getMap = new Map<string, RESTCallback>();
> const postMap = new Map<string, RESTCallback>();
> const putMap = new Map<string, RESTCallback>();
> const deleteMap = new Map<string, RESTCallback>();
> 
> function sayHello():string {
> 		return "안녕한";
> }
> 
> getMap.set("/hello", sayHello);
> // ...
> ```
> 
> 그래서 NestJS를 사용한다면???
> 라우터는 개에게 밥으로써 줄 수 있구요
> 끼얏호우
> 
> Get 데코레이터를 달아둔 것만으로도 GET 요청을 딸-깍할 수 있구요
> 크하하
> 
> 마찬가지로
> 
> ```typescript
> @Post("/hello")
> sayHello():string {
>     return "안녕한";
> }
> ```
> 
> 이렇게 달아두면 POST 요청이 되는 것이구요
> 
> ![[image 4.png]]
> 
> 근데 Get 데코레이터를 Post 데코레이터로 변경하였기 때문에
> Great한 오류 JSON이 도착했구요
> 
> 그런데 여기에서 이상한 점:
> 
> ```typescript
> constructor(private readonly appService:AppService) {}
> 
> @Get()
> getHello():string {
>     return this.appService.getHello();
> }
> ```
> 
> Service를 참조하다???
> 
> 그냥 전부 다 저기 안으로 집어 넣으면 그만 아님???
> 
> 어째서???
> 
> 네
> 
> Service는 비즈니스 로직을 담당하게 책임을 분할하면 보기 매우 좋겠죠???
> 객체지향 몇 번 해보면 자연스럽게 깨닫는 미더덕이기 때문에
> 그러하구요

> [!note]+ # #1.2 Services
> 여기에서 이어가다:
> [[1 Architecture of NestJS]] 
> 
> 우리는 구조와 아키텍처에 대해 이야기해야 할 필요가 있어진
> 
> NestJS는 아주 마음에 들게도
> 
> Controller와 비즈니스 로직(Service)을 구분 짓고 싶어 함
> 
> 그래서 결국
> Controller는 URL을 가져오는 로직과
> 그것을 매치하여 메서드를 실행하는 로직만 끼요옷하는 것인
> 이러언
> 
> 그래서 Service에 가면 또 다른 클래스가 보임
> 
> ```typescript
> // /src/app.service.ts
> import { Injectable } from '@nestjs/common';
> 
> @Injectable()
> export class AppService {
>     getHello():string {
>         return '안녕 못 해';
>     }
> }
> ```
> 
> 안에 getHello가 보이네요
> 
> 아무래도 AppController.getHello()의 return appService.getHello()가 저것 같아 보이는
> 
> 그리고 NestJS의 이 방식을 따라 AppController의 sayHello를 분리할 수 있음
> 
> > [!note]+ 변경 전:
> > ```typescript
> > // /src/app.controller.ts
> > import { Controller, Get, Post } from '@nestjs/common';
> > import { AppService } from './app.service';
> > 
> > @Controller()
> > export class AppController {
> >     constructor(private readonly appService:AppService) {}
> > 
> >     @Get()
> >     getHello():string {
> >         return this.appService.getHello();
> >     }
> > 
> >     @Get("/hello")
> >     sayHello():string {
> >         return "안녕한";
> >     }
> > }
> > ```
> > 
> > ```typescript
> > // /src/app.service.ts
> > import { Injectable } from '@nestjs/common';
> > 
> > @Injectable()
> > export class AppService {
> >     getHello():string {
> >         return '안녕 못 해';
> >     }
> > }
> > ```
> 
> > [!note]+ 변경 후:
> > ```typescript
> > // /src/app.controller.ts
> > import { Controller, Get } from '@nestjs/common';
> > import { AppService } from './app.service';
> > 
> > @Controller()
> > export class AppController {
> >     constructor(private readonly appService:AppService) {}
> > 
> >     @Get()
> >     getHello():string {
> >         return this.appService.getHello();
> >     }
> > 
> >     @Get("/hello")
> >     sayHello():string {
> >         return this.appService.sayHello();
> >     }
> > }
> > ```
> > 
> > ```typescript
> > // /src/app.service.ts
> > import { Injectable } from '@nestjs/common';
> > 
> > @Injectable()
> > export class AppService {
> >     getHello():string {
> >         return '안녕 못 해';
> >     }
> > 
> >     sayHello():string {
> >         return "안녕한";
> >     }
> > }
> > ```
> 
> 당연하겠지만 Controller와 Service의 메서드 이름은 달라도 됩니다
> 근데 그러면 각자 들어 갔을 때 보기 불편할 것이구요
> 이러언
> 
> 이렇게 운동하는 거에요
> 아주잘했어요
> 
> 그래서 Module은 하나만 존재할 수 있으며
> *아마 같은 이름으로 시작하는 파일들을 지칭하는 듯 하구요
> 그러니까 app.controller.ts, app.service.ts와 같은 것에서 app.module.ts가 2개 있으면 안 된다 이런 것을 지칭하는 것 같아용*
> 
> AppModule은 말 그대로 루트입니다
> 트리에서 가장 꼭대기가 되는 그 노드 맞구요
> 
> 우리가 하는 모든 것을 import하다
> 
> 레스토랑을 만든다???
> AppModule에 추가해야 하구요
> 
> 인증 시스템???
> 역시나 AppModule에 추가해야 하구요
> 
> AppModule에 추가해야만 하는 이유로는
> 뭐
> AppModule을 NestFactory.create에 넣고 내려
> 
> 가장 간단하게 다시 한 번 정리하자면
> Controller는 URL을 가져오고 함수의 리턴값을 반환하다
> Service는 비즈니스 로직(메서드)을 Controller에 제공하다
> 
> 또한 모든 URL은 Controller에 담다
> Service는 필요하다면 DB와 통신하여 값을 가져오다
> 
> 이제는 다음이 필요한:
> Re: 제로부터 시작하는 Nest 구조 생활
> 
> ```typescript
> // /src/app.module.ts
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
> 디렉터리:
> 
> - /src
>     - app.module.ts
>     - main.ts
> 
> ![[image 5.png]]
> 
> 씨
> 