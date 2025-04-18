1. 데이터 베이스의 이상 현상에 대해서 설명해주세요.

> 문진수
>
> DB 이상현상은 삽입, 삭제, 수정할 때 발생하는 오류들을 말합니다. 삽입 이상은 데이터를 삽입할 때 의도하지 않은 데이터를 함께 삽입하지 않으면 삽입되지 않는 것을 말합니다. 갱신 이상은 중복된 데이터 중에서 일부만 수정ㅎ되어 데이터의 모순이 발생하는 것을 말합니다. 삭제 이상은 데이터를 삭제할 때 의도하지 않은 데이터까지 함께 삭제되어야 하는 것을 말합니다.

> 백명규
> 
> 데이터 베이스의 이상 현상에는 삽입 이상, 삭제 이상, 갱신 이상이 있습니다. 
> 이러한 이상 현상이 일어나는 이유는 데이터의 중복 때문입니다. 
> 한 예로 갱신 이상의 경우 서울 16반이 604호의 호실을 결정짓는데 각각의 A, B, C라는 사람에 대해 서울 16반 604호라는 데이터를 모두 가지고 있다면 
> 서울 16반의 호실이 변경되는 경우 모든 인원에 대해서 변경하지 않고 일부만 변경된다면 데이터의 일관성이 깨지게 됩니다. 
> 따라서, 이런 문제를 해결하기 위해서는 적절하게 정규화를 적용하여 결정자에 따른 데이터 종속성을 파악하여 중복을 제거하는 정규화 과정을 거쳐야 합니다.
> 
> ※ 짧게 예시 부분을 이야기 안해놔도 대충 알아듣긴 하는 거 같음.

---
2. 데이터베이스의 정규화에 관해서 설명해주세요.

> 문진수
>
> 정규화는 이상현상이 발생하는 릴레이션을 분해하여 이상현상을 없애는 작업을 말합니다. 즉 테이블간의 중복을 없애는 과정입니다. 제1정규화는 테이블의 컬럼이 원자값을 가지도록 만드는 것을 말합니다. 제2정규화는 제1정규화를 진행한 테이블에 대해서 완전 함수 종속을 만드는 과정입니다. 완전 함수 종속이란 기본키의 부분집합이 결정자가 되지 않는 상태를 말합니다. 제3정규화는 제2정규화를 마친 테이블에 대해서 이행적 종속을 제거하는 과정입니다. 이행적 종속이란 기본키가 아닌 컬럼이 결정자가 되는 것을 말합니다.

> 백명규
> 
> 정규화는 관계형 데이터베이스에서 테이블 설계에 있어 중복된 데이터를 제거하는 과정이라고 생각을 합니다. 
> 이런 정규화 과정을 제대로 거치지 않는다면 데이터의 중복으로 인해 데이터의 삽입, 삭제, 변경 과정에서 일관성이 깨지는 이상 현상이 발생하게 됩니다. 
> 따라서 테이블에서 설계를 하는 과정에 있어 반드시 결정자에 따른 데이터 종속성을 파악한 뒤 중복을 제거하는 과정을 거쳐야 합니다.
> 
> ※ 보통은 이렇게 직접적으로 묻기보단 데이터베이스에 대해서 자신있다. 혹은 데이터베이스를 관련해서 좀 공부를 해봤다고 하면 테이블 설계와 관련해서
> 고려하는 점들에 관해서 물어볼 때 곁다리로 말하게 되는 경우가 많은 것 같음.

---
3. 트랜잭션의 격리 수준에 대해서 설명해주세요. 
본인이 마지막으로 진행한 프로젝트에선 어떤 격리 수준을 골랐고 그 격리 수준에선 어떤 문제가 발생할 수 있지 말씀해주세요.

> 문진수
>
> 격리 수준에는 크게 READ UNCOMMITED, READ COMMITED, REPEATABLE READ, SERIALIZABLE이 있습니다. READ UNCOMMITED는 커밋되지 않은 TX의 변경 사항을 다른 TX에서 읽을 수 있는 Dirty Read가 발생하여 데이터베이스의 무결성을 보장할 수 없습니다. READ COMMITED는 커밋된 데이터는 다른 TX에서 읽을 수 있습니다. TX 진행중에 다른 TX에서 커밋을 하게 되면 이 부분은 읽을 수 있기에 동일한 쿼리에 없었던 행이 추가되는 팬덤 리드가 발생하거나 이전에 값과 다른 값이 조회되는 현상(UNREPEATABLE READ)이 발생할 수 있습니다. REPEATABLE READ에서는 동일 TX에서 값을 읽을 때 현재 TX 번호보다 낮은 TX 번호의 내역만 undo 로그에서 읽기 때문에 READ COMMITED에서 발생했던 문제가 생기지 않습니다. SERIALIZABLE의 경우 모든 TX를 순차적으로 실행시키기 때문에 충돌에 의한 문제가 발생하지 않지만 동시 처리 속도가 굉장히 느려집니다.
>
> 마지막으로 사용했던 프로젝트에서는 MySQL의 기본 격리 수준인 REPEATABLE READ를 사용했습니다. 문제가 발생할 수 있는 유일한 케이스는 동일한 레코드를 읽을 때 SELECT → 다른 TX 커밋 → SELECT FOR UPDATE를 할 경우입니다. undo log는 append only 파일이기 때문에 락을 적용할 수 없어서 버퍼 풀에서 데이터를 읽기 때문에 다른 TX의 커밋을 읽게 되며 SELECT 했을 때와 다른 데이터가 조회될 수 있습니다.

---
4. 프로시져(PROCEDURE)에 관해서 설명해주세요. 프로시져를 통해 얻을 수 있는 장점과 단점은 뭘까요?

> 문진수
>
> 프로서저는 작업을 수행하기 위한 명령어들을 모아둔 것을 말합니다. 장점으로는 하나의 네트워크 I/O로 여러 쿼리를 수행할 수 있기 때문에 효율적입니다. 다만 가독성이 매우 떨어지고 디버깅이 굉장히 어렵기 때문에 유지보수가 어렵습니다.

---