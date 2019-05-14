# 리눅스 명령어 모음  

### 검색   
- 파일명으로 검색하기
find [경로] [-name] [파일 명]  
 `find ./ -name mysql.sock`  

- 작동중인 프로세스
`ps -ef | grep tomcat`  

- 하위폴더까지 모두 삭제
`rm -rf folderName`  

- netstat으로 LISTEN 확인
`netstat -tnlp`  
`netstat -anp | grep LISTEN | grep tcp`  

- ssh : ssh -p 포트 -i 인증파일 user@address  

- tcp 와 tcp6는 IPv4 IPv6 차이이다.  

- 리눅스 ssh는 기본으로 22번 포트를 사용하고 EC2 인스턴스를 만들면 이를 열어준다.  
- Well-known 포트를 피해 다른 포트로 열어주려면 설정을 바꾸어야 한다.  
- ssh와 tcp 계층에 대해서 조사하기
