# hashCode() 와 Equals()  

- equals 는 두 객체의 **내용** 이 같은지, 동등성(equality) 를 비교하는 연산자
- hashCode 는 두 객체가 같은 객체인지, 동일성(identity) 를 비교하는 연산자

- hashCode는 Heap에 있는 객체의 메모리 주소를 바탕으로 생성된다. 객체를 구별하기 위해서 고유한 정수 값을 출력해주는 메서드가 hashCode()다.

- 만약 사용자 객체를 만들었으면 equals()와 hashCode()를 오버라이딩해서 내용이 같은 두 객체를 서로 같은 객체로 인식하게 만들어야한다.

- 특히, HashMap, HashSet, HastTable과 같은 컬렉션은 객체를 받아들일 때, 객체의 동일성 비교를 hashCode()를 호출해서 실행한다.

- 한 글자 String의 hashCode() 값은 아스키코드 값이다. (2글자 부터는 길어짐)

**hashCode() 메서드의 구현**  
- Object 클래스 내부의 hashCode() 메소드 구현
```
public native int hashCode();
```
- String 클래스 내부의 hashCode() 메소드 구현
```
public int hashCode() {
       int h = hash;
       if (h == 0 && value.length > 0) {
           char val[] = value;

           for (int i = 0; i < value.length; i++) {
               h = 31 * h + val[i];
           }
           hash = h;
       }
       return h;
   }
```  
**31을 더하는 이유**  
31은 소수이면서 홀수이다. 소수를 사용하는 장점은
명확하지는 않지만 전통적이다.  
31이 좋은 속성은 곱셉 변화 및 성능 향상을 위한
감산에의해 대체될 수 있다.  
문자열의 각각 Byte의 ASCII 코드 공식을 통해 더해진
총합을 hash값으로 사용하고 있다.  

**중간에 객체의 값이 변경됐을 경우**
```
Map<Person, Integer> map = new HashMap<Person, Integer>();

Person p1 = new Person();
p1.setId(1);
p1.setName("Kally");
Person p2 = new Person(); p2.setId(1);

p2.setName("Sam");
map.put(p1, 1);
map.put(p2, 1);

p1.setName("Sam");

System.out.println(map.size()); // 2
```

Map 은 put() 하는 순간에 들어오는 오브젝트의 hashCode() 값을 기억하고 있으므로, name 이 변경된 뒤의 hashCode() 값을 인식하지 못한다.  

그러므로 equals() 나 hashCode() 에서 비교하는 멤버로 immutable을 사용할 수 없다면, mutable 한 멤버는 비교의 대상으로 사용해서는 안된다.

**hashCode는 어떻게 구현해야 하는가?**

>최악의 hashCode는 ```@Override public int hashCode(){return 42;}```
>이런 형태입니다. 이 형태는 동일한 객체들이 같은 해쉬 값을 갖게되므로 어떻게 보면 적법하다고도 할수 있지만 모든 객체가 다 똑같은 해쉬 값을 갖는 최악의 형태입니다. 이렇게 되면 모든 객체는 같은 버킷에 위치하고 새로 넣을때마다 계속 충돌이 발생해 링크드 리스트로 버킷을 연결해서 선형 구조가 되어 탐색과 삽입삭제가 엄청나게 느려지는 결과를 초래합니다.


### hashCode()와 관련된 규약  
1. equals() 로 비교시 두개의 오브젝트가 같다면, hashCode() 값도 같아야 한다.
1. equals() 로 비교시 false 라면, hashCode() 값은 다를수도, 같을수도 있다. 그러나 성능을 위해서는 hashCode() 값이 다른것이 낫다. 그래야 해싱 알고리즘으로 Set 에 해당 오브젝트가 존재하는지 아닌지 빠르게 검색할 수 있다.
1. hashCode() 값이 같다고 해서, eqauls() 가 true 를 리턴하는 것은 아니다. 해싱 알고리즘 자체의 문제로, 같은 해시값이 나올 수 있다.
