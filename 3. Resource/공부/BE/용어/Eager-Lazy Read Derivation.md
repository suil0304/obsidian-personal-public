---
노트 생성 시각: "2026년 11월 14일 16시 51분"
tags:
  - BE
  - 용어
---

Eager/Lazy Read Derivation입니다
한국어로 직역하자면 선행/후행 읽기 파생이려나요

우리가 짜는 보통의 CRUD 서비스는 Lazy Read Derivation 쪽입니다
무슨 말이냐 하면 받는 시점에 조회하고 반환하잖아요

그에 비해서 Eager Read Derivation은 수정/생성 시점에 캐시합니다
조회 비용을 줄이는 선택을 함과 동시에 수정이 무서워지는 방식인 거죠
트레이드 오프