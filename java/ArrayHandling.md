# 배열 처리 팁  

1. 배열 초기화  
  - 1차원 배열은 ```Arrays.fill(arr, ' ');``` 을 하면 된다.
  - 2차원 배열은 다음과 같다.
  ```
  for (int i = 0; i < n; i++) {
          Arrays.fill(arr[i], ' ');
      }
  ```
