> [!note]+ # #2.0 Your First JS Project
> JS를 다루는 법: 브라우저의 콘솔을 이용하다
> 
> ![[image 60.png]]
> 
> 이런 느낌이구요
> 
> 노마드코더에 에러가 좀 많이 나고 있구요
> 
> > [!note]+ ## window.alert()
> > 말 그대로 알림이구요
> > 
> > ```javascript
> > window.alert("like this");
> > ```
> > 
> > ![[image 61.png]]
> > 
> > 그러하구요
> 
> > [!note]+ ## 1+1
> > ![[image 62.png]]
> > 
> > 연산 가능하구요
> > 
> > 대략적으로 추론해봤을 때
> > 
> > eval 함수로 직접 돌리는 것 같구요
> > 흐음
> 
> > [!note]+ ## ReferenceError
> > ![[image 63.png]]
> > 
> > idk를 입력했을 때
> > idk는 정의되지 않았기 때문에 아예 에러가 뜨고 있구요
> > 
> > 다만 밑에다 정의해두고 위에서 console.log로 출력
> > 또는 var variable;
> > 이렇게 하면 undefined가 나올 것 같구요
> 
> 그래서 console에 긴 것을 하나 하나 일회용으로 작성해야만 하다???
> 그것은 아닌
> 고노야로
> 
> index.html과 /css/style.css, /js/app.js를 만들다
> 
> ```css
> /* /css/style.css */
> body {
>     background-color: beige;
> }
> ```
> 
> ```javascript
> // /js/app.js
> console.log("like this");
> ```
> 
> ```html
> <!-- index.html -->
> <!DOCTYPE html>
> <html lang="ko">
>     <head>
>         <meta charset="UTF-8">
>         <meta name="viewport" content="width=device-width, initial-scale=1.0">
>         <title>Momentum Clone Coding</title>
>         <link rel="stylesheet" href="./css/style.css">
>     </head>
>     <body>
>         <script src="./js/app.js"></script>
>     </body>
> </html>
> ```
> 
> 이렇게 연결하여 사용하다
> 
> ![[image 64.png]]
> 
> 간단하죠???

> [!note]+ # #2.1 Basic Data Types
> 프로그래밍에 있어 가장 기본적인 2가지 타입을 알아봅시다
> 
> ```javascript
> 2+2;
> ```
> 
> 이렇게 했을 때 연산이 가능한 이유는 JS가 이것이 number 타입임을 알고 있어서구요
> 
> 다른 것임을 강조하는 이유가 무엇인지 대략적으로 궁금해지는데
> 
> JS에서는 정수나 실수나 둘 다 같은 타입으로 담아버리는 미친 짓을 하였기 때문에
> 둘이 막 그렇게 별반 달라지지 않아져버렸구요
> 
> number라는 하나의 책임으로 둘이 묶여버리니 메서드도 동일한 것을 사용하고 사용자가 걸러내야만 하는 어디서 나온 발상일지 모를 무언가가 되었습니다
> 이러언
> 
> 그래서 어떻게 Hello라는 문자열을 출력시키다???
> 
> 간단하잖아용
> 
> ```javascript
> "Hello";
> ```
> 
> ![[image 65.png]]
> 
> 이러언
> CORS가 떠버린 것 같구요
> 
> 그것보다 간단하잖아용
> 
> “ “를 사용하여 해당 문자가 문자열임을 증명하다
> 
> 쉬운

