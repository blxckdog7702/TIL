# 자바 인자 전달 방식  

**기본지식**  
  - parameter : formal-parameter(형식 인자)
  - argument : actual-parameter(실인자)

```
public void doSomething(int something);
```
위 코드의 변수 somthing은 paramter이다.  

```
int ten = 10;
doSomething(ten);
```  
위 코드의 변수 ten은 argument이다.  

**결론**  
자바는 기본적으로 '값에 의한 전달'이다. 하지만 레퍼런스 타입의 경우 전달되는 값이 레퍼런스이다. ('참조에 의한 전달'과 다름)  

참조 타입일 때, 해당 객체의 레퍼런스를 직접 넘기는 것이 아니라, 같은 메모리를 가리키는 새로운 레퍼런스를 만들어서(복사해서) 넘겨준다.  

그래서 다음 코드와 같은 차이가 나타나는 것이다.  

```
public static void main( String[] args ) {
    Dog aDog = new Dog("Max");
    // we pass the object to foo
    foo(aDog);
    // aDog variable is still pointing to the "Max" dog when foo(...) returns
    aDog.getName().equals("Max"); // true, java passes by value
    aDog.getName().equals("Fifi"); // false
}

public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // change d inside of foo() to point to a new Dog instance "Fifi"
    d = new Dog("Fifi");
    d.getName().equals("Fifi"); // true
}
```  
위 코드는 값이 그대로 "Max"로 유지된다.  

```  
public static void main( String[] args ) {
    Dog aDog = new Dog("Max");
    foo(aDog);
    // when foo(...) returns, the name of the dog has been changed to "Fifi"
    aDog.getName().equals("Fifi"); // true
}

public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // this changes the name of d to be "Fifi"
    d.setName("Fifi");
}
```  
위 코드는 값이 "Fifi"로 바뀐다.
