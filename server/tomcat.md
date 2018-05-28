# 톰캣 관련  
1. 톰캣의 기본 Root context는 `tomcat/webapps`이다.
1. war 파일을 올리는 이유
```
FTP로 올릴 때 압축해서 올리면 압축을 일일이 해제해야 하는데
WAR 파일로 올리면 개발 서버의 경우 Tomcat이 알아서 압축을 해제해서
배포해주기 때문이다.
```
3. 톰캣 버전 확인  
tomcat 설치 경로/lib으로 이동 후 다음 커맨드 입력  
`java -cp catalina.jar org.apache.catalina.util.ServerInfo`  
