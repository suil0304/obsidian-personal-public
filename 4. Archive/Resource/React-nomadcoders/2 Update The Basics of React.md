> [!note]+ # #2.0 Introduction
> 처음부터 배워볼 것이구요
> 
> React가 우리를 위해 해결해주는 문제가 무엇인지부터 이해하고 가봅시다
> 
> 그렇잖아요
> 기술은 도구를 고치기 위해 만들어지고
> 
> 이 기술이 고치려 하는 문제가 무엇인지를 알게 되면
> 이 기술에 대해 더 자세히 이해하게 됩니다
> 당연한 소리구요
> 
> 정리 하나 없이 갑자기 배우면 혼란스러울 뿐이구요
> 
> React는 UI를 인터렉티브하게 만들어줍니다
> 
> 그리고 React를 만든 팀은
> 인터렉티브하게 만들려면 어떠한 것들이 필요한지 알고 있습니다
> 
> 비교를 위해 다음 그것에 바닐라 JS로 코드를 짜볼 예정이구요
> 
> 버튼을 누르면 간단하게 버튼을 누른 횟수를 텍스트에 업데이트하고 싶구요
> 
> 그러려면 HTML로 가야죠???
> 버튼을 만들고
> JS로 가서 그 버튼을 찾아
> addEventListener로 click을 추가하면
> 이제 되네요
> 
> 근데???
> 
> 길고 복잡하잖아요
> 이거
> 
> 그리고 이 문제점은 React도 알고 있습니다
> 
> 그리고 이러한 문제점들에 대하여 지름길 등등을 파두었습니다
> 
> 좋잖아요

> [!note]+ # #2.1 Before React
> #2.0에서 만들겠다 했던 것
> 여기에서 만들 예정이구요
> 
> 원래였다면
> 
> ```html
> <!DOCTYPE html>
> <html lang="ko">
>     <head>
>         <meta charset="UTF-8">
>         <meta name="viewport" content="width=device-width, initial-scale=1.0">
>         <title>비교해보기</title>
>     </head>
>     <body>
>         <button type="button" id="clicker">클릭</button>
>         <p id="counter">0</p>
>         <script type="module" src="./js/counter.js"></script>
>     </body>
> </html>
> ```
> 
> ```javascript
> const clicker = document.querySelector("#clicker");
> const counter = document.querySelector("#counter");
> 
> let clickCount = 0;
> 
> clicker.addEventListener("click", () => {
>     clickCount++;
>     counter.innerText = clickCount;
> });
> ```
> 
> 이렇게 했어야만 했습니다
> 콜백 지옥이라고 부르는 데에는 이유가 있음을 알아야 합니다
> 크아악
> 
> 하지만
> React로 짜면 다르다는 것입니다
> 
> 그래서 React는 무엇을 하면 되는 거죠
> 
> react와 react-dom을 import하면 됩니다
> 이해한
> 
> script의 src로 가져오겠습니다
> 
> ```html
> <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
> <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
> ```
> 
> 이렇게 하면 React가 HTML에 import되는 것이구요
> 
> 여기에서 잠시 끊고 갈 것이구요
> 
> React로 어플리케이션을 시작하는 방법
> 등
> 
> 그렇게 하여 어떻게 이러한 것들을 대체하는가
> 전부 알아볼 예정이구요

> [!note]+ # #2.2 Our First React Element
> 이제 어떻게 React Element를 만드는지 알아볼 예정이구요
> 
> 원래는 HTML에서 전부 명시를 했었잖아요???
> 
> 근데 이렇게 안 하고 React.createElement로 전부 생성해서 넣을 것이구요
> 
> 그래서 일단 어려운 방식으로 먼저 가봅시다
> JSX라는 문법이 있는데
> 
> 일단 그거 사용은 안 하고 만들어볼 거임
> ㅇㅇ
> 
> 그리고 어려운 방식으로 가면 본질을 찾을 수 있지 않을까 싶구요
> 
> ```javascript
> const clicker = React.createElement("button");
> const counter = React.createElement("p");
> ```
> 
> 이렇게 해서 생성을 하긴 했는데
> 이제 어떻게 하면 됨???
> 
> 여기에서 react와 react-dom이 무슨 역할을 하는지 대략적으로 말해봅시다
> 
> react가 인터렉티브한 UI를 만드는 라이브러리구요
> react-dom이 이 React Element를 DOM에 띄우는 라이브러리입니다
> 이러언
> 
> 그래서 ReactDOM의 render를 사용해볼 예정이구요
> 
> ```javascript
> ReactDOM.render(clicker, );
> ```
> 
> 어디다가 배치하죠
> 
> body밖에 없잖아요
> 
> 그래서 보통의 개발자들은 #root를 가진 div만큼은 HTML에 넣어놓습니다
> 이러언
> 
> ```html
> <script>
>     const root = document.querySelector("#root");
> 
>     const clicker = React.createElement("button");
>     const counter = React.createElement("p");
> 
>     ReactDOM.render(clicker, root);
>     ReactDOM.render(counter, root);
> </script>
> ```
> 
> 그래서 root 가져오는 것 만큼은 어쩔 수가 없었구요
> 
> ![[image 16.png]]
> 
> ?
> 
> render하라고 하는 그 순간에 넣은 것만 띄워주나 봅니다
> 오;;;
> 
> 아무튼
> 
> createElement의 두 번째 인자로는 만들 태그의 props를 넣어주면 되구요
> 
> 일단
> render된 p로 해봅시다
> 
> ```javascript
> const counter = React.createElement("p", {
>     id: "counter",
>     children: "0"
> });
> ```
> 
> ![[image 17.png]]
> 
> 아주좋았어
> 
> 근데 사실 세 번째 인자가 만들어질 태그의 내용을 넣는 곳이었구요
> 뭐한 거지
> 
> ```javascript
> const counter = React.createElement("p", {
>     id: "counter"
> }, "0");
> ```
> 
> ![[image 18.png]]
> 
> 똑같구요
> 
> 아무튼
> 아주좋았어
> 
> 이러한 것들을 통해 더 확실하게 깨달을 수 있는 것입니다
> 
> React는 JS로 시작해서 JS로 끝나는군요
> interesting
> 
> 그래서 Event는 어떻게 넣죠

