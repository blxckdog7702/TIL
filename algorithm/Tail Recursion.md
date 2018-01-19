# 꼬리재귀  

재귀 함수는 코드가 짧아져서 가독성을 높일 수 있지만, 스택 오버 플로우를 일으킬 수 있다.  

함수를 호출할 때는 함수의 입력 값(매개변수), 리턴 값, 그리고 함수가 끝나고 돌아갈 위치 값 등을 스택에 저장한다.  

재귀 함수를 사용하면 함수가 끝나지 않은 채 연속적으로 함수가 호출되기 때문에 스택에 계속 메모리가 쌓이게 된다.  

그래서 함수를 호출하면서 스택에 쌓인 메모리가 스택의 용량을 초과하면 스택 오버 플로우 에러가 난다.  

이를 해결할 수 있는 방법 중 하나가 꼬리재귀(Tail Recursion) 이다.  

꼬리 재귀란, 재귀 호출이 끝난 후 '호출한' 함수에서 추가 연산을 요구하지 않도록 구현하는 재귀의 형태이다. 이를 이용하면 호출 스택이 깊어지는 문제를 컴파일어가 선형으로 처리할 수 있도록 알고리즘을 바꿔서 스택을 재사용할 수 있게 된다.  

물론 컴파일러가 이런 최적화 기능을 제공하는지 먼저 확인해야 한다.  

다음은 일반적인 재귀함수의 코드이다.  

```  
int Factorial(int n)
{
	if (n == 1) return 1;

	return n * Factorial(n-1);
}
```  
이 함수를 컴파일러는 다음과 같이 해석한다.  
```  
int Factorial(int n)
{
	if (n == 1) return 1;
	int result = Factorial(n - 1);

	return n * result;
}
```  

다음은 꼬리 재귀 함수의 코드이다.  
```  
int FactorialTail(int n, int acc)    // acc : accumulator의 약자
{
	if (n == 1) return acc;

 //  일반 재귀에서의 n * Factorial(n-1)와 달리 반환값에서 추가 연산을 필요로 하지 않음
	return FactorialTail(n - 1, acc * n);   
}

int Factorial(int n)
{
	return FactorialTail(n, 1);
}
```  
이 함수를 컴파일러는 다음과 같이 해석한다.  
```
int FactorialTail(int n)
{
 int acc = 1;

 do
 {
   if (n == 1) return;
   acc = acc * n;
   n = n - 1;
 } while (true);
}
```  

컴파일러가 함수의 내용을 선형적으로 바꿔서 처리한다.  

출처 : http://bozeury.tistory.com/entry/%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80-%EC%B5%9C%EC%A0%81%ED%99%94Tail-Recursion
