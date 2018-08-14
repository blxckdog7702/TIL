# 향상된 연결 리스트  
배열 3개를 이용하여 연결리스트를 만든다.  
`0 ~ 100000` 범위의 값들이 있다면 연결리스트로 탐색하려 할 때 시간이 오래 걸린다.  
이를 해결하기 위해 `0 ~ 99`, `100 ~ 199`, `200 ~ 299`, `...` 범위로 나누어 연결 리스트를 구성한다.

선언  
```
int[] A;
int[] B;
int[] C;
int M;
A = new int[MAX / DIV + 5];
B = new int[MAX + 1];
C = new int[MAX + 1];
M = 1;
```  
`A` : `0 ~ 99` 등 구획을 담당하는 `HEAD` 배열이다.  
`B` : 같은 헤드 내에서 이전 값의 인덱스를 가지고 있는 `LINK` 배열이다. 0을 가지고 있으면 마지막 노드이다.  
`C` : B 배열과 1:1 매칭되서 실제로 데이터를 가지고 있는 `DATA` 배열이다.  

값 추가  
```
private void add(int value) {
  C[M] = value;
  B[M] = A[value / DIV];
  A[value / DIV] = M++;
}
```

값 삭제  
```
private void del(int value) {
	int preIndex = B[A[value/DIV]];
	B[A[value/DIV]] = 0;
	A[value/DIV] = preIndex;
	check[value] = false;
}
```
