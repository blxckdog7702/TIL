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
