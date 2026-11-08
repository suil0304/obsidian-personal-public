---
노트 생성 시각: "2026년 11월 07일 22시 19분"
tags:
  - BE
  - 도구
---

# import 방식
참 신기한 부분이라 보는데

얘네는
```TypeScript
import { z } from "zod";
import * as z from "zod";
import { object } from "zod";
```
이것을 셋 다 지원합니다

내부적으로 { z }로 가져온 것은 라이브러리에서 이렇게 묶어주구요
```TypeScript
import * as z from "./external.js";
export { z, z as default };
```

^debf56

똑같다는 소리에요
이러언

처음 보기에 z를 일반 변수라 생각할 수 있는데
ESM aliased namespace variable이라 생각하면 됩니다
일반 변수에 어떻게 .infer나 .input 같은 유틸리티 타입이 들어 있겠어요

# [[검증|검증]]
문서 참고하세요

# coerce
받을 때 일반적인 검증은 원하는 값이 안 오면 그대로 에러란 말이죠???
근데 이 친구는 평소대로의 JS처럼 암시적 형변환을 거쳐도 안 맞을 때만 에러를 내뱉습니다

대략 이렇게 사용하구요
```TypeScript
Zod.coerce.number(); // "1234"도 통과합니다
```

# transport
검증된 값을 다른 값으로 변환시킵니다
일종의 파이프라인에서 값 바꿔치기라고나 할까나
미들웨어라 부르기에는 살짝 그게 아쉽잖아요?

```TypeScript
Zod.string().transport((value) => value.length);
```

받으면 실제로는 value가 value.length로 오는 거죠

# refine
Zod.custom과 비슷한 느낌으로 사용자 정의 검증을 구현할 수 있구요
차이점이라 함은 이 친구가 타입을 변환하지는 않는다는 것이네요

```TypeScript
Zod.custom();
```

이렇게 custom은 처음부터 사용하여 구현하는 느낌이 강하지만

```TypeScript
Zod.string()
	.refine(
		(value) => {
			return value.length >= 8;
		},
		{
			error: "value는 8자 이상이어야 합니다."
		}
	);
```

로 사용할 수 있다는 것입니다

당연하게도 transport와 refine을 함께 사용하는 것도 가능합니다

# preprocess
전처리구요
검증 전에 미리 전처리하는 것입니다

# pipe
파이프라인마냥 어떤 스키마의 output을 다른 스키마의 input으로 넣을 수 있습니다

이게무슨