> [!note]+ # #2.2 Variables
> 다음은 변수구요
> 
> Clean Code
> 우리들의 영원한 성서에서도 나오는 말입니다
> 
> 매직 넘버는 일단 제거하고 봐야 한다는 사실을 말이죠
> 
> ```javascript
> console.log(5 + 2);
> console.log(5 * 2);
> console.log(5 / 2);
> ```
> 
> 이런 아주 간단한 예에 대하여 적용 가능한
> 
> 저거 5를 6을 변경하거나 할 때 어떻게 변경할 거에요
> 
> 하나 하나 다 변경하고 있을 시간에 이렇게 하는 것이 훨씬 더 효율적이고 당장에 귀찮을지 몰라도 유지보수하기 좋은 코드가 탄생한다는 소리입니다
> 
> ```javascript
> const FIVE = 5;
> const TWO = 2;
> 
> console.log(FIVE + TWO);
> console.log(FIVE * TWO);
> console.log(FIVE / TWO);
> ```
> 
> 아예 변수 상수 자체를 변경해야 하는 순간이 오지 않는 이상 값 2개만 바꿔도 저 6개를 다 바꿀 수 있다는 소리가 되는 것입니다
> 
> 이 얼마나 훌륭해요
> 
> 변수 또는 상수 이름 짓는 법은 각각 다릅니다
> 
> 대략적으로 표를 나눠볼 수 있겠죠???
> 
> 그러나 그렇게 하기는 귀찮은
> 
> 대략 JS는 변수 이름 지을 때 camelCase로 짓는다는 점만 알아두면 됩니다

> [!note]+ # #2.3 const and let
> const와 let의 차이는 무엇일까용
> 
> const는 constant에서 왔습니다
> 
> 네
> 상수라는 뜻이죠???
> 
> 하지만 let은 변수를 선언할 때 사용합니다
> 
> var라는 키워드도 있는데
> 얘는 전역으로 변수 선언할 때 사용하라고 있는 녀석이고
> 
> let은 블록 범위 변수를 선언할 때 좋습니다
> 애초에 그러라고 새롭게 추가된 예약자인지라

> [!note]+ # #2.4 Booleans
> > [!note]+ boolean
> > 사실상 가장 간단한 데이터 타입이 아닐까 싶구요
> > 
> > 이것은 true와 false만 받습니다
> > 
> > 불 대수가 무엇인지 간단하게만 알고 있어도 이해할 수 있을 것이라 생각합니다
> > 
> > 당연하지만 true와 false는 값이기 때문에 문자열로 써버리면 빡빡이가 되는 것이구요
> > 
> > 세상의 누가 true = true;로 변수를 선언하겠어요
> 
> > [!note]+ null
> > 또한 null이라는 것이 있구요
> > 
> > 이것은 typeof하면 “object”로 잘못 가져오는 에러가 있구요
> > 
> > null이라고 하면 0x00이잖아용???
> > 근데 typeof 맵에 0x00번째가 “object”여서 “object”로 잘못 가져온다 알고 있구요
> > 
> > 아무튼 falsy합니다
> 
> > [!note]+ undefined
> > ```javascript
> > console.log(hoisting);
> > let hoisting = "hoisting";
> > ```
> > 
> > 와 같이 호이스팅으로 끌어 올려지거나
> > 
> > ```javascript
> > let undefinedValue;
> > console.log(undefinedValue);
> > ```
> > 
> > 로 초기화시키지 않으면 볼 수 있는 값이구요
> > 
> > 사실 optional에서 더 자주 볼 수 있지 않나 싶구요
> > 
> > 이것도 falsy합니다
> 
> null과 undefined의 의미를 잘 이해한 상태로 사용해야만 하구요
> 그렇지 않으면 많은 개발자들이 수일을 죽일 예정이구요

> [!note]+ # #2.5 Arrays
> Array는 말 그대로 배열이구요
> 
> 무엇보다 런타임 동적인 JS에서는 무엇이든 담을 수 있구요
> 
> string[]이라거나 number[] 이런 것은 TypeScript나 가서 사용하라 하구요
> 
> 뭐 얘를 들어서 dayOfWeeks라고 하자면
> 
> ```javascript
> const dayOfWeeks = ["월", "화", "수", "목", "금", "토", "일"];
> ```
> 
> 이렇게 하지
> 
> ```javascript
> const dayOfWeeks = "월" + "화" + "수" + "목" + "금" + "토" + "일";
> ```
> 
> 이렇게 하는 인간은 특히 드물잖아용
> 
> 문자열 포맷을 하라고 해도
> 
> ```javascript
> dayOfWeeks.join("");
> ```
> 
> 이렇게 하면 되는데
> 
> 굳이죠
> ㅇㅇ
> 
> ```javascript
> const anyArray = [0, 0.0, "string", false, null, undefined, {}, () => {}];
> ```
> 
> 전부 다 담을 수 있구요
> 이러언
> 
> 당연하게도 JS는 0부터 인덱스가 시작하기 때문에
> 어디 Lua에서나 볼 법한
> 1부터 시작하는 인덱스를 사용해버렸다간???
> 바로 터지기 쉽지는 않고
> undefined를 볼 확률이 높아지겠죠???
> 
> 또 array에 요소를 추가할 수 있구요
> 
> ```javascript
> anyArray.push("Another One");
> ```

