# 리눅스 명령어 모음  

### 검색   
- 파일명으로 검색  
find [경로] [-name] [파일 명]  
 `find ./ -name mysql.sock`  

- 파일명으로 검색  
locte [파일 명]  
`locate *.log`  
locate 명령은 디렉토리를 뒤지지 않는다. DB에서 검색한다. 이 컵퓨터의 파일들에 대한 DB가 따로 존재하는데, 거기서 찾는다.  
그 DB이름은 mlocate이다. mlocate 안의 파일 목록은 `sudo updatedb` 명령을 통해 업데이트 가능.  

- 경로 검색  
whereis [명령어]  
`whereis ls`   

### 프로세스  
- 작동중인 프로세스
`ps -ef | grep tomcat`  
`ps -ef | grep `  

- 실행중 프로그램을 백그라운드로 보내는 단축키  
`^ + z`  

- 백그라운드로 보내졌던 프로그램을 다시 포어그라운드로 보내는 단축키  
`fg`  

- 백그라운드에 있는 프로세스를 확인하는 단축키
`jobs`  
job 앞에 +가 붙은게 fg시 나오고, -가 붙은건 +가 없어지면 이어서 +가 된다.  
앞에 붙은 번호로 fg하고 싶으면 `fg %번호` 로 호출하면 됨

- 명령어가 실행될 때 백그라운드로 실행하려면 뒤에 &를 붙이기  
`ls&`

### 정기적 작업  
cron
`crontab -e` 해서 작업 정의하는 에디터로 들어감.  
m h dom mon dow command 정의  
*/1 : 매 1분
10 1 : 1시 10분

m : minute (0 - 59)
h : hour
dom : day of month (1 - 31)
mon : month (1 - 12)
dow : day of week (0 - 6) sunday = 0

### 서비스, 데몬  
- 아파치 on/off   
`sudo service apache2 start`  
`sudo service apache2 stop`  

### 삭제
- 하위폴더까지 모두 삭제
`rm -rf folderName`  

### 네트워크
- netstat으로 LISTEN 확인
`netstat -tnlp`  
`netstat -anp | grep LISTEN | grep tcp`  

- tcp 와 tcp6는 IPv4 IPv6 차이이다.  

- 리눅스 ssh는 기본으로 22번 포트를 사용하고 EC2 인스턴스를 만들면 이를 열어준다.  
- Well-known 포트를 피해 다른 포트로 열어주려면 설정을 바꾸어야 한다.  
- ssh와 tcp 계층에 대해서 조사하기

### 다중 사용자, 권한  
- 자신이 누구인지?  
`id`  

- 현재 이 시스템에 누가 접속해있는지?  
`who`  

- super user  
`su`  

- 유저 생성  
`sudo adduser -m whitedog`  
-m은 홈폴더까지 같이 생성  

- 유저 비번 설정  
`sudo passwd whitedog`  

- 유저 변경  
`su - whitedog`  

- 유저 권한 변경  
sudo 권한 부여  
`sudo usermod -a -G sudo whitedog`  

- 읽기 쓰기 권한 변경  
`chmod u+rwx` : owner  
`chmod g+rwx` : group  
`chmod o-rwx` : other  
`chmod u+a` : owner all  
`chmod -R dir` : dir 하위에도 모두 적용  

  그외 숫자로 지정하는 방법도 있다. 
