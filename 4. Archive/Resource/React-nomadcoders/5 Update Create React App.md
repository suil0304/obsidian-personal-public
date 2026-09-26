> [!note]+ # #5.0 Introduction
> create-react-app과 친해져 봅시다
> 
> ```bash
> npx create-react-app your-name
> ```
> 
> Vite 등도 있지만
> React 앱은 보통 이것으로 만들 수 있구요
> 
> 드디어 HTML 파일에 즉석으로 import하는 짓거리를 멈출 수 있게 되었습니다
> 
> 또한
> create-react-app은 웹을 publish하는 기능도 갖추고 있다고 하네요
> 
> ```javascript
> // /src/index.js
> import React from 'react';
> import ReactDOM from 'react-dom/client';
> import './index.css';
> import App from './App';
> import reportWebVitals from './reportWebVitals';
> 
> const root = ReactDOM.createRoot(document.getElementById('root'));
> root.render(
>   <React.StrictMode>
>     <App />
>   </React.StrictMode>
> );
> 
> // If you want to start measuring performance in your app, pass a function
> // to log results (for example: reportWebVitals(console.log))
> // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
> reportWebVitals();
> ```
> 
> 익숙한 것이 은근 많이 보이고 있구요
> 
> ```html
> <!-- /public/index.html -->
> <!DOCTYPE html>
> <html lang="en">
>   <head>
>     <meta charset="utf-8" />
>     <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
>     <meta name="viewport" content="width=device-width, initial-scale=1" />
>     <meta name="theme-color" content="#000000" />
>     <meta
>       name="description"
>       content="Web site created using create-react-app"
>     />
>     <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
>     <!--
>       manifest.json provides metadata used when your web app is installed on a
>       user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
>     -->
>     <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
>     <!--
>       Notice the use of %PUBLIC_URL% in the tags above.
>       It will be replaced with the URL of the `public` folder during the build.
>       Only files inside the `public` folder can be referenced from the HTML.
> 
>       Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
>       work correctly both with client-side routing and a non-root public URL.
>       Learn how to configure a non-root public URL by running `npm run build`.
>     -->
>     <title>React App</title>
>   </head>
>   <body>
>     <noscript>You need to enable JavaScript to run this app.</noscript>
>     <div id="root"></div>
>     <!--
>       This HTML file is a template.
>       If you open it directly in the browser, you will see an empty page.
> 
>       You can add webfonts, meta tags, or analytics to this file.
>       The build step will place the bundled scripts into the <body> tag.
> 
>       To begin the development, run `npm start` or `yarn start`.
>       To create a production bundle, use `npm run build` or `yarn build`.
>     -->
>   </body>
> </html>
> ```
> 
> div#root도 있네용
> 
> 딸-깍이잖아
> 
> 우선 배우는 과정이기 때문에
> reportVitals 함수를 비롯한 대부분의 무언가를 제거해봅시다
> 이러언

> [!note]+ # #5.1 Tour of CRA
> create-react-app과 친밀해지는 시간을 가져봅시다
> 이러언
> 
> 컴포넌트를 만들어볼 예정이구요
> 
> Props와 PropTypes를 만져보도록 합시다
> 
> ```bash
> npm install prop-types
> ```
> 
> ```javascript
> /**
>  * @import React from "react"
>  */
> 
> import PropTypes from "prop-types";
> 
> /**
>  * @typedef {{
>  *      text:string
>  * }} ButtonProps
>  */
> /**
>  * 
>  * @param {ButtonProps} props 
>  * @returns {React.JSX.Element}
>  */
> function Button({ text = "hello" }) {
>     return (
>         <button>
>             {text}
>         </button>
>     );
> }
> 
> Button.propTypes = {
>     text: PropTypes.string.isRequired
> };
> 
> export default Button;
> ```
> 
> 좋습니다
> 
> 이제 CSS를 적용시켜볼 수 있을 것 같구요
> 
> CSS를 적용시키는 방법은 약 2가지구요
> 
> 우선 CSS 파일을 만들어 보다
> 
> ```css
> /* /src/css/Button.css */
> button {
>     color: white;
>     background-color: tomato;
> }
> ```
> 
> 첫 번째 방식으로는 CSS 파일을 부수 효과 가져오기 방식으로 가져오는 것이구요
> 
> ![[image 153.png]]
> 
> 좋구요
> 
> 또는 style에 직접 inline으로 달아줄 수 있구요
> 
> 아니면 다음과 같이 해볼 수도 있다고 하구요
> 
> ```css
> .btn-component {
>     color: white;
>     background-color: tomato;
> }
> ```
> 
> ```javascript
> /**
>  * @import React from "react"
>  */
> 
> import PropTypes from "prop-types";
> 
> import style from "../css/Button.module.css";
> 
> /**
>  * @typedef {{
>  *      text:string
>  * }} ButtonProps
>  */
> /**
>  * 
>  * @param {ButtonProps} props 
>  * @returns {React.JSX.Element}
>  */
> function Button({ text = "hello" }) {
>     return (
>         <button className={style["btn-component"]}>
>             {text}
>         </button>
>     );
> }
> 
> Button.propTypes = {
>     text: PropTypes.string.isRequired
> };
> 
> export default Button;
> ```
> 
> ![[image 154.png]]
> 
> 이렇게 변환해주고
> 
> ![[image 155.png]]
> 
> ![[image 156.png]]
> 
> CSS를 완벽하게 모듈로써 사용 가능해집니다
> 
> TS와 함께 사용하면
> 
> ```typescript
> declare module "../css/Button.module.css" {
> 	declare const style:{
> 		"btn-component":string
> 	};
> };
> ```
> 
> 와 같은 형태로 타입 정의 파일을 만들 수 있을 것 같구요
> 
> 정말 좋네요
> 
> 심지어
> CSS에서 타이틀 이름이 겹쳐도 실제 빌드 과정에서는 랜덤 문자열로 나오니
> 매우 좋은 것이구요