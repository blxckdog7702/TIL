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

2차원 배열은  
```
Arrays.sort(input, (a, b) -> Integer.compare(a[0], b[0]));
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

4. 배열 복사  
- ```System.arrayCopy();```
```
int[] arr = {1,2,3,4,5};

int[] copied = new int[10];
System.arraycopy(arr, 0, copied, 1, 5);//5 is the length to copy

System.out.println(Arrays.toString(copied));
```
- ```Arrays.copyOf()```
```
int[] copied = Arrays.copyOf(arr, 10); //10 the the length of the new array
System.out.println(Arrays.toString(copied));

copied = Arrays.copyOf(arr, 3);
System.out.println(Arrays.toString(copied));
```

`Arrays.copyOf` 는 요소를 복사할 뿐 아니라, `System.arrayCopy()`를 이용하여 새로운 배열을 만든다.  
`Arrays.copyOf` 소스 내부에서 `System.arrayCopy()` 를 이용한다.
```
public static int[] copyOf(int[] original, int newLength) {
   int[] copy = new int[newLength];
   System.arraycopy(original, 0, copy, 0, Math.min(original.length, newLength));
   return copy;
}
```
