1. 외래키를 사용할 때 외래키를 사용하면서 얻는 장점과 단점은 무엇일까요?

> 문진수
>
> 외래키를 사용하면 데이터 무결성을 쉽게 보장할 수 있습니다. 특히 데이터의 참조 관계가 자주 변경되지 않는 경우에 유리합니다. 하지만 외래키 제약조건을 검사하는 데는 성능적인 비용이 들며 운영 환경에서 장애나 복구 상황이 발생했을 때 제약조건으로 인해 데이터 복구가 어려워질 수도 있습니다. 따라서 외래키의 사용 여부는 데이터의 특성을 고려하여 판단해야 합니다.

---
2. 외래키가 적용된 테이블에서 일어나는 데드락에 관해서 설명해주세요.

> 문진수
>
> 하나의 트랜잭션에서 자식 테이블을 Insert하고 부모 테이블의 컬럼을 변경하는 작업이 있는 경우 해당 트랜잭션이 동시에 여러개 들어오게 되면 데드락이 발생할 수 있습니다. InnoDB의 경우 자식 테이블의 Insert가 발생할 때 부모 테이블에 공유락이 걸리기 때문입니다.

---