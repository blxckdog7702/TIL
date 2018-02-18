# 제네릭(Generics)  

## 제네릭이란?  
컬렉션 클래스, 클래스, 메서드에 컴파일 시의 타입 체크를 해주는 것.  
클래스 내부에서 사용할 데이터 타입을 나중에 인스턴스를 생성할 때 확정하는 것.  

## 제네릭의 장점  
1. 타입 안정성 제공  
  - 의도하지 않은 타입의 객체를 저장하는 것을 막고, 객체를 꺼내올 때 형변환에서 발생할 수 있는 오류를 줄여준다.
2. 코드 간결화
  - 객체를 꺼내올 때 형변환 과정이 필요없기 때문에 코드가 간결해진다.

## 제네릭 타입  
타입을 파라미터로 가지는 클래스와 인터페이스를 말한다.  

```  
public class Box<T> {
    private T t;

    public T get() { return t; }
    public void set(T t) { this.t = t; }
}
```  

```  
Box<String> box = new Box<String>();
```  

위와 같이 선언하면 내부는 다음과 같이 재구성되서 인스턴스화 된다.  

```  
public class Box<String> {
    private String t;

    public String get() { return t; }
    public void set(String t) { this.t = t; }
}
```  

## 컬렉션에서 제네릭 이전의 문제점  
제네릭을 사용하지 않으면 컬렉션 안에 추가되는 객체는 모두 `Object` 타입으로 들어간다. 컬렉션에 값을 추가할 때는 문제가 되지 않지만 꺼낼때는 다음과 같이 형변환을 해야했다.

```  
String hello = (String) aList.get(0); // Object를 String으로 캐스팅.
```

또한 추가할때 원하는 클래스가 아니여도 문제가 되지 않기 때문에, 잠재적으로 형변환 오류 가능성을 가지고 있었다.

## 컬렉션 사용 예  
```  
ArrayList<String> aList = new ArrayList<String>();
aList.add("test");
aList.get(0); // 형변환 필요없음
```  

위와 같이 사용하고 `<>` 안에 들어가는 건 **참조 타입** 만 들어갈 수 있다. 그래서 `int` 나 `long` 같은 원시형 변수 대신 `Integer` 나 `Long` 같은 wrapper 클래스를 이용해야 한다.

## 다형성 사용 예  
제네릭 타입을 부모 타입으로 정하면 자식 타입도 추가할 수 있지만, 꺼낼때는 형변환이 필요하다.  

```  
class Product{ }
class Tv extends Product{ }

//Product 클래스의 자손객체들을 저장할 수 있는 ArrayList를 생성
ArrayList<Product> list = new ArrayList<Product>();

list.add(new Product());
list.add(new Tv());

Product p = list.get(0);// 형변환이 필요없다.
Tv t = (Tv)list.get(1);// 형변환을 필요하다.
```  

## 와일드카드  
보통 제네릭에서는 하나의 타입만 지정하지만 와일드 카드를 지정하면 매개변수의 다형성을 이용할 수 있다.  

```
// Product 또는 그 자손들이 담긴 ArrayList를 매개변수로 받는 메서드.
// 인터페이스도 마찬가지로 extends 키워드를 사용한다.
public static void printAll(ArrayList<? extends Product> list){
}
```

## 복수의 제네릭  
```  
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}

class Person<T, S>{//복수의 제네릭을 사용할 시에는 ','를 사용한다.
    public T info;
    public S id;
    Person(T info, S id){
        this.info = info;
        this.id = id;
    }
}

public class GenericDemo {
    public static void main(String[] args) {
        Person<EmployeeInfo, int> p1 = new Person<EmployeeInfo, int>(new EmployeeInfo(1), 1);
    }
}
```

## 메서드에 적용  
```  
// U 데이터 타입은 info라는 매개변수의 데이터타입(EmployeeInfo)이 된다.
public <U> void printInfo(U info){
      System.out.println(info);
}

p1.<EmployeeInfo>printInfo(e);
p1.printInfo(e);// 제네릭 생략이 가능함
```  

출처 : http://devbox.tistory.com/entry/Java-%EC%A0%9C%EB%84%A4%EB%A6%AD  
