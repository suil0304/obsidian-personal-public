> [!note]+ # #5.0 Introduction
> 드디어 컴퓨터에 밑바닥부터 TS를 설치하는 방법에 대하여 알아보는 시간
> 
> 블록 체인의 PoC
> 개념 증명이라고 하네요
> 이것을 TS 객체지향으로 만들어볼 예정이구요
> 
> 그 전에 블록 체인에 대하여 조사해보자면
> 블록 체인이라고 하는 것은
> 
> ![[image 147.png]]
> 
> 다음과 같다고 하구요
> 호오
> 
> 원래 저걸 서버에 다 보관하면
> 서버만 계속 더 무거워질 뿐이고 뭐 그러한데
> 
> 나눠서 보관하니 그렇게 크게 필요하지 않을 것 같구요
> 
> 개인 → 서버 → 개인이 아닌
> 개인 → 개인이다 보니
> 속도도 더 빠를 것 같구요
> 
> 되게 좋은 개념인 것 같네용
> interesting

> [!note]+ # #5.1 Targets
> 본격적으로 TS 개발 환경을 만들어볼 것이구요
> 
> ```bash
> npm init -y
> ```
> 
> 이러면 package.json을 만들어 주구요
> 
> 구조가 대략적으로 다음과 같이 되어 있는데
> 
> ```json
> {
>   "name": "typescript-for-beginners",
>   "version": "1.0.0",
>   "description": "",
>   "main": "index.js",
>   "scripts": {
>     "test": "echo \"Error: no test specified\" && exit 1"
>   },
>   "keywords": [],
>   "author": "",
>   "license": "ISC",
>   "type": "commonjs"
> }
> ```
> 
> main을 제거하고
> scripts를 변형할 예정이구요
> 
> ```bash
> npm install -D typescript
> ```
> 
> 이걸로 TS를 설치하는데 개발 의존성으로 설치하겠다는 소리구요
> 
> 일반적으로 TS가 런타임에서 필요한 건 아니잖아요
> 
> 또한 commonjs는 require로 모듈 import가 가능한 무언가이기 때문에
> 저는 type을 module로 변경하여 사용할 예정이구요
> 
> 이제 /src를 만든 후 거기 안에 index.ts를 만들어 줍시다
> 
> 컴파일을 해야 하는데
> 그러기 위해서는 tsconfig.json이 필요하구요
> 
> tsc에서 init을 시도하다
> 
> ```bash
> npx tsc --init
> ```
> 
> 이러면 ts의 compiler가 tsconfig.json을 추천 설정들만 활성화 시켜서 만들어 주구요
> 
> 다음과 같은 구조를 지니게 됩니다
> 
> ```bash
> {
>   // Visit https://aka.ms/tsconfig to read more about this file
>   "compilerOptions": {
>     // File Layout
>     // "rootDir": "./src",
>     // "outDir": "./dist",
> 
>     // Environment Settings
>     // See also https://aka.ms/tsconfig/module
>     "module": "nodenext",
>     "target": "esnext",
>     "types": [],
>     // For nodejs:
>     // "lib": ["esnext"],
>     // "types": ["node"],
>     // and npm install -D @types/node
> 
>     // Other Outputs
>     "sourceMap": true,
>     "declaration": true,
>     "declarationMap": true,
> 
>     // Stricter Typechecking Options
>     "noUncheckedIndexedAccess": true,
>     "exactOptionalPropertyTypes": true,
> 
>     // Style Options
>     // "noImplicitReturns": true,
>     // "noImplicitOverride": true,
>     // "noUnusedLocals": true,
>     // "noUnusedParameters": true,
>     // "noFallthroughCasesInSwitch": true,
>     // "noPropertyAccessFromIndexSignature": true,
> 
>     // Recommended Options
>     "strict": true,
>     "jsx": "react-jsx",
>     "verbatimModuleSyntax": true,
>     "isolatedModules": true,
>     "noUncheckedSideEffectImports": true,
>     "moduleDetection": "force",
>     "skipLibCheck": true,
>   }
> }
> 
> ```
> 
> 참 많은데
> 
> rootDir와 outDir의 주석을 풀어주면 딸ㅋㅋ깍ㅋㅋ이 가능해지네용
> 
> 강의에서는 compilerOptions 밖에 includes: [”src”]를 하고 있는데
> 이것은 root가 src가 되니 따로 더 포함시킬 것이 없는 한 includes는 추가하지 않아도 되구요
> 아주좋았어
> 
> 이제 package.json으로 가서 build script를 만들면 됩니다
> 
> package.json의 scripts에 다음 script를 추가하면 되구요
> 
> ```json
> "build": "npx tsc"
> ```
> 
> 또한 낮은 버전의 JS로 컴파일해야 한다 하면???
> 다 지원해줍니다
> 
> const는 나중에 나온 문법이라 낮은 버전의 JS로 가면 에러가 나는게 정상이란 말이죠???
> TS에서는 최신 문법만 사용해도
> 자연스럽게 컴파일이 가능함
> ㅇㅇ
> 
> 이제 Block class를 정의해볼 예정이구요
> 
> ```typescript
> class Block {
> 	 constructor(
> 			 private data:string
> 	 ) {}
> 	 static hello():string {
> 			 return "Hello";
> 	 }
> }
> ```
> 
> ES3와 같은 class 문법도 제대로 지원하지 않는 고노야로 세대로 컴파일하게 되었을 때
> 
> JSDoc과 함께 생성 함수 + 객체를 만드는 모습을 볼 수 있는데
> 지금 시점에서는 지원 다 끊겨서 확인이 불가능해졌구요
> 이러언

