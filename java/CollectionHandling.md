# 컬렉션 처리 팁  

1. 개수 세기
  - ```Collections.frequency();```
  - ```int count = Collections.frequency(컬렉션, 값);```
  - 맵의 경우에는 ```컬렉션``` 자리에 ```map.values();```

2. 최대
  - ```Collections.max();```
  - ```Entry<Character, Integer> maxEntry = Collections.max(map.entrySet(), (entry1, entry2) -> entry1.getValue() - entry2.getValue());```

  >Entry는 map안의 key-value 한 쌍을 이야기한다. getKey, getValue가 가능하다.

  여기서 Comparable의 compare 함수를 람다식으로 구현했다.

  자바 8이전엔 익명 클래스를 이용하여 Comparable을 구현했다면,
  ```
Collections.sort(listDevs, new Comparator<Developer>() {
      @Override
	  public int compare(Developer o1, Developer o2) {
        return o1.getAge() - o2.getAge();
      }
});
  ```

  자바 8에서는 람다식을 이용하여 다음과 같이 구현한다.
  ```
  listDevs.sort((Developer o1, Developer o2)->o1.getAge()-o2.getAge());
  ```  
  참고로 이거 반대로 빼면 거꾸로 정렬된다.  

3. 간편 출력  
  - ```coll.forEach((obj)->System.out.println(obj));```

4. for-each 중 요소 삭제  
for-each 중 컬렉션의 요소를 삭제하면 에러가 난다. 다음과 같이 구현하면 안전하게 사용가능하다.
```  
List<String> names = ....
Iterator<String> i = names.iterator();
while (i.hasNext()) {
   String s = i.next(); // must be called before you can call i.remove()
   // Do something
   i.remove();
}
```

5. 컬렉션 성능비교  
**Vector vs List**  

`Vector`는 동기화를 지원하여 `List`에 비해 다소 느리다.  
`List`는 동기화를 지원하지 않는다. `Synchronized Wrapper` 클래스를 이용하여 동기화 이용 가능하다.  

**ArrayList vs LinkedList**  
`ArrayList`는 검색에 유리, 삽입/삭제에 불리. (특히 삭제연산에 많은 시간 소요)  
`LinkedList`는 검색에 불리, 삽입/삭제에 유리.  

`ArrayList`는 생성시 초기 크기를 지정해줘야 capacity를 늘리면서 성능저하가 발생되지 않는다. 물론 초기 크기를 너무 크게 할당해도 오버헤드가 된다.  
크기를 늘릴때 `Vector`는 100%, `ArrayList`는 50% 씩 늘린다.  
