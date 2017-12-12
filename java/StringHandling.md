# 문자열 처리 팁  

1. String의 특정 위치에 set하는 방법   
  - 방법 1 substring + "set할 문자" + 나머지 subString 이어붙이기  
  - 방법 2 stringBuilder.setCharAt(index, '?');  

2. 정규식을 이용한 ```split()``` 메서드 사용  
  - 영어 대문자 ```words = input.split("[A-Z]");```

3. ```isEmpty()```  
  - ```isEmpty(null);``` = true;
  - ```isEmpty("");``` = true;
  - ```isEmpty(" ");``` = false;