> [!note]+ # #5.2 Lib Configuration
> tsconfig.json의 lib에 대하여 알아보다
> 
> lib은 합쳐진 라이브러리의 정의 파일을 특정해주는 역할을 한다 적혀 있는데
> 이게 무슨 소리죠
> 
> 대충 이해한 대로 요약해보자면
> 사용할 라이브러리를 저기에 적었다???
> TS는 그것이 해당 환경에 쓰인다 인식하게 되고
> 자동 완성 등을 지원해준다 정도가 되려나
> 
> .d.ts라고 타입 정의 파일이 있는데 그것을 배우면서 더 자세하게 알 수 있을 것 같구요
> 흐음
> 
> 그래서 예시로
> ”dom”이라는 라이브러리를 lib에 추가해주면 TS가 document 등에 대하여 찾을 수 있지만
> ”dom”을 지우면 document에 대하여 찾지 못 하는 모습을 볼 수 있구요
> 
> ![[image 148.png]]

> [!note]+ # #5.3 Declaration Files
> .d.ts 파일입니다
> 네
> 
> 세상의 모든 JS 개발자가 TS도 함께 사용하는 것은 아닙니다
> JS로 짜여진 라이브러리의 경우 JS의 고노야로 특성 덕분에 타입이고 뭐고 전혀 알 길이 없단 말이죠
> 
> 근데 또 그렇다고 이 전부를 TS로 대체하기에는 힘들고 뭐 그렇단 말이죠
> 
> 그럴 때 .d.ts로 어떤 함수는 다음과 같고 타입은 무슨 어쩌구저쩌구 해서 서술만 잘 해두어도
> 
> 라이브러리 설치하면서 따로 @types/…로 설치가 가능해지니 아주 좋아진단 말입니다

> [!note]+ # #5.4 JSDoc
> 하지만 대부분의 경우 직접 .d.ts를 작성해야 할 일이 오지는 않습니다
> 
> 또한 JS에서 TS로 이전하고는 싶으나 힘든 경우도 다수 있을 수 있어요
> 
> 그럴 때 사용하다
> 
> ```javascript
> // @ts-check
> ```
> 
> JS 파일에서 TS와 같은 강한 타입 체크를 하라는 뜻이구요
> 
> 맨 위에 달아 사용하는 것입니다
> 
> 근데 JS에서는 타입 못 다는데 어떻게 하냐구요???
> 
> 다음을 시도하다
> 
> ```javascript
> /**
>  * @param {string} a
>  */
> function func(a) {
>     
> }
> ```
> 
> ![[image 149.png]]
> 
> 그래서 다음과 같이 JS에서도 타입을 넣을 수 있구요
> 
> 실제로 요즘에는 TS가 컴파일하는데 시간이 걸리니 차라리 JSDoc으로 갈아타는 곳도 있구요
> 다만 욕 먹는 곳도 있던데
> 이러언
> 

