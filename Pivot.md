# Pivot / Unpivot
## Pivot
행을 열로 회전

### Pivot절 구문
1. Aggregate_function : 집계할 컬럼 지정
2. For절 : Pivot 할 컬럼을 지정
3. In절 : Pivot 할 컬럼값을 지정

```
Pivot aggregate_function(집계할 컬럼) for [Pivot할 컬럼명] In [컬럼값]
```
ex. Pivot aggregate_function(Sum(급여)) for deptno In (10, 20, 30);


## Unpivot
열을 행으로 회전

### Unpivot절 구문
1. Unpivot column절 : Unpivot된 값이 들어갈 컬럼을 지정
2. For절 : Unpivot된 값을 설명할 값이 들어갈 컬럼을 지정
3. In절 : Unpivot할 컬럼 + 설명할 값의 리터럴 값 지정
4. Include nulls : unpivot된 열의 값이 널인 행도 결과에 포함


#### Pivot, Unpivot 을 사용할 수 없는 경우, Case 표현식 사용
