# Azure Discovery Day 101  
#### 클라우드메이트, Azure MVP 김세준 님  

## 클라우드를 쓰는 이유?
- 대량의 가용성(고 가용성(DR), 민첩성, 탄력성, 확장성)
- 유연한 예산 운용(근데 IDC에서도 서버 대여 해주는 걸? 하지만 그들은 구매를 목적으로 대여해준다. 자동차 장기 리스 해주듯이)

### 규모의 경제  
규모가 작을 때 보다 대규모로 운영 할 때 비용이 적게 들고 효율적으로 일할 수 있는 능력 -> 구글, 아마존, MS가 이렇게 제공

한대든 여러대든 관리 방법은 똑같으니까 양 많으면 싸지지!  

### 클라우드의 종류  
- 공용 클라우드
- 사설 클라우드 : 접근 권한이 정해져있음, Zen, VmWare, Hyper-V, Azure Stack.
- Iaas, Paas(DB, OS 등 관리, 우리는 App만 올려서 사용), Saas 설명

### Azure의 장점  
- On-premise의 데이터를 클라우드로 옮기는 방법? Azure!
- 다른 업체들은 Hypervisor를 직접 하지 않는다, Zen과 KVM? KVN?을 쓴다.
- MS Data 센터 소개영상 시청, 건물 여러개가 모인 동이 AZ이고 AZ의 모임이 Region이지.
- NoC(Network Operation Center) : 네트워크 관제 센터
- 빨간불 들어오면 알바가 서버 클러스터만 갈아끼움. 하지만 사용자의 서비스는 죽지 않지.
- 한국에도 2개 있음. 각 나라의 법에 따라서 각 지역에 2개의 리전을 Pair로 묶는다. 동남아의 경우 나라들 법이 비슷비슷해서 전체커버.
- ISMS가 있다. Azure를 쓰며 ISMS 심사를 받게되면 하이패스로 통과
- CHEF 같은걸 사용할 때 Integration이 없거나 일반인이 만든것 뿐이다. Azure는 MS직원이 직접 올림.
- Azure Integration 검색. Tool이 Integration이 되어있으면 퍼블리싱은 Azure가 대신 해줘요. Git만 쓸 줄 알면 됨.

### Azure 서비스 모델 이해  
- 구매 옵션과 고객 지원 옵션이 따로 있다.
- 고객 지원 옵션 Premier로 쓰면 한명 전임으로 붙음

### Azure SLA  
- 과금이 종량제로 되니까 언제까지 보장하겠다가 아니고 사용하는동안 얼마나 보장할지가 계산하는게 SLA이다.
- 99.99999~~ 식으로 표현. 당연히 올라갈수록 비싸지
- 서비스 종류에 따라 SLA 수준이 모두 다름
- 가용성 세트 등 여부에 따라 달라짐
- 금융권은 10초 이상 멈추면 금감원에 보고를 해야한다구?
- 작동 중지 시간에 대한 보상을 알아보지 않는 사람이 꽤 많다.
- 멈춰도 보상금이 적기 때문에 DR이나 백업을 만들어야함. 하지만 - DR은 비싸지. 꼭 멈추지 말아야 할 서비스를 판단해야해.


### Storage SLA  
- LRS : 11 9 하나의 지역에서 3카피
- ZRS : 12 9 
- GRS : 16 9 2개의 지역에서 6개 복제본 (pair region)
- RA-GRS : GRS + Read Access가 가능

### Azure 차별점
- Azure 포털을 써보세요! 커스커마이징도 잘 돼요.
- Hyper-scale
- Enterprise grade
- Hybrid

### 학습법  
Microsoft Learn 들어가면 배울 수 있다.  
https://github.com/krazure/workshop-itpro-101

# Azure에서 제공하는 서비스의 특징  
### Azure 리소스 관리자  
- 리소스를 그룹화하고 관리한다.  
- 권한에 대한 역할 기반 액세스 제어 가능.  
- Management Groups - Subscriptions - Resource groups - Resource 단계로 권한 설정이 가능하다.
- Export template 기능으로 stack 배포가 가능. 인프라는 찍어내고 우리는 소스와 데이터만 업로드하면 됨  
- Custom deployment 기능에 템플릿, 파라미터 템플릿을 이용하여 앱 배포시 옵션을 설정, 태그를 사용해 다른 리소스 체계화가 가능.
- 템플릿만 업로드하면 wordPress가 뜨는 마법!

