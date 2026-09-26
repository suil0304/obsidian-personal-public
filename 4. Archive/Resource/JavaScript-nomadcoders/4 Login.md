> [!note]+ # #4.0 Input Values
> ```html
> <input type="text" id="" placeholder="What in your name?">
> <button type="button">Log In</button>
> ```
> 
> ![[image 138.png]]
> 
> 못생겼구요
> CSS를 적용시키지 않은 탓이구요
> 지금은 개발 중이니
> 이러언
> 
> div로 묶어주구요
> 
> ```html
> <div id=login-form>
> 	<input type="text" id="" placeholder="What in your name?">
> 	<button type="button">Log In</button>
> </div>
> ```
> 
> ```javascript
> const loginForm = document.getElementById("login-form");
> ```
> 
> 이렇게 가져올 수 있구요
> 
> 그리고 그 밑에 있는 input을 다음과 같이 가져올 수 있구요
> 
> ```javascript
> const loginInput = loginForm.querySelector("input");
> ```
> 
> 또한 button도 가져올 수 있구요
> 
> ```javascript
> const loginButton = loginForm.querySelector("button");
> ```
> 
> 근데 loginForm을 가져와서 querySelector로 가져오는 것은
> loginForm을 가져오고 하는 만큼 길어지잖아용???
> 이러기는 하지만
> 솔직히 이 쪽이 더 의도적이고 자연스러운 코드라고 읽히고는 있구요
> 
> 아무튼 교체하여 이러언을 수행하다
> 
> ```javascript
> const loginInput = document.querySelector("#login-form input");
> const loginButton = document.querySelector("#login-form button");
> ```
> 
> loginButton에 대하여 click Event를 집어 넣을 수 있겠죠???
> 
> ```javascript
> function handleButtonClick() {
> 	console.log("click!!!!!!");
> }
> 
> loginButton.addEventListener("click", handleButtonClick);
> ```
> 
> console.dir로 loginInput 내부를 살펴보면???
> value라고 나와 있는 프로퍼티를 확인할 수 있구요
> 이것은 당연하게도 값입니다
> 여기서는 loginInput의 text value가 되겠네용
> 
> 그래서 console.log 안에 loginInput.value를 넣고 내리면
> 입력한 텍스트가 출력됩니다
> 아주좋았어

> [!note]+ # #4.1 Form Submission
> 근데 text가 비어 있으면 값을 입력해주세요라던가 무언가를 띄워야 하잖아용???
> 그래서 다음을 수행하다
> 
> ```javascript
> function handleButtonClick() {
> 	if(loginInput.value.length <= 0) {
> 		window.alert("Please write your name.");
> 		return;
> 	}
> 	else if(loginInput.value.length >= 15) {
> 		window.alert("Your name is so long.");
> 		return;
> 	}
> }
> ```
> 
> 근데 이래버리면 JS 끄는 등에서는 이러언이 되잖아용
> 
> ```javascript
> <div id=login-form>
>     <input required maxlength="15" type="text" placeholder="What in your name?">
>     <button type="button">Log In</button>
> </div>
> ```
> 
> 이렇게 하면 HTML에서 자체적으로 어느 정도는 해주겠죠
> 
> 근데???
> 이래도 안 먹히네용???
> 
> 당연한 소리인
> 
> form 요소를 사용하여 묶어야 정상 작동이 가능한
> 
> ```javascript
> <form id="login-form">
>     <input required maxlength="" type="text" placeholder="What in your name?">
>     <button type="submit">Log In</button>
> </form>
> ```
> 
> 아주좋았어
> 
> 근데 이러면 또 submit되면서 화면을 새로고침한단 말이죠???
> 
> 우리는 또한 이것은 막고 싶을 뿐인

> [!note]+ # #4.2 Events
> 또 다시 돌아온 Event
> 
> ```javascript
> const loginForm = document.getElementById("login-form");
> const loginInput = loginForm.querySelector("input");
> 
> /**
>  * submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleLoginSubmit(event) {
>     event.preventDefault();
> }
> 
> loginForm.addEventListener("submit", handleLoginSubmit);
> ```
> 
> Event가 읽혔을 때 해당하는 event를 보내는 것인데
> event.preventDefault를 호출하면 말 그대로 기본 동작을 예방할 수 있구요
> 
> event를 console.log()에 넣어 내리면???
> 
> ![[image 139.png]]
> 
> 이렇게 나오죠???
> 
> 뭐 그래서
> 
> 다음으로는 nomadcoders.co와 연결되는 a 태그를 추가하여 이러언을 수행하다
> 
> ```html
> <a href="https://nomadcoders.co/"></a>
> ```
> 
> ![[image 140.png]]
> 
> ![[image 141.png]]
> 
> client의 마우스 위치도 가져올 수 있구요
> 호오
> 
> ![[image 142.png]]
> 
> 무슨 차이인지는 잘 모르겠는데
> 모니터 화면 상에서 어디를 클릭했는지인 것 같구요
> 이러언
> 
> 근데 a 태그의 클릭 기본 동작을 preventDefault하고 싶구요
> 
> ```javascript
> /**
>  * a tag click handler
>  * @param {PointerEvent} event 
>  */
> function handleLinkClick(event) {
>     event.preventDefault();
> }
> 
> link.addEventListener("click", handleLinkClick);
> ```
> 
> 이렇게 하면 막히면서 다른 링크로 넘어가지지 않구요
> 아주좋았어

