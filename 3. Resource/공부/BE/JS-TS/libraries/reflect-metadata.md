---
노트 생성 시각: "2026년 11월 12일 15시 09분"
tags:
  - BE
---

JS는 이미 동적이기 때문에 이 인간들은 더욱 더 동적이고 혁신적인 방법을 생각해낸 것 같습니다
동적-메타데이터 접근법이라니

그렇게 어렵지는 않을 것이라 생각하기 때문에 직접 코드 뜯어 보며 이해하는 것도 좋겠습니다

그렇다고 메타데이터만 접근 가능한 라이브러리는 아니네요
이름이 그렇긴 한데 다른 것도 있긴 있음

# 사용
특이합니다

```TypeScript
import "reflect-metadata";

Reflect.defineMetadata("role", "admin", Test);
```

side-effect import를 수행하면 자동으로 Reflect가 global로 가져와집니다
바로 사용하시면 되구요

굳이 import \* as Reflect from "reflect-metadata";를 하지 않아도 되는게
얘네는 내보내는 것이 없습니다
export { }로 되어 있음