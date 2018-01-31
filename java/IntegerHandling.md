# Integer 클래스 다루기  

1. bitCount()  
2의 보수 체계에서 1의 개수를 리턴해준다.  
```  
Integer.bitCount(15); //4
```  

2. toBinaryString(), toHexString();
```  
Integer.toBinaryString(15); //1111
Integer.toHexString(15); //f
```  

3. unsignedInt  
```  
int vInt = Integer.parseUnsignedInt("4294967295");
System.out.println(vInt); // -1
String sInt = Integer.toUnsignedString(vInt);
System.out.println(sInt); // 4294967295
```  
Long도 마찬가지로 할 수 있다.

## 부록 : BigInteger  

1. 생성  
```
BigInteger b = new BigInteger("원하는 숫자");
```  

2. 변수  
```  
BigInteger.ZERO
BigInteger.ONE
BigInteger.TEN
```

3. 주요 메서드  
```  
add(Biginteger val)       // 더하기
subtract(Biginteger val)  // 빼기
mutiply(Biginteger val)   // 곱하기
devide(Biginteger val)    // 나누기
equals(Object x)          // 값이 같은지 비교
compareTo(BigInteger val) // val보다 크면 1, 같으면 0, 작으면 -1
toString()                // 10진수로 출력
toString(int n)           // n진수로 출력
valueOf(long n)           // n값과 같은 BigInteger 리턴
```
