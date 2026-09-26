> [!note]+ ## URL(Uniform Resource Locator)
> **자원(Resource) 위치(Locator) 나타내다 통일된(Uniform) 방식**
> 
> 대략적으로 주소와 같음.
> 
> `https://www.example.com:443/shop/books?category=it#intro`
> 
> 1. **Protocol(Scheme):** `https`
>     *어떠한 규칙으로 통신할 것인가?*
> 2. **Host(Domain Name):** `www.example.com` 
>     *어느 컴퓨터(서버)로 찾아갈 것인가?*
> 3. **Port:** `:443`
>     *그 서버의 몇 번째 문(포트)로 들어갈 것인가? (HTTP는 기본 80 포트, HTTPS는 기본 443 포트 사용)*
> 4. **Path:** `/shop/books`
>     *구체적으로 서버의 어떤 경로에 있는 자원인가?*
> 5. **Query String:** `?category=it`
>     *(서버에 전달할 추가 옵션이나 정보 등등)*
> 6. **Fragment(Anchor):** `#intro`
>     *페이지 내의 특정 위치(제목 등)를 가리킴.*

> [!note]+ ## URI(Uniform Resource Identifier)
> **자원을 식별하는 가장 넓은 개념(이름 혹은 주소).**
> 
> 대략적으로 변수 식별자와 같음.
> 
> ```c
> #include <stdio.h>
> 
> int main() {
> 	int variable = 0; // URI
> 	int* varPtr = &variable; // URL
> 
> 	return 0;
> }
> ```
> 
> 모든 URL은 다 내꺼다요
> 하지만???
> 모든 URI는 URL이 될 수 없다 이거거든용???

> [!note]+ ## 관계
> URI가 URL을 포함하는 관계
> 
> 객체지향적으로 설명하자면 이렇게 된다고 하네요
> 
> ```java
> interface URI {}
> 
> class URL implements URI {}
> ```

> [!note]+ ## 결론(정리)
> | **구분** | **개념적 느낌** | **비유(C언어/수학)** | **역할** |
> | --- | --- | --- | --- |
> | **URI** | **추상적 식별** | 정수 / 변수명 | "무엇"인지 정의함 |
> | **URL** | **구체적 구현** | 자연수 / 메모리 주소 | "어디"에 있는지 가리킴 |
