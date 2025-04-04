

1. 데이터베이스의 인덱스에 대해서 설명해주세요.

> 문진수
>
> 인덱스는 데이터를 효율적으로 조회하기 위해 사용되는 자료구조입니다. MySQL의 경우 B+Tree를 기본으로 사용하여 주어진 키 순서로 정렬하여 저장합니다. CUD 성능을 희생하고 R의 성능을 극대화하는 목적으로 사용됩니다. 서비스의 특성을 고려하여 Read, Wrtie 비율을 적절하게 따져서 인덱스를 설정하는 것이 중요합니다.

---

2. MySQL에서 B+Tree의 구조에 대해서 설명해주세요.

> 문진수
>
> B+Tree는 이진 트리를 확장하여 각 노드가 N개의 자식을 가질 수 있는 균형 트리입니다. 각 노드는 값과 주소를 저장하는 페이지 단위로 구성되어 있으며 데이터를 조회할 때는 페이지 단위로 디스크에서 읽어오기 때문에 하나의 페이지에 가능한 한 많은 키를 저장하는 것이 성능에 유리합니다. 따라서 키의 크기는 가급적 작게 설정하는 것이 좋습니다. 또한 B+Tree는 리프 노드들끼리 연결 리스트로 되어 있어 순차 접근 성능이 뛰어납니다.

---

3. 인덱스에서 B+Tree 구조 대신 트리 구조나 Hash 구조를 사용하지 않는 이유는 무엇이라 생각하시나요?

> 문진수
>
> B+Tree가 인덱스 구조로 많이 사용되는 이유는 범위 검색과 특정 키 값으로 정렬됨에 있습니다. hash는 자료구조 특성상 Range Scan이 불가능하기 때문에 기본 인덱스로 채택하기에는 어려움이 있습니다. 물론 자주 조회되는 값들에 대해서 어뎁티브 해시 인덱스를 메모리에 만들어둠으로써 일부 조회 성능을 높일 수는 있습니다. 트리 구조는 깊이가 많이 깊어져 Disk I/O가 많이 발생할 수 있습니다. 일반적인 트리 구조의 경우 Depth가 깊어져서 Disk I/O가 많이 발생하여 성능상으로 B+Tree가 유리합니다.

4. 클러스터 인덱스와 세컨더리 인덱스의 차이는 무엇인가요?

> 문진수
>
> 클러스터 인덱스는 실제 데이터가 물리적 저장소에 순서대로 정렬되어 저장되는 인덱스입니다. PK에 대해 생성되며 이 인덱스의 리프 노드에는 실제 데이터 레코드가 저장되어 있습니다. 즉 인덱스 자체가 데이터를 포함하고 있어 별도의 추가 탐색 없이 원하는 데이터를 빠르게 조회할 수 있습니다. 특히 PK 기준의 Range Scan에 매우 효율적입니다. 반면 세컨더리 인덱스는 클러스터 인덱스와 달리 데이터의 물리적 정렬과는 무관합니다. B+Tree 구조로 인덱스 키 값만 정렬되어 있으며 리프 노드에는 해당 레코드의 PK가 저장됩니다. 실제 데이터를 조회하기 위해선 이 PK를 이용해 클러스터 인덱스를 한 번 더 타고 들어가는 과정을 거치므로 Disk Random I/O가 추가로 발생합니다.

---

5. 유니크 인덱스와 세컨더리 인덱스의 차이는 무엇인가요?

> 문진수
>
> 유니크 인덱스와 세컨더리 인덱스는 사실상 거의 동일합니다. 유니크 인덱스의 경우 중복 체크를 위해 체인지 버퍼를 사용하지 못하기 떄문에 값이 변경하는 비용이 상대적으로 큽니다. 조회 성능에서는 일반적으로 세컨더리 인덱스에서 유니크 인덱스에 비해 추가적으로 하는 작업은 CPU에서 컬럼이 같은지 비교하는 것이지 Disk I/O가 아니기 때문에 성능 차이가 미미합니다. 만약 다른 페이지의 데이터를 읽는 것이라면 추가적인 Disk I/O가 발생할 수는 있습니다. 유니크 인덱스 같은 경우 효율적으로 중복 체크를 해주기 때문에 적절하게 사용하면 좋습니다.