> [!note]+ # #4.4 Getting Username
> 사실 a 태그는 preventDefault와 click, submit Event의 차이를 알아보고자 이러언한 무언가였구요
> 따흐흑
> 
> 뭐 그래서
> username을 입력하여 submit했을 때
> 제대로 입력했으면 form을 지워버리고 싶구요
> 흐음
> 
> 이건 첫 번째 Lesson
> HTML에서 요소 지워버리기
> 
> 이건 두 번째 Lesson
> CSS에서 숨겨버리기
> 
> hidden class를 classList에 추가하여 이러언시키다
> 
> ```css
> .hidden {
>     display: none;
> }
> ```
> 
> ```javascript
> /**
>  * submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleLoginSubmit(event) {
>     event.preventDefault();
> 
>     loginForm.classList.add("hidden");
> }
> 
> loginForm.addEventListener("submit", handleLoginSubmit);
> ```
> 
> 이름을 적어줄 h1 태그를 추가하다
> 
> ```javascript
> <h1 class="hidden" id="greeting"></h1>
> ```
> 
> 기본적으로는 hidden으로 숨겨져 있어야 하기 때문에
> 이렇게 해뒀구요
> 
> ![[image 143.png]]
> 
> ```javascript
> const greeting = document.getElementById("greeting");
> 
> const hiddenClass = "hidden";
> /**
>  * submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleLoginSubmit(event) {
>     event.preventDefault();
> 
>     greeting.innerText = `Hello, ${loginInput.value}!`;
> 
>     loginForm.classList.add(hiddenClass);
>     greeting.classList.remove(hiddenClass);
> }
> 
> loginForm.addEventListener("submit", handleLoginSubmit);
> ```
> 
> 아주좋았어
> 
> 근데 이러면 새로고침될 때마다 계속 적어야 하잖아용
> 불편한

> [!note]+ # #4.5 Saving Username
> window.localStorage가 있구요
> 이것은 그래서 무엇인???
> 
> ![[image 144.png]]
> 
> ![[image 145.png]]
> 
> interesting
> 
> ![[image 146.png]]
> 
> 이해한
> 말 그대로 localStorage였는
> 
> 이것으로 저장한 다음 이러언스러운 로직을 추가하는게 가능할 것 같은

> [!note]+ # #4.6 Loading Username
> 이제는 username이 비어 있을 경우 이전과 같은 로직을 수행하고
> username이 비어 있지 않은 경우 바로 h1을 띄우면 되는
> 
> ```javascript
> // class name
> const HIDDEN_CLASS_NAME = "hidden";
> 
> // localStorage
> const USERNAME_KEY = "username";
> 
> // login
> const loginForm = document.getElementById("login-form");
> const loginInput = loginForm.querySelector("input");
> 
> // greetingie
> const greeting = document.getElementById("greeting");
> 
> let localUsername = window.localStorage.getItem(USERNAME_KEY);
> 
> /**
>  * submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleLoginSubmit(event) {
>     event.preventDefault();
> 
>     const username = loginInput.value;
> 
>     localUsername = username;
>     window.localStorage.setItem(USERNAME_KEY, username);
> 
> 
>     loginForm.classList.add(HIDDEN_CLASS_NAME);
> 
>     showGreeting();
> }
> 
> /**
>  * show show show greenchi
>  */
> function showGreeting() {
>     greeting.innerText = `Hello, ${localUsername}!`;
>     greeting.classList.remove(HIDDEN_CLASS_NAME);
> }
> 
> if(localUsername === null) {
>     loginForm.addEventListener("submit", handleLoginSubmit);
>     loginForm.classList.remove(HIDDEN_CLASS_NAME);
> }
> else {
>     showGreeting();
> }
> ```
> 
> 코드가 점점 길어지는 모습이 마음에 들구요
> 크하하

> [!note]+ # #4.7 Super Recap
> 천천히 돌아보고 뭐 이러언
> 
> 쉽잖아용
> 
> 넘기다