> [!note]+ # #2.6 Objects
> 객체구요
> 
> JS에서 객체란 Python의 Dictionary 개념이라 생각할 수도 있을 것 같구요
> 
> 왜냐하면
> 
> ```javascript
> const object = {
> 	num: 1,
> 	str: "string"
> };
> 
> console.log(object["num"]); // result: 1
> ```
> 
> 1을 출력하구요
> 
> 사실상 당연한 소리인게
> 저거 자체가 거의 JSON이라
> 
> ```javascript
> const object = {
> 	"num": 1,
> 	"str": "string"
> };
> ```
> 
> 이렇게 해도 동작하구요
> 
> 다만 조금 더 전문적으로 맵 개념을 사용해보고자 한다면???
> Map이라는 클래스를 꺼내서 넣고 내려
> 
> 또한 값 수정 및 넣기도 가능하구요
> 
> ```javascript
> const object = {
>     "null": null
> };
> 
> object["null"] = false;
> object["plus"] = true;
> 
> console.log(object["plus"]);
> ```
> 
> 이딴 코드가 실제로 문제 없이 동작하구요

> [!note]+ # #2.7 Functions part One
> 그러면 함수는 뭔데
> 
> 함수는 마법의 상자입니다
> 
> 수학에서는 함수를 x에 대하여 y의 값이 하나만 나오는 경우로 한정 지었죠???
> 
> 하지만 프로그래밍에서의 함수는 전혀 다릅니다
> 
> x를 넣었는데 여러 개가 return될 수도 있구요
> x만 넣는 것이 아니라 x, y, z에 대하여 한 가지를 return할 수도 있는 것이구요
> 심지어는 아예 값이 안 들어와도 return할 수 있고
> 아무 것도 안 들어오고 아무 것도 return을 안 하는 경우도 존재할 수 있구요
> 
> 아무튼 대단한 친구라고 생각하는게 좋을 것 같다는게 제 생각이구요
> 
> 함수의 대표적인 기능 중 하나는 코드 중복 최소화가 있을 것 같구요
> 
> ```javascript
> function hello(name) {
>   console.log("Hello, " + name + "!");
> }
> ```
> 
> 이렇게 했을 때
> 
> ```javascript
> hello("world");
> hello("suil");
> hello("suli");
> hello("hello");
> hello("function");
> hello("thing");
> ```
> 
> 원래 사용자 정의 함수 없었으면
> 
> ```javascript
> console.log("Hello, world!");
> console.log("Hello, suil!");
> console.log("Hello, suli!");
> console.log("Hello, hello!");
> console.log("Hello, function!");
> console.log("Hello, thing!");
> ```
> 
> 가 될 수 있었구요
> 
> 함수 자체가 없었다면
> 출력 과정 모두를 하나 하나 계속 나열했어야만 했을 것이구요
> 
> 많이 쓰는 코드를 줄여주는 아주 고마운 녀석이라고 할 수 있을 것이구요
> 
> 근데 이번 것에 대해서는 매개변수가 안 나와버렸구요
> 
> 매개변수 없이 단순하게
> 
> console.log(”Hello, world!”);를 function으로 묶어 hello로 이름 짓고 호출하는 방법을 알아보는 시간이었던 것 같구요
> 이러언

