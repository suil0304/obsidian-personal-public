---
노트 생성 시각: "2026년 11월 01일 13시 59분"
tags:
  - BE
  - 도구
---

보다 보면 알아서 외워지는 것들이 커맨드라
굳이 적을 필요가 있을까 싶기도 한데
간단하게 적어봅시다

# new
새로운 프로젝트를 생성합니다
아주 간단하네요

이와 관련한 플래그는 다음과 같구요
- --strict
	아주 중요합니다
- --no-observe
	요즘에 NestJS 업데이트하면서 nestjs/observe가 기본으로 들어왔더라구요
	빼고 싶다면 참고하세요
- --skip-tests
	소중한 테스트 파일들을 생성하지 않고 초기화합니다
- --skip-git
	모노 레포 구성 도중 apps/api 등에서 .git이 추가로 설정되는 경우가 있습니다
	이것을 넣으면 .git을 스킵하구요

`n`으로 줄일 수 있습니다

# add
사용하면 npm에서 가져오며 동시에 CLI schematic 설정도 한다고 하네요

패키지 매니저는 직접 체크하고 그것을 사용한다네요
체크 순서는 yarn -> pnpm -> bun -> npm이라나 뭐라나
current work directory만 확인하기 때문에 상위에 무언가가 있는 구조라면 아쉬운 것이구요

이와 관련한 플래그는 다음과 같구요
- --skip-install
	먼저 `bun add @nestjs/swagger`를 한 후 `nest add --skip-install @nestjs/swagger`를 하면 CLI schematic 설정만 하고 끝내줘요
	좋습니다

# upgrade
현재 프로젝트를 최신 NestJS 버전에 맞게 마이그레이션합니다

잘 될지는 모르겠네요
흐음

이와 관련한 플래그는 다음과 같구요
- --skip-install
	이미 잘 설치되어 있을 수도 있잖아요
	스킵하는 플래그구요
- --no-observe
	최신으로 마이그레이션하는데 @nestjs/observe를 함께 추가하고 싶지 않은 경우 용이하겠네요

`update`로 적을 수도 있습니다

# generate
귀찮게 생성하고 이어 붙이고 할 시간을 아껴주는 아주 감사한 친구입니다

대략 이렇게 사용할 수 있겠는데
`nest g [want] [flags]`
그래서 무엇을 바로 생성 가능한지 아는 것도 중요하겠죠

이런 것들을 붙일 수 있구요
- resource
	CRUD가 가능한 전체 리소스를 바로 추가해줍니다
	module -> service -> controller와 DTO, 엔티티를 포함한다 생각하면 되겠네요
- module
- controller
- service
- 등등

이와 관련한 플래그는 다음과 같구요
- --no-spec
	spec은 대략적으로 단위 테스트 파일이라 생각하시면 됩니다
	추가하고 싶지 않다면 선택하세요
- --flat
	src에 흩뿌려서 추가하고 싶다면 추천합니다

`g`로 줄일 수 있습니다