##  인프라 기반 서비스  
### Azure IaaS
- lift and shift가 가능하다.
- VM, Containers(Docker Cluster에 Docker Image 배포), Service Fabric(Cluster 안에 war, jar 같은 App을 배포), Other  

### Azure PaaS  
- App service, Functions, Logic apps, Power apps
- Web-app같은 경우 소스파일만 업로드하면 WAS설정이나 이런건 전혀 신경쓰지 않아도 된다.
- Web-app에서 Scale-out할 떄 자동화, 각 서버에 있는 소스들간의 싱크도 알아서 해줌(AwS는?)
- Logic Apps : 매 5분마다 naver에 get 요청을 보내고 실패하면 slack에 메시지 보내는 기능을 쉽게 만들 수 있다. 물론 금방 만들 수 있지만 이 또한 서버에서 돌아가야하는데 이건 알아서 돌려주고 잘 죽지도 않지

### 가상머신  
- Busterable은 터질 수 있으니 개발용으로 써라
- 비슷한게 AWS의 T-type이다.
- B타입은 터질 수 있지만 클러스터로 잘 묶어서 디자인을 할 수 있으면 B타입이 더 싸고 좋지. 하지만 그럴 수 있는 사람이 많이 없다.
- 규모를 측정해주는 툴도 있어.

#### 컨테이너 서비스  
가상화 환경이지만 가상 시스템과는 달리 운영 체제는 포함되지 않음.  
컨테이너는 가볍게 만들어져 동적으로 생성, 확장 및 중단되도록 설게됨.  

#### 네트워크 서비스  
NAT 지원하기 때문에 기본적으로 Internet Outbound가 가능하다.
하지만 그 공용 IP가 찍힐텐데?  
방법 1. 로드밸런서를 붙인다. 그럼 로드밸런서 Ip로 나가.  
방법 2. 가상컴퓨터에 공용IP 붙여 그럼 NATing이 가능해진다.

Azure Load Balancer : 5튜플을 기반으로 부하분산 처리를 한다.

Application Gateway를 만들때 WAF(방화벽) 설정도 해준다. MS가 얼마나 공격을 많이 받는지 생각해보면...쓸만하겠지..?

Http, Https 같은 보안성에 대한 테스트를 해주는 사이트가 있다.

Azure DNS : Cisco Umbrella에서 Domain blacklist를 갖고있고 그걸 참조해서 막아주는 서비스가 있다.  

Azure E-book도 있다.  


## 서버리스
서버의 특성, 확장 등을 고려하지 않아도 개발 및 배포, 서비스 운영이 가능한 것을 뜻함.  
CPU 자원과 메모리 자원을 안쓴다는 의미가 아니고 미리 선언해서 쓰지 않는다. 라는 의미다.  
서버를 몇대 쓰겠다 라고 선언할 필요없이, 서버에 대한 걸 모르고 그냥 쓴다. 정의해야 할 일들이 줄어들고 있는거지.  
그렇다고 서버가 없는건 당연히 아니지, 서버에 대한 구성을 내가 하지 않을 뿐.  

CPU는 개수가 아닌 Hz로 세는게 맞다.  

### Function
- Funtions와 결합하면 좋은 서비스
- Logic Apps
- Azure Cosmos DB
- evnet grid  

### Cognitive Service  
- ML 모델, input값 넣으면 output 내보내줌.
- 이미지를 넣어서 몇명인지 센다거나, Text를 분석하거나 등

## 마이크로 서비스  
독립적으로 배포 가능한 서비스들의 묶음 들로서 특정한 방법으로 소프트웨어를 디자인 하는 것.  
리소스를 효율적으로 쓰기 위한 목적.  
로그인, 메일, 채팅, 게시판을 서빙하는 서비스가 있을 때, 게시판의 이용 폭주로 scale out을 할 때 새로운 서버에도 동일한 jar로 설치한다. 게시판을 늘리기 위해서 다른 서비스도 늘리게 되고 다른 서비스가 늘어나면서 따라오는 관리까지 해야한다.  
부하가 걸리는 서비스를 늘리는게 정상인데 다른 서비스까지 늘린다? 그럼 그만큼의 자원은 낭비가 되는거지.  

