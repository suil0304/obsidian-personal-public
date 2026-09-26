> [!note]+ # #3.0 The Document Object
> 그래서 HTML과 JS를 연결하여 어떻게 사용하다???
> 
> 봐왔듯이 JS로 HTML 요소 삭제
> 추가
> 수정
> 읽기
> 
> 다 가능하다는 소리인 거임
> 다 해줬잖아
> 
> ![[image 83.png]]
> 
> document라는 직접 정의된 변수로 HTML 본문 전체를 가져올 수 있구요
> 
> ```javascript
> console.dir(document);
> ```
> 
> 위의 명령어를 적어 아래와 같은 데이터를 가져올 수 있습니다
> 그러니까 한 마디로 객체라는 소리구요
> 
> ![[image 84.png]]
> 
> 그 중에 title이라는 필드가 있구요
> 
> title에는 수일이 적어둔 Momentum Clone Coding이 있구요
> 
> 신기하네용
> 
> document의 title 값을 수정하면 무슨 일이 일어나다???
> 
> ![[image 85.png]]
> 
> 다음과 같이 변하는
> 아주좋았어
> 
> 그래서 document에는 body 필드도 있던데
> 이것을 따로 console.log로 찍어보면???
> 
> ![[image 86.png]]
> 
> 말 그대로 body를 가리키는 모습을 볼 수 있었구요
> 
> document.location으로 현재 어느 위치에 있는가 등등 가져올 수 있구요
> 그냥 다 가져올 수 있다라 생각하는게 좋을 것 같구요

> [!note]+ # #3.1 HTML in Javascript
> ```html
> <h1 id="title">Grab me!</h1>
> ```
> 
> 다음을 index.html의 body에 추가한 다음 JS로 가져오는 방법을 알아보다
> 
> ```javascript
> document.getElementById("title");
> ```
> 
> title id를 가진 요소를 가져오구요
> 
> ![[image 87.png]]
> 
> ```javascript
> /**
>  * @type {HTMLElement}
>  */
> const title = document.getElementById("title");
> 
> console.dir(title);
> ```
> 
> ![[image 88.png]]
> 
> 속성 값이 전부 나오고 있구요
> 신기하네용
> 
> 이 중에 하나를 잡아서 보다
> 
> ```javascript
> autofocus: false
> ```
> 
> 이렇게 나와 있는 값이 있는
> 
> ```html
> <h1 id="title" autofocus>Grab me!</h1>
> ```
> 
> 이렇게 했을 때
> 
> autofocus를 다시 출력시켜보면
> 
> ![[image 89.png]]
> 
> true가 나오구요
> 
> 확실하게 연결되어 있음을 다시 한 번 볼 수 있었구요
> 
> ```html
> <h1 id="title" class="test">Grab me!</h1>
> ```
> 
> class도 가져올 수 있구요

> [!note]+ # #3.2 Searching For Elements
> class로 요소를 가져올 수 있습니다
> 
> 이렇게 요소가 있다고 가정했을 때
> 
> ```html
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> <h1 id="title" class="test">Grab me!</h1>
> ```
> 
> ```javascript
> document.getElementsByClassName("test");
> ```
> 
> 이렇게 바로 가져올 수 있구요
> 
> ![[image 90.png]]
> 
> 이렇게 가져오는게 가능하구요
> 
> 배열 요소이기 때문에 당연하게도 elements[0]과 같은 형태로 인덱스 접근이 가능하구요
> 
> ```html
> <div class="test">
> 	<h1>Grab me!</h1>
> </div>
> ```
> 
> 위와 같은 형태의 무언가에서 h1을 가져오고 싶구요
> 
> ```javascript
> document.getElementsByTagName("h1");
> ```
> 
> 이렇게 해서 가져올 수도 있겠지만???
> 
> 모든 h1을 가져오고 싶은 것은 아니잖아용
> 물론 Array를 반환하는 녀석이구요
> 당연하잖아용
> 
> document.querySelector라는 것으로 CSS 선택자로 가져오듯이 요소를 가져올 수 있구요
> 
> ```javascript
> document.querySelector("div.test > h1");
> ```
> 
> 위와 같이 입력하면 test class를 가진 div 요소의 바로 밑 h1 자식 중 한 요소를 가져오라는 뜻이구요
> 여기까지도 쉽잖아용
> 
> ![[image 91.png]]
> 
> 이렇게 해서 바로 가져올 수 있구요
> 
> 한 녀석만 가져오는 것이 싫다면???
> 
> ```javascript
> document.querySelectorAll("div.test > h1");
> ```
> 
> 이건 모두 검색해서 배열로 가져오구요
> 
> 그래서 h1을 가져와 innerText를 수정할 수 있구요
> 
> ```javascript
> const element = document.querySelector("div.test > h1");
> 
> element.innerText = "Changed";
> ```
> 
> 아주좋았어

