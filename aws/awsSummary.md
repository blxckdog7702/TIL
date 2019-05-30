# AWS 관련 정리

## 정리  
- Lambda Function은 버전별 관리 가능
- SES에 예약발송 기능은 없음

## 정리필요  
- Lambda에 외부 config 설정할 수 있는지?
- S3 getObjectAsString의 용량 한도는?
- S3에 파일이 여러개 뜬다면 어떻게 처리되고 선택 가능한 옵션이 있나? 


# Lambda  

## Lambda in VPC  
람다 함수로 VPC 내의 Private 서브넷에 있는 리소스(예:RDS)에 접근하려면 람다 함수 또한 VPC를 설정해야 한다.

하지만 람다 함수에 VPC를 설정하면 인터넷과 인/아웃바운드가 막히게 된다. 왜냐하면, 람다 함수가 VPC 안에서 작동하면 Public IP를 가지지 못하고 Private IP만을 가지기 때문이다. 람다 함수에서 발생한 패킷은 인터넷 게이트웨이를 통과하지 못하고 버려진다.  

나의 경우엔 람다 함수에 VPC를 설정하지 않고 S3에 잘 접근하고 있었는데, RDS를 사용하기 위해 람다 함수에 VPC를 설정했더니 잘 되던 S3에 접근하지 못하고 Time out 에러가 발생했다.  

VPC안의 람다 함수가 VPC 밖의 다른 AWS 서비스나 인터넷에 접근하려면 NAT 게이트웨이가 필요하다. NAT 게이트웨이는 Public 서브넷에 두고, RDS와 람다 함수는 Private 서브넷에 둔다.
> Public 서브넷 : 인터넷과 연결된 VPC 내의 서브넷  
> Private 서브넷 : 인터넷과 분리된 VPC 내의 서브넷. NAT를 통해 인터넷으로 접근이 가능하다.  

그 다음 라우팅 테이블을 만들어 Private 서브넷에 설정하고, 그 라우팅 테이블의 모든 아웃바운드를 NAT로 통하게 설정하면 된다. 이후 각종 인/아웃바운드 보안 그룹 설정을 해주고, 람다 함수 IAM에 `AWSLambdaVPCAccessExecutionRole`을 추가하면 된다.  

S3나 DynamoDB는 VPC Endpoint 라는 기능을 제공한다. 따로 NAT 설정 없이도 Private 서브넷의 보안 그룹에 Endpoint를 추가해주면 Private 서브넷 내에서 접근이 가능하다.
