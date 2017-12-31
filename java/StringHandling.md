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

4. 일일이 sysout으로 찍는 것보다 StringBuilder에 넣어서 한 번에 찍는게 더 빠르다.

5. StringBuilder 개행문자 처리 방법.
  - 자바 7이후 : ```sb.append(System.lineSeparator());```
  - 기존 : ```sb.append(System.getProperty("line.separator"));```