> [!note]+ # #2.8 Functions part Two
> 이건뭐야
> 
> 위를 참조하길 바라다
> 
> 그래서 object 안에 함수도 넣을 수 있었는데 어떻게 넣음???
> 
> ```javascript
> const object = {
> 	func: function() {
> 		// ...
> 	}
> };
> ```
> 
> 다음과 같구요
> 
> 지금 function 다음에 식별자가 오질 않았는데
> 
> 이것을 익명 함수라 부르다
> 
> JS에서는 함수도 일급 객체이기 때문에 그냥 넘겨버리는게 가능해져버리는
> 
> 아니면 메서드 느낌으로 생성할 수도 있구요
> 
> ```javascript
> const object = {
> 	func() {
> 		// ...
> 	}
> };
> ```
> 
> 어째 function 키워드가 사라지니 괴상하게 보이는데
> 그것은 아쉬운 것임을 알기 바라다

> [!note]+ # #2.9 Recap
> 다시 정리하는 시간
> 
> 사실 쉽잖아요
> 
> 처음 하는 것도 아니고
> 
> 넘겨버리다

> [!note]+ # #2.10 Recap II
> 그래서 배열과 객체, 함수에 대해 다시 정리하는 시간까지 모두 가져보았다면
> 
> 계산기 객체를 만들어보다
> 이러언
> 
> ```javascript
> const caculator = {
>     /**
>      * 둘을 더해보는 어드밴쳐 타임
>      * @param {number} a 
>      * @param {number} b 
>      * @returns {number}
>      */
>     add: function(a, b) {
>         return a + b;
>     },
>     /**
>      * 둘을 빼보는 어드밴쳐 타임
>      * @param {number} a 
>      * @param {number} b 
>      * @returns {number}
>      */
>     sub: function(a, b) {
>         return a - b;
>     },
>     /**
>      * 둘을 곱해보는 어드밴쳐 타임
>      * @param {number} a 
>      * @param {number} b 
>      * @returns {number}
>      */
>     mult: function(a, b) {
>         return a * b;
>     },
>     /**
>      * 둘을 나눠보는 어드밴쳐 타임
>      * @param {number} a 
>      * @param {number} b 
>      * @returns {number}
>      */
>     div: function(a, b) {
>         return a / b;
>     }
> };
> ```
> 
> JSDoc은 JS만 사용할 생각이라면 필수입니다
> 
> 이 거지 같은 런타임 동적에서 살아 남기 위해서는 타입을 명시해야 할 필요가 있음을 알아두기 바랍니다

> [!note]+ # #2.11 Returns
> 아
> 
> 그러고 보니 위에서 console.log로 바로 출력시키는게 아니라 return을 시켜버렸네요
> 
> 네
> 저게 반환값입니다
> 
> 모든 값은 return 가능합니다
> 
> TypeScript로 가면 함수 반환 타입에 never 붙여서 에러를 던질 수 밖에 없도록 강제할 수 있긴 합니다만
> 이러언

> [!note]+ # #2.12 Recap
> return 등등과 관련하여 다시 돌아보기를 해보다
> 
> 쉽잖아용
> 
> 넘기다

> [!note]+ # #2.13 Conditionals
> 조건문이구요
> 
> if는 괄호 안에 든 condition이 truthy하면 본문 실행입니다
> else는 if에 대하여 condition이 falsy하면 대신하여 else 본문 실행입니다
> else-if는 if에 대하여 condition이 falsy할 때 else-if의 괄호 안에 든 condition이 truthy하면 본문 실행입니다
> 
> > [!note]+ ## window.prompt()
> > window.prompt는 브라우저에서 입력을 받아오는 함수구요
> > 
> > 첫 번째는 받아올 때 무엇을 물어보고 받아올지구요
> > 두 번째는 값이 들어오지 아니할 때 가져올 default구요
> > 
> > 둘 다 optional이라고 하구요
> 
> 받아온 것을 형변환하겠다는 소리였구요
> 이러언
> 
> 세상에 있는 모든 프로그래밍 언어가 그러하듯이
> 당연하게도 모든 유저가 넣은 것은 string으로 받아오구요
> 
> ```javascript
> const foo = window.prompt();
> 
> console.log(typeof foo); // result: "string"
> ```
> 
> 그렇다는 것은 Number.parseInt로 받아와야만 한다는 소리겠구요
> 이러언

