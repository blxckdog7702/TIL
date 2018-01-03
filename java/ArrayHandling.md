# 배열 처리 팁  

1. 배열 초기화  
  - 1차원 배열은 ```Arrays.fill(arr, ' ');``` 을 하면 된다.
  - 2차원 배열은 다음과 같다.
  ```
  for (int i = 0; i < n; i++) {
          Arrays.fill(arr[i], ' ');
      }
  ```
2. 정렬
```
Arrays.sort(arr);
```

3. 간편 출력  
- Java8
```
Arrays.stream(arr).forEach(n -> System.out.print(n + " "));
```
결과는 ```1 2 3 4 5 ...```
- toString()
```
int[] intArray = new int[] {1, 2, 3, 4, 5};
System.out.print(Arrays.toString(intArray));
System.out.print(Arrays.deepToString(intArray));
```
결과는 ```[1,2,3,4,5]```

> toString() vs deepToString()
> toString()은 1차원 배열에서만 사용 가능.
> deepToString()은 1차원, 다차원 모두 사용 가능. 하지만 원시형 변수 1차원 배열에선 에러
