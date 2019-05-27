# OpenSSH 사용방법  
- ssh 연결 방법  
`ssh userId@hostAddress`  
- ssh with port  
`ssh userId@hostAddress:port`
- local port forwarding  
local 에서 SSH Tunnel을 거쳐 서버에 있는 Application에 접근할 때 쓴다.  
`ssh -L localPort:host_name:remotePort server_name`  
AWS RDS를 쓴다면 다음과 같이 쓰면 된다.  
`ssh -L localDBPort:Rds:RdsPort jumphost`  

- remote port forwarding  
반대로 Remote 에서 local에 있는 Application에 접근할 때 쓴다.  
아직 공용IP 주소가 없어서 인터넷을 통해 직접 연결할 수 없을 때 local이 서버가 되고, remote가 클라이언트가 되어 remote에 연 포트로 오는 모든 트래픽은 SSH에 의해 암호화되어 local로 전송되고, 다시 local에서 destination으로 전송된다.  
`ssh -R localPort:destinaion_name:destPort server_name`  
만약 로컬에서 웹 앱을 개발중인데 친구에게 보여주고 싶다면  
`ssh -R localPort:WebApp:WebAppPort friend's_server`    