> [!note]+ # #2.14 Conditionals part Two
> 근데 문제가
> 
> 어떤 이상한 인간이 숫자 집어 넣으라고 하는 곳에 문자열을 내려
> 이러면 안 되는 거잖아용???
> 
> 아주 당연한 상식으로 숫자가 아닌 문자로만 이루어진 문자열을 parseInt에 넣으면 ValueError라던가 그런 것이 뜰 것 같지만
> 
> 이 괴상한 언어는 일단 돌아가야 브라우저가 멈추지 않기 때문에
> NaN이라는 number형의 값이 나옵니다
> 
> *crys* why…
> 
> NaN이라고 하는 것은 Not a Number의 줄임말이구요
> 
> IEEE 754에 표준으로 정의된 Float의 특수 value로 매칭된 무언가라 알고 있구요
> 
> 아무튼 NaN은 자기 자신과 비교를 하면 false가 나오는 유일한 값입니다
> 이러언
> 
> 그래서 Number.isNaN으로 찾아야만 하다
> 
> ```javascript
> const age = Number.parseInt(window.prompt("How old are you?") ?? "");
> console.log(Number.isNaN(age));
> 
> if(!Number.isNaN(age)) {
>     console.log("Hello");
> }
> else {
>     console.error("what?");
> }
> ```
> 
> 이러한 방식으로 찾을 수 있었구요

> [!note]+ # #2.15 Conditional part Three
> 그러면 2개 이상의 condition을 어떻게 한 if 안에 넣다???
> 
> 가독성 따지면 아래가 맞지만
> *함수 안에서의 조기 리턴*
> 
> ```javascript
> if(isNaN(age)) {
> 	return;
> }
> 
> if(age <= 18) {
> 	console.log("you cannot drink beer.");
> 	return;
> }
> 
> console.log("you can drink beer.");
> ```
> 
> 근데 이러면 길어지잖아용
> 물론 저는 위의 형태를 더 좋아하긴 합니다만
> 
> ```javascript
> if(!isNaN(age) && age > 18) {
> 	console.log("you can drink beer.");
> 	return;
> }
> 
> console.log("you cannot drink beer.");
> ```
> 
> 한 if로 줄여 서술할 수 있게 되긴 합니다
> 이러언
> 
> 여기에서 정리하다
> 
> &&는 앞과 뒤의 값 모두 true일 때 true가 나오는 논리 and 연산자입니다
> ||는 앞과 뒤의 값 둘 중 하나가 true가 나오면 true가 나오는 논리 or 연산자입니다
> !는 그 바로 뒤의 값을 뒤집습니다
> 이러언

> [!note]+ # #2.16 Recap
> 다시 돌아보면서 심화에 들어가 봅시다
> 
> >이라던가 < 이런 비교는 수학에서도 많이 해봤잖아용???
> 
> 그러면 같거나 크다
> 같거나 작다
> 이러한 연산자는 $\ge$나 $\le$를 직접 특수문자에서 찾아 써야 하는 건 아니잖아용
> 
> >=와 <=를 참조하다
> 이러언
> 
> ≥와 ≤의 의미와 같구요 당연히
> 
> 또한 ==과 ===가 있는데
> 
> ==는 JS가 자동으로 형변환하면서 맞는지 확인하고
> ===는 타입까지 확인하면서 맞는지 확인하는 연산자입니다
> 이러언
> 
> !=와 !==도 비슷한 역할을 하겠죠???
> !는 위에서 not의 역할을 맡는다 이야기했으니
> 자연스럽게 같지 않는가를 물어보는 고노야로인
> ㅇㅇ
> 
> 또한 연산자 우선순위를 고려하여
> ()를 씌워 더 복잡한 조건을 추가 가능하나
> 추천하지는 않구요