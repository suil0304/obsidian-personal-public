---
노트 생성 시각: "2026년 11월 14일 15시 59분"
tags:
  - BE
  - 용어
---

*Command Query Separation*

유사 패턴입니다
단순해요

# Command
여기에서의 Command(*작업/명령이라 부를 수 있겠구요*)는 다음과 같은 특징을 지닙니다

- 시스템 상태 변경
	이는 DB에 데이터를 저장하는 것도 당연히 포함됩니다
- side-effect
	부작용 등이라 부를 수 있는 것이겠는데
	함수형 관점에서 보면 순수 함수가 아니다?
	그런 정도를 가지고 있습니다
- 반환값
	처리 결과나 식별자 등을 반환해야 합니다
	식별자를 반환하는 예시는 JS의 setInterval 정도 느낌이지 않을까요

주요 관심사로는 도메인 규칙
무결성 등이 있겠구요

# Query
여기에서의 Query(*조회/질의라 부를 수 있겠구요*)는 다음과 같은 특징을 지닙니다

- 시스템 상태 조회
- side-effect 없어야 함
	한 번 값 조회하고 오는 것인데 다른 외부에서 수정하지 않는 한 변경될리가 없잖아요
	그래도 순수하다는 거죠
- 반환값
	회원 정보 조회라던가
	그러한 등등

주요 관심사로는 조회 성능
데이터 가공 등이 있겠구요

# 그래서 이것이 무엇인가?
값을 반환하는 이 메서드 하나가 Command 또는 Query 둘 중 하나만 수행하도록 하라는 소리에요

예를 들어 아래와 같은 코드가 있다고 하면
```TypeScript
const user = await userRepository.update(userId, {
	data1: newData1
});
```
이는 CQS의 관점에서는 위배됩니다

가져와도 이렇게 가져와야 한다는 것이구요
```TypeScript
await userRepository.update(userId, {
	data1: newData1
});

const user = await userRepository.get(userid);
```

update가 DB 자체의 RETURNING을 이용해서 값을 반환하도록 체이닝 메서드 returning 등을 지원했더라면 위배하지는 않았을 듯싶긴 합니다만

