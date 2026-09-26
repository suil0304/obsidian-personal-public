> [!note]+ # #4.0 Props
> 이번에는 직접 Props를 받는 컴포넌트를 만들어볼 예정이구요
> 
> 이제는 또 다른 새로운 것을 만들어 봅시다
> 
> Props가 도대체 왜 중요한가 등은 다 말할 수 없을 정도이구요
> 그렇잖아요
> 
> 재사용성이 증가하며
> 유지보수하기에도 좋은 코드가 나옵니다
> ㅇㅇ
> 
> ```javascript
> function Btn(props) {
>     return (
>         <button>{props.children}</button>
>     );
> }
> 
> function App() {
>     return (
>         <>
>             <Btn>
>                 Change
>             </Btn>
>             <Btn>
>                 Check
>             </Btn>
>         </>
>     );
> }
> ```
> 
> 그래서 위와 같구요
> 
> 이게 또
> 매개변수에서도 구조 분해 할당 비슷한게 됩니다
> 
> ```javascript
> function Btn({ children }) {
>     return (
>         <button>{children}</button>
>     );
> }
> ```
> 
> 이렇게 변경해도 되구요

> [!note]+ # #4.1 Memo
> Props가 받을 수 있는 값
> 
> 네
> {}로 하여 JSX에서 받을 수 있는 Expression 전부 받을 수 있습니다
> 이러언
> 
> 하지만???
> 
> 커스텀 Props는 당연하게도 React가 자동 설정하지 못 하는 것이기 때문에
> 
> onClick 등을 넣는다고 해서
> Event Listener가 설정되는 것은 전혀 아닙니다
> 
> ```javascript
> function App() {
>     return (
>         <>
>             <Btn onClick={() => {
> 		            console.log("clicked!");
>             }}>
>                 Change
>             </Btn>
>             <Btn>
>                 Check
>             </Btn>
>         </>
>     );
> }
> ```
> 
> onClick을 정녕 Event Listener로 사용하고자 한다면
> Btn 컴포넌트의 button 요소에 직접 연결해주어야 하구요
> 
> Props를 사용하면
> 
> 그래서
> 부모 컴포넌트가 자식 컴포넌트에 무언가를 주입시키는 패턴이 가능해지구요
> 
> 부모는 가만히 있는데
> 자식에서 부모의 값을 변경해주는 등의 행동이 가능해진다는 것입니다
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function Btn(props) {
>         console.log(props.children + " was reloaded");
>         return (
>             <button onClick={props.onClick}>{props.children}</button>
>         );
>     }
> 
>     function App() {
>         const [text, setText] = React.useState("Change");
>         
>         const handleChangeButtonClick = () => {
>             setText("Changed!");
>         };
> 
>         return (
>             <>
>                 <Btn onClick={handleChangeButtonClick}>
>                     {text}
>                 </Btn>
>                 <Btn>
>                     Check
>                 </Btn>
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> ![[image 122.png]]
> 
> ?
> 
> 같은 부모라고 App 재실행되면서
> 저 Check Btn도 다시 그려지나 봅니다
> 
> React는 최적화 함수를 많이 지원해주기 때문에
> 다음을 사용하다
> 
> ## React.memo
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function Btn(props) {
>         console.log(props.children + " was reloaded");
>         return (
>             <button onClick={props.onClick}>{props.children}</button>
>         );
>     }
> 
>     const MemorizedBtn = React.memo(Btn);
>     function App() {
>         const [text, setText] = React.useState("Change");
>         
>         const handleChangeButtonClick = () => {
>             setText("Changed!");
>         };
> 
>         return (
>             <>
>                 <MemorizedBtn onClick={handleChangeButtonClick}>
>                     {text}
>                 </MemorizedBtn>
>                 <MemorizedBtn>
>                     Check
>                 </MemorizedBtn>
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> React.memo를 사용하면 컴포넌트를 메모라이즈하기 때문에
> 고정이 됩니다
> 
> ![[image 123.png]]

> [!note]+ # #4.2 Prop Types
> prop-types라는 라이브러리가 존재하구요
> 
> 이것은 prop이 무슨 타입으로 받고 있는지
> 그러한 것들을 검사해주는 역할을 할 수 있구요
> 
> ```html
> <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
> <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
> <script src="https://unpkg.com/prop-types@15.7.2/prop-types.min.js"></script>
> <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function Btn(props) {
>         console.log(props.children + " was reloaded");
>         return (
>             <button onClick={props.onClick}>{props.children}</button>
>         );
>     }
> 
>     Btn.propTypes = {
>         children: PropTypes.optionalNode,
>         onClick: PropTypes.optionalFunction
>     };
> 
>     const MemorizedBtn = React.memo(Btn);
>     function App() {
>         const [text, setText] = React.useState("Change");
>         
>         const handleChangeButtonClick = () => {
>             setText("Changed!");
>         };
> 
>         return (
>             <>
>                 <MemorizedBtn onClick={handleChangeButtonClick}>
>                     {text}
>                 </MemorizedBtn>
>                 <MemorizedBtn>
>                     Check
>                 </MemorizedBtn>
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> ```html
> <script src="https://unpkg.com/prop-types@15.7.2/prop-types.min.js"></script>
> ```
> 
> 이렇게 설치한 다음
> 
> ```javascript
> Btn.propTypes = {
>     children: PropTypes.optionalNode,
>     onClick: PropTypes.optionalFunction
> };
> ```
> 
> 이렇게 설정해주면
> 
> 나중에 props의 값이 잘못되어 버렸을 때 검사하기 좋습니다
> 이러언

> [!note]+ # #4.3 Recap
> 다시 돌아보는 시간
> 
> prop-types는 솔직히 TS로 type 명시해서 사용하는게 더 좋다고 생각합니다
> 이러언
> 씨