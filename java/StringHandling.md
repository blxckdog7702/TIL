# 문자열 처리 팁  

1. String의 특정 위치에 set하는 방법   
  - 방법 1 substring + "set할 문자" + 나머지 subString 이어붙이기  
  - 방법 2 stringBuilder.setCharAt(index, '?');  

2. 정규식을 이용한 ```split()``` 메서드 사용  
  - 영어 대문자 ```words = input.split("[A-Z]");```

3. ```isEmpty()```  
  - ```isEmpty(null);``` = 에러 발생;
  - ```isEmpty("");``` = true;
  - ```isEmpty(" ");``` = false;

4. 일일이 sysout으로 찍는 것보다 StringBuilder에 넣어서 한 번에 찍는게 더 빠르다.

5. StringBuilder 개행문자 처리 방법.
  - 자바 7이후 : ```sb.append(System.lineSeparator());```
  - 기존 : ```sb.append(System.getProperty("line.separator"));```

6. ```String.indexOf(int ch)```  
  - 문자열 내 특정 문자의 인덱스를 알려준다. 여러개가 있으면 첫 인덱스를 알려주고, 없으면 -1을 리턴한다.

7. 문자열 내에 특정 문자 개수 알아내는 법  
```
String word = "I love you".toLowerCase();
int count = word.length() - word.replace("o", "").length();
//결과는 2
```

8. 문자열 뒤집기
```
StringBuilder sb = new StringBuilder();
sb.reverse();
```