> [!note]+ # #2.3 Events in React
> React에서 Event 넣는 법을 알아봅시다
> 
> 그 전에
> props는 지금 넣는게 의미가 없으니 다 null로 변경해줍시다
> 
> ```html
> <script>
>     const root = document.querySelector("#root");
> 
>     const clicker = React.createElement("button", null, "클릭");
>     const counter = React.createElement("p", null, "0");
> 
>     // ReactDOM.render(counter, root);
> </script>
> ```
> 
> 두 가지 전부 렌더링하려면 다음을 해야 하구요
> 
> div를 만들 수도 있고
> React.Fragment를 만들 수도 있는 거고
> 그건 저희들의 선택인 것입니다
> 
> ```html
> <script>
>     const root = document.querySelector("#root");
> 
>     const clicker = React.createElement("button", null, "클릭");
>     const counter = React.createElement("p", null, "0");
> 
>     const container = React.createElement(React.Fragment, null, [clicker, counter])
> 
>     ReactDOM.render(container, root);
> </script>
> ```
> 
> ![[image 19.png]]
> 
> 됐구요
> 
> 여기에서 React.Fragment는 React의 최상위는 항상 한 요소만 있어야 한다 규칙 때문에
> div 등이 묶을 때마다 계속 배치되는 현상을 막기 위하여 탄생한 함수구요
> 
> 아무튼 그래서
> 
> event는 on~~으로 camelCase 지키며 넣으면 되구요
> 좋잖아요
> 
> 변경은 뭐
> document.querySelector로 가져와서 하면 되는 건가요
> 이러언
> 
> 근데 이거
> 
> 좀 많이 비효율적이죠???
> 다른 방식 배울 것이구요

> [!note]+ # #2.4 Recap
> 그 전에 무엇을 배웠나 다시 생각해볼 시간이구요
> 
> 쉽잖아요
> 
> 넘기다

> [!note]+ # #2.5 JSX
> React.createElement를 대체하는 방법을 알아봅시다
> 
> 바로 JSX 문법이구요
> JSX 문법 이러니 어렵게 느껴질 수도 있으나
> 
> 이거 JS 안에 HTML 문법 끌고 오는 그것이구요
> 
> HTML의 script 태그 안에서 JS를 사용할 수 있었던 것처럼
> JS에서 HTML 문법을 사용 가능해진다는 소리입니다
> 
> 싹 다 지우고
> 다시 해봅시다
> 
> ```html
> <script>
>     const root = document.querySelector("#root");
> 
>     const counter = <p>0</p>;
> 
>     let clickCount = 0;
> 
>     const clicker = (
>         <button
>             onClick={() => {
>                 console.log("클릭됨");
>             }}
>         >
>             클릭
>         </button>
>     );
> 
>     const container = (
>         <>
>             {counter}
>             {clicker}
>         </>
>     );
> 
>     ReactDOM.render(container, root);
> </script>
> ```
> 
> 네
> 
> 엄청 깔끔해졌죠?
> 
> 그런데 정작
> HTML은 <>가 무엇을 뜻하는지 몰라 에러를 내뱉고 있구요
> 
> 저기에서 저 <>가 실제로는 React.createElement와 같거든요???
> 
> 저걸 저렇게 변환해주는 무언가를 설치해야 합니다
> 
> Babel을 사용해볼 것이구요
> 
> ```html
> <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
> ```
> 
> ![[image 20.png]]
> 
> ?
> 
> 여전히 에러가 나는
> 
> 다음을 추가하여 babel이 변환을 도울 수 있도록 하다
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     const counter = <p>0</p>;
> 
>     let clickCount = 0;
> 
>     const clicker = (
>         <button
>             onClick={() => {
>                 console.log("클릭됨");
>             }}
>         >
>             클릭
>         </button>
>     );
> 
>     const container = (
>         <>
>             {counter}
>             {clicker}
>         </>
>     );
> 
>     ReactDOM.render(container, root);
> </script>
> ```
> 
> 좋은

> [!note]+ # #2.6 JSX part Two
> 조금 더 가봅시다
> 
> 함수가 JSX를 반환하게 한다면???
> 
> 재사용 가능해지니 매우 맛있어질 것이구요
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function Counter() {
>         return (
>             <p>0</p>
>         );
>     }
> 
>     function Clicker() {
>         return (
>             <button
>                 onClick={() => {
>                     console.log("클릭됨");
>                 }}
>             >
>                 클릭
>             </button>
>         );
>     }
> 
>     const container = (
>         <>
>             <Clicker />
>             <Counter />
>         </>
>     );
> 
>     ReactDOM.render(container, root);
> </script>
> ```
> 
> JSX에서는 함수가 PascalCase를 취한다면 커스텀 태그로써 사용할 수 있도록 만들어져 있구요
> 
> 코드가 아름다워 보일 지경입니다
> 좋네요
> 
> 그래서 태그 형태로 저렇게 넣는다면
> 
> 실제로는 해당 함수를 호출한 다음에
> 나오는 React Element를 가지고 이러언 이러언
> 
> 그래서 이러한 것들을 컴포넌트라 부르구요
> 
> 컴포넌트는 PascalCase를 따라주면 좋을 것이구요