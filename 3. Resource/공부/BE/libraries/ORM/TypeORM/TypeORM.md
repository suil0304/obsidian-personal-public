---
노트 생성 시각: "2026년 11월 09일 19시 19분"
tags:
  - BE
  - ORM
  - 도구
---

Java 느낌으로 클래스를 이용해 설명하는 ORM이라 이해하시면 될 것 같구요
호오

얘네는 총 두 가지 사용 패턴을 지원합니다
Active Record와 Data Mapper인데
Data Mapper를 추천할게요

# Entity
*class decorator*

클래스를 엔티티로 만드는 느낌이라 생각하시면 됩니다

```TypeScript
@Entity("user")
class User {
	@PrimaryGeneratedColumn()
	id!:number;
	
	@Column()
	username!:string;
}
```

관련해서 여러 다른 데코레이터가 많다고 하네요

# Active Record
*class*

만약 엔티티 자체가 DB를 수정하게 하고 싶다 하면 @Entity 붙인 클래스에 추가로 extends BaseEntity를 추가하시면 됩니다

그 외에는 Data Mapper (Repository 이용)와 차이점이 별로 없어서 넘기다

# DataSource
*class*

```TypeScript
const dataSource = new DataSource({
    type: 'mysql',
    host: 'localhost',
    port: 3306,
    username: 'root',
    password: 'password',
    database: 'test'
});
```

이런 느낌으로 커넥션을 구축합니다

내부에 initalize라는 메서드가 있다고는 하는데
얘가 초기화를 하면서 연결을 수립한다고 하네요

귀찮으시면 차라리 url에 connection string을 즉석으로 꽂으시면 되겠습니다

# Repository
*variable / constant*

```TypeScript
const userRepository = dataSource.getRepository(User); // 반환 타입: Repository<User>

const user = userRepository.findOneBy({
	id: 1
});
```

이렇게 해서 직접 SQL를 작성하지 않고도 쿼리를 작성할 수 있습니다

복잡한 경우에는 userRepository.createQueryBuilder()로 체이닝 메서드 스타일 쿼리를 작성할 수 있습니다
그보다 더 복잡하면 dataSource.sql\`\`을 고려하세요

## TreeRepository
재귀적으로 자신의 엔티티 내부 속성이 자신의 엔티티를 가지는 경우입니다
이것을 ORM에서 읽기 쉬우라고 지원해주고 있구요

예시를 들자면 다음과 같습니다
```TypeScript
@Entity()
@Tree('closure-table')
export class Category {
    @PrimaryGeneratedColumn()
    id!:number;

    @Column()
    name!:string;

    @TreeChildren()
    children!:Category[];

    @TreeParent()
    parent!:Category;
}
```

또 @Tree에 들어가는 저장 방식 문자열도 총 4개가 있다고 하네요

|방식|특징|
|---|---|
|Closure Table|조상과 자손의 관계를 별도 테이블에 저장|
|Nested Set|노드의 좌우 범위를 이용해 계층 표현|
|Materialized Path|루트부터 현재 노드까지의 경로 저장|
|Adjacency List|각 노드가 부모의 ID를 보유|

# EntityManager
*variable / constant*

```TypeScript
const entityManager = dataSource.manager; // 다른 DB와 연결되는 QueryRunner를 통해 다른 EntityManager를 만들고 싶다면 dataSource.createEntityManager(queryRunner)를 사용하세요

const user = entityManager.findOneBy(User, {
	id: 1
});
```

여러 엔티티를 한 번에 사용할 수 있는 녀석입니다
한 번에 묶어서 한 트랜잭션 안에 요청할 때 용이할지도?