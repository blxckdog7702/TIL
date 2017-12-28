# 자바 EOF 처리  

Scanner
```
Scanner sc = new Scanner(System.in);

while(sc.hasNextLine()) {
  sc.nextLine();
}

while(sc.hasNextInt()) {
  sc.nextInt();
}
```

BufferedReader
```
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String input = "";
while((input = br.readLine()) != null) {
  //......
}
```

콘솔에서 EOF를 입력하려면 `ctrl + z` 를 누르면 된다.
