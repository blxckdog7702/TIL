# 클린 코드  
## 목차  

* [2장 의미있는 이름](#2장-의미있는-이름)
* [3장 함수](#3장-함수)  

## 2장 의미있는 이름  
##### 의도를 분명하게 밝혀라  
```
int daySinceCreation;
int elapsedTimeInDay;
int fileAgeInday;
```  

`str1, str2` 대신 `source, destination`을 쓰면 가독성 up

##### 검색하기 쉬운 이름을 써라  
- 통상적으로 이름이 길어질수록 검색하기 쉽다.

##### 인코딩을 피하라  
- 헝가리안 표기법처럼 타입을 변수명에 넣을 필요가 없다.
- 멤버 변수 접두어 넣을 필요 없다. `m_name`
- 인터페이스와 구현 클래스는 `IShapeFactory` 처럼 인터페이스에 표시해주기 보다는 구현 클래스에 `ShapeFactoryImpl` 이라고 나타내는게 낫다.

##### 클래스나 객체 이름  
- 클래스나 객체 이름은 명사나 명사구
- Manager, Processor, Data, Info 등과 같은 단어는 피한다.

##### 메서드 이름  
- 메서드 이름은 동사나 동사구
- set, get, is는 javabean 표준에 따라서 붙인다.
- 생성자를 중복정의 할 때는 정적 팩토리 메서드 이용
```
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
Complex fulcrumPoint = new Complex(23.0);
```
아래 코드보다 위 코드가 좋다.

##### 일관성있는 어휘 사용  
- fetch, retrieve, get을 섞어쓰면? 복잡하지

##### 말장난을 하지 마라  
- add는 둘을 더하는거고, A에 B를 넣는것은 insert나 append라는 이름을 쓰자.

## 3장 함수  
##### 작게 만들어라!  
- if/else/while 등에 들어가는 블록은 한 줄이여야 한다.

##### 함수 당 추상화 수준은 하나로  
- 같은 함수 내에서 추상화 수준이 뒤죽박죽 섞이면 파악하는데 헷갈림

##### Switch case?  
- switch 문은 추상 팩토리 클래스를 구현해서 그 안에 숨긴다.

##### flag 인수는 추하다?  
- 메서드 안에서 이것저것 많이 한다고 공표하는 셈이라 추하다?

##### 부수 효과를 일으키지 마라?  
- 함수에서 한 가지를 하겠다고 명시했는데 그 안에 다른 처리도 끼어들어가 있는 것.

##### 출력 인수  
- 일반적으로 출력 인수는 피해야 한다. 함수에서 상태를 변경해야 한다면 함수가 속한 객체 상태를 변경하는 방식을 택한다.  
```
appendFooter(s);
public void appendFooter(StringBuffer report);
```
위 코드만 보고 s가 무엇인지 위해서 함수 선언부를 찾아보게 된다.
그러므로 아래 코드처럼 바꾸는게 좋다.  
```
report.appendFooter();
```

##### trycatch  
- try/catch 블록은 별도 함수로 뽑아내는 편이 좋다.
- 정상 동작과 오류처리 동작을 분리한다.