> [!note]+ # #3.3 Events
> 지난 번에 h1.test 요소를 console.dir하면서 무엇이 있는가 살펴 보았습니다
> 
> on으로 시작하는 무언가가 굉장히 많았죠???
> 
> 이것은 부르다 Event
> 
> Event는 위에 마우스를 가져다 대든
> 클릭하든
> 뭘 하든 Event가 될 수 있음을 알아두기 바랍니다
> 
> 그리고 이 모든 Event를 JS가 listen할 수 있다는 것입니다
> 
> onclick에 대하여 다뤄보다
> 
> element.addEventListener로 가능한
> 
> ## click Event
> 
> ```javascript
> function handleTitleClick() {
> 	console.log("Title was clicked!");
> }
> 
> element.addEventListener("click", handleTitleClick);
> ```
> 
> ![[image 92.png]]
> 
> 아주좋았어

> [!note]+ # #3.4 Events part Two
> 아무래도 요소의 이벤트를 찾는 것은 구글링이 정답인 것 같습니다
> 
> MDN Web Docs이라는 사이트가 있구요
> Mozilla Developer Network Web Docs의 줄임말이구요
> 이러언
> 
> 하지만 대부분의 경우 HTML을 알려주겠죠???
> 
> Web APIs라 적힌 웹사이트를 들어가면 JavaScript 기준으로 알려준다고 하네요
> Web에 대한 Application Program Interface를 알려주는 것이니 이게 코딩이죠
> ㅇㅇ
> 
> ![[image 93.png]]
> 
> 클립보드 이벤트도 있고
> 호오
> 
> 이제 마우스가 요소 안으로 들어왔을 때의 이벤트를 추가해보다
> 
> ## mouseenter Event
> 
> ```javascript
> function handleTitleEnter() {
> 	console.log("mouse is here!");
> }
> 
> element.addEventListener("mouseenter", handleTitleEnter);
> ```
> 
> ![[image 94.png]]
> 
> ## mouseleave Event
> 
> ```javascript
> function handleTitleLeave() {
> 	element.innerText = "mouse is gone!";
> }
> 
> element.addEventListener("mouseleave", handleTitleLeave);
> ```
> 
> ![[image 95.png]]
> 
> 아주 좋았어

> [!note]+ # #3.5 More Events
> window
> 그러니까 창의 Event도 설정할 수 있구요
> 
> ## resize Event
> 
> ```javascript
> function handleWindowResize() {
> 	console.log("window was resized");
> }
> 
> window.addEventListener("resize", handleWindowResize);
> ```
> 
> ![[image 96.png]]
> 
> ## copy Event
> 
> ```javascript
> function handleWindowCopy() {
> 	window.alert("copier!");
> }
> 
> window.addEventListener("copy", handleWindowCopy);
> ```
> 
> ![[image 97.png]]
> 
> 이와 같이 paste도 처리할 수 있구요
> 
> ## offline Event
> 
> 말 그대로 브라우저가 offline 상태가 되었을 때 생기는 이벤트
> 
> 다만 인터넷 끊고 뭐하기 그러니 적지 아니할 예정이구요
> 이러언

> [!note]+ # #3.6 CSS in Javascript
> 이제는 CSS를 JS에서 건드려볼 예정인
> 
> 모든 요소에는 style이라는 프로퍼티가 있습니다
> CSS 스타일 건드릴 수 있는 그것 맞구용
> ㅇㅇ
> 
> div.test > h1 요소의 색이 blue일 때 tomato
> tomato일 때 blue로 설정하고 싶다면
> if문에서 style 값을 체크하면 되겠죠???
> 
> ```javascript
> function handleClickColorChange() {
> 	if(element.style.color === "blue") {
> 		element.style.color = "tomato";
> 		return;
> 	}
> 	
> 	element.style.color = "blue";
> }
> 
> element.addEventListener("click", handleClickColorChange);
> ```
> 
> 조기 리턴으로 else를 없애다
> 
> ![[image 98.png]]
> 
> ![[image 99.png]]
> 
> 아주좋았어
> 
> 하지만 이것은 JS에서 직접 style을 변경하는 방식인
> 슬픈

> [!note]+ # #3.7 CSS in Javascript part Two
> 이번에는 CSS와 연결하여 JS에서는 클래스만 추가하거나 빼버리는 방식으로 구현해보다
> 
> ```css
> h1 {
>     color: blue;
> 
>     &.clicked {
>         color: tomato;
>     }
> }
> ```
> 
> ```javascript
> function handleClickClassChange() {
>     if(!element.classList.contains("clicked")) {
>         element.classList.add("clicked");
>         return;
>     }
> 	element.classList.remove("clicked");
> }
> 
> element.addEventListener("click", handleClickClassChange);
> ```
> 
> ![[image 100.png]]
> 
> 어차피 하나만 변경하는 경우에는 그럴 수 있겠으나
> 대부분의 경우에 대해서는 classList가 더 나을 수 있음을 고려해야 하는
> 
> 근데 여기에서는 className = “clicked”와 같은 경우만 다뤄버린
> 이러언

> [!note]+ # #3.8 CSS in Javascript part Three
> 위의 내용을 참고하는
> 뭐 그래서
> 
> classList.toggle은 위의 내용을 자동화해주는
> 말 그대로 toggle이죠???
> 
> ![[image 101.png]]
> 
> 이런게 있네
> 아주좋았어