마이크로서비스 vs 모놀리식서비스  

마이크로서비스를 편하게 구현할 방법을 찾다 나온게 도커  
그리고 그걸 편하게 운영할 방법을 찾다 나온게 쿠버네티스  

거버넌스 : 
데브옵스 : 개발과 운영이 한꺼번에 있는 형태  

### Service Fabric  
Docker보다 먼저 나왔으나 불편해서 Docker한테 밀림.  

### DevOps  
- Azure DevOps services  
CI, CD를 제공하는 빌드, 릴리즈 파이프 라인을 만들 수 있다.  
빌드서버 제공, Git 레포지토리, Kanban 보드 및 광범위한 자동 및 클라우드 기반 부하 테스트
- QA를 하기 위해 List를 만들때 오류가 발생하면 그 시나리오를 녹화해서 티켓으로 만들어서 쏜다.  

## Azure Data Service 활용분야  
SQL Server  
- 열심히 하지만 좋다고는 말 못해요~~  

Azure SQL DB(Paas)  
SQL Server 데이터베이스 기반 서비스  
Elastic Pool을 지원한다.  
운영제체와 플랫폼을 벤더사가 관리하는데 그 Side effect를 왜 내가 받아야 하는거지? Fully managed라는 말은 이 경우를 말하는 거라고 생각 함  

DTU(Database Transaction Unit)  
The Database Transaction Unit (DTU) is the unit of measure in SQL Database that represents the relative power of databases based on a real-world measure: the database transaction.

OSS DB를 적용하기 위해서 나온 제품이 vCore 모델. vCore 수와 메모리, 디스크 용량을 정할 수 있다.  
300초를 초과하는 DTU(5분 이상 걸리는 트랜잭션)가 있다면 vCore가 싸다.  

결국 한 벤더에서도 비슷비슷한 서비스를 여러개 내는데, 어떤 방식이 더 싸게 먹힐지는 사용자가 잘 알고 사용해야 한다.  

Azure Search Indexers  
두 DB에 대해서 인덱싱을 걸 수 있다. Search 안에서 검색 돌릴 수 있다.
- CosmosDB (NoSQL) API
- Azure SQL DB

### Big Data  
어떻게 운영할거고 뭐에 쓸건지가 중요함. 벤더사가 모든걸 다 해준다는 건 아니다. -> 구글이랑 논조가 좀 다른데... 내가 잘못 알고 있던건가  

빅데이터를 하는 이유는 Insight를 얻기 위함인데  
콜센터에서 빅데이터 제품을 이용 중. 녹취 파일로 빅데이터를 돌려서 업무 외 시간 응대를 한다. 와우..  

### IoT 
할게 별로 없다. 센싱, 네트워킹, 실제로 사용가능한 인터페이스 + 정보 요약 시스템이 필요.

### 지능형 클라우드 인프라 및 보안 관리  
지능형 클라우드란 모든 앱과 서비스에 인공 지능을 구축하는 것.  
Integration이 Key이다. 로그와 어떤 DB를 비교해서 Insight를 AI가 추출해준다.  
Kohler : Azure를 사용해서 홈 인테리어 IoT 디자인, 구축하는 회사  
트럭 운전사는 Agent(단말기)만 보고 운전하고 스케쥴이나 경로는 중앙에서 관리.  

Uber : 실시간 드라이버 인증. 중동 지역에서 반응이 좋다. Cognitive service를 이용함.

ACLs : Access control lists  

DDoS protection도 기본적으로 지원, 지원 티어가 여러개 있다.  

Azure ATP : Portal, Sensors, Cloud service 에서 Abnormal한 상황 알아서 포착  

Service health : Azure에 있는 서비스들의 현재 상황 모니터링해서 알려줌.  

Cloud 워치보다는 UI가 이쁜거 같기도 함  