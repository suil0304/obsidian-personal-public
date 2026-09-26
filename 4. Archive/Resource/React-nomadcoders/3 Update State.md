> [!note]+ # #3.0 Understanding State
> counter에 숫자 업데이트하는 건 어떻게 하는 거죠
> 
> 음
> 어
> 
> 그래서 State의 개념에 대하여 알아봅시다
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function Container() {
>         return (
>             <>
>                 <p>0</p>
>                 <button type="button">클릭</button>
>             </>
>         )
>     }
> 
>     ReactDOM.render(<Container />, root);
> </script>
> ```
> 
> 우선 index.html의 script 부분을 다음과 같이 변경해주고
> 
> 불편하고 안 좋은 지향해서는 안 되는 방식으로 우선 구현해봅시다
> 
> JSX 문법 안에서 {}를 사용하면 외부 변수 등을 가져올 수 있구요
> 또는 JSX에서 표현 불가능한 것들을 {}를 열어 JS Expression을 사용할 수 있습니다
> 이러언
> 
> 그렇게 button onClick Event Prop에 clickCount 변수를 ++하는 함수를 추가하면
> 
> ![[image 74.png]]
> 
> 똑같습니다
> 
> 그래서 ReactDOM.render를 계속 호출시키면 될 것 같구요
> 
> 하지만 이렇게 render 함수를 개발자가 알고 있어야 하고
> 심지어 수동적으로 계속해서 사용해야 한다는 그것부터가 마음에 들지는 않구요

> [!note]+ # #3.1 setState part One
> 그래서 useState 훅을 사용해야 하는 것이구요
> 
> ```javascript
> const state = React.useState();
> ```
> 
> console.log로 출력했을 때
> 
> ![[image 75.png]]
> 
> 흐음
> 
> Array를 반환하네요
> 
> 뒤의 function을 사용하면 값을 설정할 수 있구요
> 
> 앞의 값은 현재의 값입니다
> 
> ```javascript
> const state = React.useState(0);
> ```
> 
> 이렇게 초기값을 쥐어줄 수 있구요
> 
> 뒤의 function으로 값을 변경하면
> React가 자동으로 다시 그려줍니다
> 
> 이러언
> 
> 그래서 state[0]의 형태로 값을 가져올 수 있겠구요
> state[1]의 형태로 호출하여 값을 변경할 수 있겠네요
> 
> 근데 array index 접근은 좀 많이 더러운 것 같구요
> 
> ```javascript
> const [state, setState] = React.useState(0);
> ```
> 
> 이렇게 구조 분해 할당을 이용하면 조금 더 맛있게 사용할 수 있겠네요
> 끼얏호우

> [!note]+ # #3.2 setState part Two
> 이제 구조 분해 할당으로 가져온 state를 태그에 연결하면 됩니다
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function App() {
>         const [clickCount, setClickCount] = React.useState(0);
> 
>         const countUp = () => {
>             setClickCount((prev) => prev + 1);
>         };
>         
>         return (
>             <>
>                 <p>{clickCount}</p>
>                 <button
>                     type="button"
>                     onClick={countUp}
>                 >
>                     클릭
>                 </button>
>             </>
>         )
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> ![[image 76.png]]
> 
> ![[image 77.png]]
> 
> 잘 되네용
> 이-히히

> [!note]+ # #3.3 Recap
> 쉽잖아용
> 
> 넘기다

> [!note]+ # #3.4 State Functions
> 사실 위에서 (prev) => prev + 1의 형태로 화살표 함수를 넘겼었는데
> 
> 이거는 setState가 기본적으로 다음과 같은 형태를 지니고 있기 때문이구요
> 
> ```typescript
> function setState<T>(value:T):void;
> function setState<T>(value:(prev:T) => T):void;
> ```
> 
> function을 넘기게 되면 prev로 이전 값을 React가 넘겨주기 때문에
> 이렇게 clickCount를 늘리면 좋을 것이구요

> [!note]+ # #3.5 Inputs and State
> 단위 변환 프로그램 같은 것을 만들어볼 예정이구요
> 
> 그래서 input의 onChange에 handler를 달아서 값을 가져오면 좋을 것 같네용
> 
> Event를 console.log로 출력시키면
> 기존의 Event가 아닌
> 
> ![[image 78.png]]
> 
> 이렇게 나오는데
> 
> React는 이벤트를 최적화시킨다고 하네요
> 이러언
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function App() {
>         const [minute, setMinute] = React.useState(0);
>         const [hour, setHour] = React.useState(0);
> 
>         const handleChange = (event) => {
>             setMinute(Number.parseInt(event.target.valueAsNumber));
>         };
> 
>         return (
>             <>
>                 <h1>Super Converter</h1>
>                 <label htmlFor="minute">Minutes</label>
>                 <input
>                     id="minute"
>                     type="number"
>                     placeholder="Minutes"
>                     value={minute}
>                     onChange={handleChange}
>                 />
>                 <h2>You want to convert {minute}</h2>
>                 <label htmlFor="hour">Hours</label>
>                 <input
>                     id="hour"
>                     type="number"
>                     placeholder="Hours"
>                     value={hour}
>                 />
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> 이렇게 할 수 있을 것 같구요
> 아주좋았어
> 
> 이제 minute를 받아 hour를 계산하도록 하면 되겠네요

> [!note]+ # #3.6 State Practice part One
> 복습 좀 해봅시다
> 
> 그러면서 해줘야 할 것들이 있었는데
> 
> 이미 위에서 다 처리를 해버렸기 때문에
> 할 것이 없네요
> 이러언
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function App() {
>         const [minute, setMinute] = React.useState(0);
>         const [hour, setHour] = React.useState(0);
> 
>         const handleMinuteChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setMinute(value);
>             setHour(value / 60);
>         };
> 
>         const handleHourChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setHour(value);
>             setMinute(value * 60);
>         };
> 
>         return (
>             <>
>                 <h1>Super Converter</h1>
>                 <div>
>                     <label htmlFor="minute">Minutes</label>
>                     <input
>                         id="minute"
>                         type="number"
>                         placeholder="Minutes"
>                         value={minute}
>                         onChange={handleMinuteChange}
>                     />
>                 </div>
>                 <div>
>                     <label htmlFor="hour">Hours</label>
>                     <input
>                         id="hour"
>                         type="number"
>                         placeholder="Hours"
>                         value={hour}
>                         onChange={handleHourChange}
>                     />
>                 </div>
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> 이렇게 하여 계산도 완성했구요
> 
> reset도 만들어 주면 좋을 것 같구요
> 
> ![[image 79.png]]
> 
> ![[image 80.png]]
> 
> 아주좋았어

> [!note]+ # #3.7 State Practice part Two
> 근데 flip 버튼을 누르면 입력 가능한 input이 바뀌고
> 그러한 방식이었으면 좋겠구요
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function App() {
>         const [minute, setMinute] = React.useState(0);
>         const [hour, setHour] = React.useState(0);
> 
>         const [flip, setFlip] = React.useState(false);
> 
>         const handleMinuteChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setMinute(value);
>             setHour(value / 60);
>         };
> 
>         const handleHourChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setHour(value);
>             setMinute(value * 60);
>         };
> 
>         const handleResetButtonClick = () => {
>             setMinute(0);
>             setHour(0);
>         };
> 
>         const handleFlipButtonClick = () => {
>             setFlip((prev) => !prev);
>         }
> 
>         return (
>             <>
>                 <h1>Super Converter</h1>
>                 <div>
>                     <label htmlFor="minute">Minutes</label>
>                     <input
>                         id="minute"
>                         type="number"
>                         placeholder="Minutes"
>                         value={minute}
>                         onChange={handleMinuteChange}
>                         disabled={flip}
>                     />
>                 </div>
>                 <div>
>                     <label htmlFor="hour">Hours</label>
>                     <input
>                         id="hour"
>                         type="number"
>                         placeholder="Hours"
>                         value={hour}
>                         onChange={handleHourChange}
>                         disabled={!flip}
>                     />
>                 </div>
>                 <button type="button" onClick={handleResetButtonClick}>Reset</button>
>                 <button type="button" onClick={handleFlipButtonClick}>Flip</button>
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> 좋잖아요
> ㅇㅇ
> 
> ![[image 81.png]]
> 
> ![[image 82.png]]
> 
> 아주좋았어
> 
> state를 1개로 변경하는 방법이 존재하나
> 가독성이 떨어진다 느끼기 때문에
> 넘기다
> 
> 아무튼 다음에는 킬로미터와 마일을 계산하는 무언가를 추가한 후 마무리 짓는다고 하구요
> 이러언

> [!note]+ # #3.8 Recap
> 다시 돌아보는 시간
> 
> 쉽잖아요
> 
> state라는게 뭐
> 사실상 당연한 개념을 React에서 전용으로 사용하라 제공해준 것이라
> 쉬워요 그냥

> [!note]+ # #3.9 Final Practice and Recap
> 메뉴를 추가하여 어떤 변환기를 사용할 것인지 설정하도록 할 것이구요
> 
> ```html
> <script type="text/babel">
>     const root = document.querySelector("#root");
> 
>     function MinuteAndHour() {
>         const [minute, setMinute] = React.useState(0);
>         const [hour, setHour] = React.useState(0);
> 
>         const [flip, setFlip] = React.useState(false);
> 
>         const handleMinuteChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setMinute(value);
>             setHour(value / 60);
>         };
> 
>         const handleHourChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setHour(value);
>             setMinute(value * 60);
>         };
> 
>         const handleResetButtonClick = () => {
>             setMinute(0);
>             setHour(0);
>         };
> 
>         const handleFlipButtonClick = () => {
>             setFlip((prev) => !prev);
>         }
> 
>         return (
>             <>
>                 <h2>Minute Thing Converter</h2>
>                 <div>
>                     <label htmlFor="minute">Minutes</label>
>                     <input
>                         id="minute"
>                         type="number"
>                         placeholder="Minutes"
>                         value={minute}
>                         onChange={handleMinuteChange}
>                         disabled={flip}
>                     />
>                 </div>
>                 <div>
>                     <label htmlFor="hour">Hours</label>
>                     <input
>                         id="hour"
>                         type="number"
>                         placeholder="Hours"
>                         value={hour}
>                         onChange={handleHourChange}
>                         disabled={!flip}
>                     />
>                 </div>
>                 <button type="button" onClick={handleResetButtonClick}>Reset</button>
>                 <button type="button" onClick={handleFlipButtonClick}>Flip</button>
>             </>
>         );
>     }
> 
>     function KilometerAndMile() {
>         const [kilometer, setKilometer] = React.useState(0);
>         const [mile, setMile] = React.useState(0);
> 
>         const [flip, setFlip] = React.useState(false);
> 
>         const handleMinuteChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setKilometer(value);
>             setMile(value / 1.609);
>         };
> 
>         const handleHourChange = (event) => {
>             const value = event.target.valueAsNumber;
> 
>             setMile(value);
>             setKilometer(value * 1.609);
>         };
> 
>         const handleResetButtonClick = () => {
>             setKilometer(0);
>             setMile(0);
>         };
> 
>         const handleFlipButtonClick = () => {
>             setFlip((prev) => !prev);
>         }
> 
>         return (
>             <>
>                 <h2>Kilometer Thing Converter</h2>
>                 <div>
>                     <label htmlFor="kilometer">Kilometers</label>
>                     <input
>                         id="kilometer"
>                         type="number"
>                         placeholder="Kilometers"
>                         value={kilometer}
>                         onChange={handleMinuteChange}
>                         disabled={flip}
>                     />
>                 </div>
>                 <div>
>                     <label htmlFor="mile">Miles</label>
>                     <input
>                         id="mile"
>                         type="number"
>                         placeholder="Miles"
>                         value={mile}
>                         onChange={handleHourChange}
>                         disabled={!flip}
>                     />
>                 </div>
>                 <button type="button" onClick={handleResetButtonClick}>Reset</button>
>                 <button type="button" onClick={handleFlipButtonClick}>Flip</button>
>             </>
>         );
>     }
> 
>     const converterArray = [
>         MinuteAndHour,
>         KilometerAndMile
>     ];
>     function App() {
>         const [index, setIndex] = React.useState(0);
> 
>         const handleSelectChange = (event) => {
>             setIndex(Number.parseInt(event.target.value));
>         };
> 
>         const getCurConverter = (index) => {
>             return converterArray[index];
>         };
>         const CurConverter = getCurConverter(index);
> 
>         return (
>             <>
>                 <h1>Super Converter</h1>
>                 <select onChange={handleSelectChange}>
>                     <option value="0">Minute & Hour</option>
>                     <option value="1">Kilometer & Mile</option>
>                 </select>
>                 <CurConverter />
>             </>
>         );
>     }
> 
>     ReactDOM.render(<App />, root);
> </script>
> ```
> 
> index 접근하지 말라는 소리는 없었잖아용
> ㅇㅇ