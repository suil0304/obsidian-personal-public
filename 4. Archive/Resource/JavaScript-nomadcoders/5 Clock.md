> [!note]+ # #5.0 Intervals
> 이쯤에서부터는 기능에 따라 모듈화로 파일을 쪼개보다
> 
> /js/app.js를 greeting.js로 이름 변경
> 그리고 clock.js를 추가하다
> 이러언
> 
> 우선 index.html에 h2 요소를 추가하다
> 이것은 시계가 될 것인
> 
> ```html
> <h2 id="clock"></h2>
> ```
> 
> 그리고 clock.js에 다음을 추가하다
> 
> ```javascript
> /**
>  * @type {HTMLHeadingElement}
>  */
> const clock = document.querySelector("#clock");
> ```
> 
> clock을 제대로 가져오고 있는
> 
> 그래서 interval과 timeout이 무엇인???
> 
> interval은 매번 일어나는 무언가입니다
> timeout은 한 번 일어나고 끝인 무언가입니다
> 
> 그래서 다음과 같이 사용하구요
> 
> ```javascript
> setInterval(func, 1000);
> ```
> 
> 첫 번째 인자는 함수
> 두 번째 인자는 ms 단위의 실수를 받습니다
> 
> 지울 때는 setInterval에서 나온 id를 clearInterval에 넣고 내려

> [!note]+ # #5.1 Timeouts and Dates
> 그러면 timeout은 어떻게 사용하는???
> 
> 다음과 같이 사용하는
> 
> ```javascript
> setTimeout(func, 1000);
> ```
> 
> 간단하죠???
> 
> 마찬가지로 setTimeout 또한 id를 반환하기 때문에
> 
> 지울 때는 setTimeout에서 나온 id를 clearTimeout에 넣고 내려
> 
> 그래서 다 좋은데
> 
> 날짜와 시간은 어떻게 가져오다???
> 
> Date 클래스를 사용하다
> 
> ```javascript
> const date = new Date();
> console.log(date);
> ```
> 
> ![[image 157.png]]
> 
> 다 해줬잖아
> 
> 모든 자세한 필드와 메서드에 대하여 다음을 참조하길 바라다
> 
> [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date)
> 
> 그래서 결국 setInterval과 이것 저것을 조합하여
> 다음을 얻을 수 있는
> 
> ```javascript
> function setClock() {
>     const date = new Date();
>     clock.innerText = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
> }
> 
> setClock()
> setInterval(setClock, 1000);
> ```
> 
> 근데 이러면 여러 군데에 대하여 10보다 작은 숫자들이 00, 01, 02, …가 아닌 0, 1, 2, …가 되어버리기 때문에
> 매우 불편해져버리는
> 크아악

> [!note]+ # #5.2 PadStart
> 우리는 길이를 무조건 이 만큼 채워야 한다는 무언가를 string에서 가져와 사용할 수 있는
> 
> ```javascript
> "1".padStart(2, "0"); // result: "01"
> ```
> 
> pad는 padding의 줄임말이구요
> 
> 만약 이미 첫 번째 인수의 길이와 같거나 더 긴 경우 더 채우지 않고 원래의 문자열을 반환한답니다
> 
> ```javascript
> /**
>  * @type {HTMLHeadingElement}
>  */
> const clock = document.querySelector("#clock");
> 
> function setClock() {
>     const date = new Date();
> 
>     const hour = String(date.getHours());
>     const minute = String(date.getMinutes());
>     const second = String(date.getSeconds());
> 
>     clock.innerText = `${hour.padStart(2, "0")}:${minute.padStart(2, "0")}:${second.padStart(2, "0")}`;
> }
> 
> setClock()
> setInterval(setClock, 1000);
> ```

> [!note]+ # #5.3 Recap
> 돌아보기 시간이구요
> 
> 역시나 쉽잖아용