1. inner join과 outer join의 차이에 관해서 말씀해주세요.

> 문진수
>
> Inner Join은 조인 컬럼 값이 동일한 조합에 한해서 결과 집합에 포함됩니다. 만약 기준 테이블에 레코드가 존재하더라도 조인 대상 테이블에 일치하는 값이 없으면 결과 집합에서 제외됩니다. 반면 Outer Join의 경우 Left, Right Outer join이 일반적으로 사용되는데 주 테이블의 레코드를 기준으로 모든 결과는 기본으로 다 포함되게 됩니다. Full Outer Join도 있는데 이는 왼쪽 집합에 존재하지만 오른쪽 집합에 존재하지 않는값, 오른쪽 집합에 존재하지만 왼쪽 집합에 존재하지 않는 값도 모두 결과 집합에 포함되어 나옵니다.

---
2. HAVING절과 WHERE 절의 차이는 무엇인가요? 
그러면 ANSI SQL에서 GROUP BY절에 없는 데이터를 HAVING 절이나 SELECT 절에 사용할 수 있나요?

> 문진수
>
> SELECT 문의 쿼리 실행 순서를 살펴보면 FROM, JOIN, WHERE, GROUP BY, HAVING, SELECT, ORDER BY로 수행됩니다. WHERE절의 경우 GROUP BY 전에 실행되며 모든 대상 테이블의 레코드에 대해서 조건이 걸립니다. 반면 HAVING은 WHERE 절에서 필터링되고 GROUP BY에 의해서 그룹핑된 데이터에 대해서 조건을 적용하게 됩니다.

---
3. SELECT 절로 데이터를 조회해올 때 쿼리에서 우선 적용되는 절에 관해서 순서대로 말씀해주세요.

> 문진수
>
> SELECT 문의 쿼리 실행 순서를 살펴보면 FROM, JOIN, WHERE, GROUP BY, HAVING, SELECT, ORDER BY, LIMIT 순서로 실행됩니다.

---
4. UNION, UNION ALL, INTERSECT에 관해서 설명해주세요. ANSI SQL과 MySQL에선 각각의 절이 사용이 가능한가요?

> 문진수
>
> UNION은 SELECT로 조회한 데이터를 합치는데 중복을 제거한 후 결과가 나옵니다. UNION ALL의 경우 중복을 제거하지 않고 가져옵니다. 중복 체크가 없기에 성능상 이점이 있습니다. INTERSECT의 경우 두 집합의 교집합, 즉 같은 데이터만 가져오게 됩니다. MySQL에서는 INTERSECT가 없기 때문에 JOIN, EXISTS를 조합하여 쿼리를 작성해야 합니다.

---
5. GROUP BY에서 NULL로 처리된 데이터는 집계에서 어떻게 처리되나요?

> 문진수
>
> NULL도 하나의 값으로써 다른 값들과 동일하게 하나로 묶여서 집계됩니다.

---
6. DISTINCT에 관해서 설명해주세요. 어떤 절에 사용할 수 있고, 
DISTINCT에는 인덱스가 적용이 되나요? 그리고 ANSI SQL에서 DISTINCT는 SELECT에서 하나의 컬럼에만 설정할 수있나요?

> 문진수
>
> DISTINCT는 중복을 제거하는 역할을 하지만 결과를 정렬하지는 않습니다. SELECT 되는 전체 레코드의 조합이 유일하도록 가져오는 것이지 하나의 컬럼만 유니크하게 가져오는 것은 아닙니다.

---