> [!note]+ # #7.0 Setup
> 우선 HTML을 만들고 연결 등을 해보면 좋겠죠???
> 
> 입력을 받는 등의 행동을 수행해야 하니
> form 안에 input을 넣는 것이 좋겠는
> 끼얏호우
> 
> ```javascript
> <form id="todo-form">
>     <input type="text" placeholder="Write a To Do and Press Enter" required>
> </form>
> ```
> 
> 이제 ul로 unordered list를 추가하면 TODO 리스트 어쩌구를 추가할 수 있겠는
> 아주좋았어
> 
> ```javascript
> <ul id="todo-list"></ul>
> ```
> 
> 이렇게만 하면 li는 JS에서 추가하니
> 아주좋았어
> 
> ```javascript
> /**
>  * @type {HTMLFormElement}
>  */
> const todoForm = document.getElementById("todo-form");
> /**
>  * @type {HTMLUListElement}
>  */
> const todoList = document.getElementById("todo-list");
> ```
> 
> 이제 이렇게 가져오면 끝
> 
> 그래요
> input을 넣고 안에 값을 입력했는데
> Enter를 눌러도 안 사라지면 TODO 리스트에서는 이상하게 보일 것 같구요
> 이러언
> 
> ```javascript
> /**
>  * @type {HTMLFormElement}
>  */
> const todoForm = document.getElementById("todo-form");
> /**
>  * @type {HTMLInputElement}
>  */
> const todoInput = todoForm.querySelector("input");
> /**
>  * @type {HTMLUListElement}
>  */
> const todoList = document.getElementById("todo-list");
> 
> /**
>  * TODO form의 submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleTodoSubmit(event) {
>     event.preventDefault();
>     const inputValue = todoInput.value;
>     todoInput.value = "";
> }
> 
> todoForm.addEventListener("submit", handleTodoSubmit);
> ```

> [!note]+ # #7.1 Adding ToDos
> ```javascript
> /**
>  * TODO 리스트에 TODO 추가하기.
>  * 이러언
>  * @param {string} value 
>  */
> function addTodo(value) {
>     
> }
> ```
> 
> 우선 함수 하나 만들고 시작해보다
> 
> 이것 저것 구현을 하면
> 다음과 같이 되는
> 
> ```javascript
> /**
>  * TODO 리스트에 TODO 추가하기.
>  * 이러언
>  * @param {string} value 
>  */
> function addTodo(value) {
>     const todoLi = document.createElement("li");
>     const todoSpan = document.createElement("span");
>     const todoDeleteButton = document.createElement("button");
> 
>     todoSpan.innerText = value;
> 
>     todoLi.appendChild(todoSpan);
>     todoLi.appendChild(todoDeleteButton);
> 
>     todoList.appendChild(todoLi);
> }
> ```
> 
> 근데 버튼을 추가만 했지 삭제하는 기능은 구현하지 않았음
> 이게뭐야

> [!note]+ # #7.2 Deleting To Dos
> ```javascript
> /**
>  * 
>  * @param {PointerEvent} event 
>  */
> function handleClickTodoDelete(event) {
>     /**
>      * @type {HTMLButtonElement}
>      */
>     const target = event.target;
>     /**
>      * @type {HTMLLIElement}
>      */
>     const parent = target.parentElement;
> 
>     parent.remove();
> }
> 
> /**
>  * TODO 리스트에 TODO 추가하기.
>  * 이러언
>  * @param {string} value 
>  */
> function addTodo(value) {
>     const todoLi = document.createElement("li");
>     const todoSpan = document.createElement("span");
>     const todoDeleteButton = document.createElement("button");
> 
>     todoSpan.innerText = value;
>     todoDeleteButton.innerText = "X";
> 
>     todoDeleteButton.addEventListener("click", handleClickTodoDelete);
> 
>     todoLi.appendChild(todoSpan);
>     todoLi.appendChild(todoDeleteButton);
> 
>     todoList.appendChild(todoLi);
> }
> ```
> 
> event.target은 말 그대로 Event의 타겟을 의미하구요
> click Event에서 타겟은 눌린 본인이 되겠죠???
> 
> 그리고 target.parentElement는 그 위의 li를 가리키게 되겠죠???
> 
> 그 parentElement의 메서드 remove를 호출하여 제거하다
> 아주좋았어