> [!note]+ # #5.5 Blocks
> TS로 블록체인을 해봅시다
> 
> 블록체인의 기초를 배울 수 있을 것이라 하구요
> 호오
> 
> 이러한 것을 통해 블록체인이나 가상화폐에 관심이 생겼으면 좋겠다고 하네요
> 
> 만약 더 해보고 싶다면 [여기](https://nomadcoders.co/nomadcoin)를 참조하면 될 것 같구요
> 
> 또한 TS 프로젝트를 만들 때 생산성을 높이는 방법에 대해서도 알아봅시다
> 
> 지금의 방식은 효율적이지는 않습니다
> package.json을 보면 항상 build script를 실행한 다음
> node로 실행하고 있기 때문이구요
> 
> 일단 start script를 새로 만들어 줍시다
> 
> node dist/index.js를 넣어주면 되겠구요
> 
> 아무튼 뭐 하나 하는데 build 후 start를 계속 해줘야 하니 좀 불편한 감이 없지 않아 있구요
> 
> 그래서 개발 의존성으로 다음과 같은 라이브러리를 설치해봅시다
> 
> ```bash
> npm install --D ts-node
> ```
> 
> 이러면 TS 코드를 빌드할 필요 없이 ts-node가 바로 실행해주구요
> 
> 다음 script를 scripts에 넣어주면 됩니다
> 
> ```json
> "dev": "npx ts-node src/index"
> ```
> 
> ![[image 150.png]]
> 
> ???
> 
> AI가 말하기로는 요즘에는 Node.js에서 자체적으로 .ts 파일을 읽고 실행하려는 기능이 추가되었는데
> 무언가 이상하다고 하구요
> 
> tsx를 사용하는게 차라리 더 좋다고 하네요
> 흐음
> 
> ```bash
> npm uninstall ts-node
> npm install tsx
> ```
> 
> ```json
> "dev": "npx tsx src/index"
> ```
> 
> 이렇게 하면 잘 실행이 되구요
> 아주좋았어
> 
> 그리고 nodemon을 설치하면 자동 refresh를 해주어 개발할 때 매우 편하니 같이 설치해봅시다
> 
> ```bash
> npm install nodemon
> ```
> 
> dev를 다음과 같이 교체합시다
> 
> ```json
> "dev": "npx nodemon"
> ```
> 
> 실시간으로 배웠는데
> nodemon.json이라는 것이 있다고 하구요
> 
> 안에는 이렇게 채웠습니다
> 
> ```json
> {
>     "watch": ["src"],
>     "ext": "ts",
>     "exec": "tsx src/index.ts"
> }
> ```
> 
> src 디렉터리 아래를 재귀적으로 훑어서 ts 확장자를 지닌 것이 있는지 확인하구요
> 
> 원래는 nodemon --exec tsx src/index.ts라 작성해야 했던 것을
> nodemon 하나로 끝내게 해주는 아주 좋은 설정이구요
> 
> 이제 블록체인을 디자인해봅시다
> 
> 말 그대로 여러 개의 블록이 사슬로 묶인 것이라 하구요
> 
> 블록 안에는 데이터가 들어 있다고 하네요
> 블록체인으로 보호하고픈 데이터가 들어 있습니다
> 
> 그리고 이 블록은 다른 블록과 연결되어 있습니다
> 
> 말 그대로 사슬처럼 연결되어 있음
> ㅇㅇ
> 
> 그리고 그 사슬은 해쉬값이라고 하구요
> 
> Block class를 선언해줍시다
> 
> 그리고 블록에는 어떠한 값이 들어가야 하는가를 정의해줍시다
> 
> ```typescript
> interface BlockShape {
>     
> }
> 
> class Block {
> 
> }
> ```
> 
> 우선 블록에는 이전 해쉬값이 필요합니다
> 당연한 소리구요
> 
> 해쉬값이 사슬이라고 했으니 적어도 이전 사슬을 본인이 기억하고 있어야 합니다
> 
> 그리고 몇 번째 위치에 있는지도 필요하구요
> 
> 데이터도 필요하네요
> 
> 이제 이 interface를 Block이 구현하도록 만듭시다
> 
> 아 맞다
> 
> 다음 해쉬도 필요하구요
> 
> ```typescript
> interface BlockShape {
>     hash:string;
>     prevHash:string;
>     height:number;
>     data:string;
> }
> 
> class Block implements BlockShape {
>     constructor(
>         public prevHash:string,
>         public height:number,
>         public data:string
>     ) {}
> }
> ```
> 
> 근데 이러면 hash 필드를 제대로 구현하고 있지 않구요
> 
> 왜냐하면 hash는 블록의 prevHash, height, data로 계산하기 때문이라 하구요
> 신기한
> 
> 그렇기 때문에 당연하지만
> 본인의 해쉬값은 본인의 고유 서명과 같다고 하구요
> 
> 위에 생성자로 초기화되지 않는 public 필드 hash를 선언해줍시다
> 
> 그리고 static 메서드를 이용하여 만들어줄 것이라고 하네요
> 
> 아무튼
> 
> static 메서드 calcHash를 만들어야 하구요
> prevHash와 height, data를 입력값으로 받아 새로운 hash를 출력하도록 해야 합니다
> 
> hash 계산은 라이브러리 중 하나인 crypto를 활용할 예정이구요
> 
> 근데 npm install crypto를 설치했더니 node의 타입 정의 파일이 필요하다고 하구요
> 
> 같이 설치해줍시다
> 
> ```bash
> npm install -D @types/node
> ```
> 
> 그러면서 조금 더 자세하게 파보면 좋을 것 같구요

> [!note]+ # #5.6 DefinitelyTyped
> GitHub에는 DefinitelyTyped라는 아주 큰 레포지터리가 존재합니다
> 
> [https://github.com/Definitelytyped/DefinitelyTyped](https://github.com/Definitelytyped/DefinitelyTyped)
> 
> 들어가보면 types라는 디렉터리가 존재하구요
> 
> 우리는 저기에서 타입을 다 가지고 있던 것이었습니다
> 이러언
> 
> 여러 사람들이 참여하는 오픈소스 프로젝트이니 참여해볼 가치가 있을 것 같구요
> 
> 그래서 드디어 hash를 만들어보다
> 
> ```typescript
> import crypto from "crypto";
> 
> interface BlockShape {
>     hash:string;
>     prevHash:string;
>     height:number;
>     data:string;
> }
> 
> class Block implements BlockShape {
>     public hash:string;
> 
>     constructor(
>         public prevHash:string,
>         public height:number,
>         public data:string
>     ) {
>         this.hash = Block.calcHash(prevHash, height, data);
>     }
> 
>     static calcHash(prevHash:string, height:number, data:string):string {
>         const toHash = `${prevHash}${height}${data}`;
>         return crypto.createHash("sha256")
>             .update(toHash)
>             .digest("hex");
>     }
> }
> ```
> 
> sha256이라는 알고리즘으로 해쉬를 만들겠다고 넘겨주는 것이구요
> update에 3개를 대충 이어 붙인 toHash를 집어 넣어 계산하도록 한 후
> digest에서 hex 형태로 내보내라는 소리입니다
> 호오
> 
> ![[image 151.png]]
> 
> 그렇다고 하네요

> [!note]+ # #5.7 Chain
> 이제 드디어 본격적으로 이어볼 시간이구요
> 
> BlockChain class를 만들어 봅시다
> 
> private 필드 blocks는 Block[]형이구요
> public 메서드 addBlock은 data:string을 받아 직접 생성
> 뭐 그러하게 구현해보면
> 
> ```typescript
> class BlockChain {
>     private blocks:Block[];
> 
>     constructor() {
>         this.blocks = [];
>     }
> 
>     private getPrevHash():string {
>         const block = this.blocks[Math.max(this.blocks.length - 1, 0)];
>         return block ? block.hash : "";
>     }
> 
>     public addBlock(data:string):void {
>         const block = new Block(this.getPrevHash(), this.blocks.length + 1, data);
>         this.blocks.push(block);
>     }
> }
> ```
> 
> 다음과 같아지구요
> 
> 생성해서 addBlock을 몇 번 날린 후 임의로 printBlocks 메서드를 추가해 테스트하면
> 
> ![[image 152.png]]
> 
> 아주좋았어

> [!note]+ # #5.8 Conclusions
> TS 공식 문서를 읽을 수 있다면 읽어보는 편이 아주 좋구요
> 
> 블록체인 등에 관심이 있다면 여기를
> 
> [노마드 코인 – 노마드 코더 Nomad Coders](https://nomadcoders.co/nomadcoin)
> 
> 뭐
> 그러합니다
> 
> 이러언