> [!note]+ # #7.3 Saving To Dos
> 저장을 만들어볼 차례입니다
> 
> 당연하게도 localStorage를 사용할 것이구요
> 
> ```javascript
> /**
>  * TODO 리스트에 TODO 추가하기.
>  * 이러언
>  * @param {string} value 
>  */
> function addTodo(value) {
>     todoArray.push(value);
>     window.localStorage.setItem(TODO_LIST_KEY, JSON.stringify(todoArray));
> 
>     const todoLi = document.createElement("li");
>     const todoSpan = document.createElement("span");
>     const todoDeleteButton = document.createElement("button");
> 
>     todoSpan.innerText = value;
>     todoDeleteButton.innerText = "X";
> 
>     todoDeleteButton.addEventListener("click", handleClickTodoDelete);
> 
>     todoLi.appendChild(todoSpan);
>     todoLi.appendChild(todoDeleteButton);
> 
>     todoList.appendChild(todoLi);
> }
> ```
> 
> JSON.stringify로 todoArray를 변환하다
> string으로 변환되기에 저장하기 좋아지는
> 고노야로
> 
> 근데 이러면 불러오기와 삭제는 어떻게 함???

> [!note]+ # #7.4 Loading To Dos part One
> 이제 불러오는 기능을 구현해볼 것이구요
> 
> JSON.parse로 다시 돌려놓을 수 있음
> 
> ```javascript
> const localTodoArray = window.localStorage.getItem(TODO_LIST_KEY);
> 
> if(localTodoArray) {
>     /**
>      * @type {string[]}
>      */
>     const parsed = JSON.parse(localTodoArray);
> 
>     parsed.forEach((value) => {
>         todoArray.push(value);
>     });
> }
> ```
> 
> 이렇게 하면 forEach를 돌려서 채워줄 수 있겠구요
> 
> 화살표 함수를 드디어 사용하네용
> 이러언
> 
> li 추가는 뭐
> 다음에 하도록 하구요
> 이러언

> [!note]+ # #7.5 Loading To Dos part Two
> 원래였으면 addTodo 함수에 push가 안 들어가 있어서
> todoArray가 텅 비어 있음
> → 기존 localStorage 덮어쓰기
> 
> 근데 저는 이미 처리를 해두어서 멀쩡하구요
> 이러언
> 
> ```javascript
> if(localTodoArray) {
>     /**
>      * @type {string[]}
>      */
>     const parsed = JSON.parse(localTodoArray);
> 
>     parsed.forEach(addTodo);
> }
> ```
> 
> 이제 삭제 처리만 하면 되겠구나
> 이러언

> [!note]+ # #7.6 Deleting To Dos part One
> 삭제 접근에 용이하도록 id를 추가하여 리팩토링하다
> 
> ```javascript
> /**
>  * @typedef {{
>  *      id:number,
>  *      text:string
>  * }} Todo
>  */
>  
>  /**
>  * TODO form의 submit handler
>  * @param {SubmitEvent} event 
>  */
> function handleTodoSubmit(event) {
>     event.preventDefault();
>     const inputValue = todoInput.value;
>     todoInput.value = "";
>     addTodo({
>         id: todoArray.length + 1,
>         text: inputValue
>     });
> }
> 
> /**
>  * TODO 리스트에 TODO 추가하기.
>  * 이러언
>  * @param {Todo} value 
>  */
> function addTodo(value) {
>     todoArray.push(value);
>     window.localStorage.setItem(TODO_LIST_KEY, JSON.stringify(todoArray));
> 
>     const todoLi = document.createElement("li");
>     const todoSpan = document.createElement("span");
>     const todoDeleteButton = document.createElement("button");
>     
>     todoLi.id = value.id;
> 
>     todoSpan.innerText = value.text;
>     todoDeleteButton.innerText = "X";
> 
>     todoDeleteButton.addEventListener("click", handleClickTodoDelete);
> 
>     todoLi.appendChild(todoSpan);
>     todoLi.appendChild(todoDeleteButton);
> 
>     todoList.appendChild(todoLi);
> }
> ```
> 
> id까지 추가했으면 삭제는 금방이라 생각하기 때문에
> 다음에 이어서 하다

> [!note]+ # #7.7 Deleting To Dos part Two
> 이를 위하여 todoArray.filter를 사용할 수 있는
> 
> true가 나오면 남기고 false가 나오면 거른답니다

> [!note]+ # #7.8 Deleting To Dos part Three
> ```javascript
> /**
>  * 
>  * @param {PointerEvent} event 
>  */
> function handleClickTodoDelete(event) {
>     /**
>      * @type {HTMLButtonElement}
>      */
>     const target = event.target;
>     /**
>      * @type {HTMLLIElement}
>      */
>     const parent = target.parentElement;
> 
>     todoArray = todoArray.filter((todo) => {
>         return Number.parseInt(parent.id) !== todo.id;
>     });
>     window.localStorage.setItem(TODO_LIST_KEY, JSON.stringify(todoArray));
> 
>     parent.remove();
> }
> ```
> 
> 이렇게 filter로 걸어두면 잘 걸러지겠구요
> 아주좋았어