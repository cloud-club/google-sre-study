# Chapter 1 - Introduction

## SRE의 배경?

System Administrator가 이미 존재하는 소프트웨어 컴포넌트를 모아서 함께 동작하도록 배포. 서비스가 성장할 수록 이벤트/업데이트 및 업무 증가.  
대개 ops 팀에 속하게 됨.
다만 수작업 + dev vs ops의 갈등이라는 단점이 존재

> 보수적으로 운영할 것인가, 새 버전의 product를 빠르게 배포할 것인가?

## Google SRE

> 소프트웨어 시스템 개발을 통해 복잡한 문제를 해결할 수 있다는 신념 + 수작업을 대신할 수 있는 소프트웨어 작성

- Google의 SRE팀은 system engineer만이 아니라 50% 이상이 software engineer.
- 끊임없이 엔지니어링을 추구해서 늘어나는 업무를 줄이자 => Ops 업무는 50%로 유지하고 나머지는 개발 -> 시스템을 자동화.

- 여기서 말하는 개발은 시스템 개선을 위한 개발이 아닐까?
  - 개발팀은 실제로 application service에 관련된 개발을 진행. SRE는 시스템을 개선하기 위한 개발을 진행
  - ex) 모니터링 시스템, CI/CD, IaC
  - golang 등으로 이미 완성된 소프트웨어를 사용하는 것만이 아닌 커스텀
  - 해당 개발의 영역은 dev team이 작업이 어려운 부분이며 시스템에 관련되었기 때문에 SRE팀이 작업하는(해야하는) 부분이라고 생각

## DevOps vs SRE?

회바회인 것 같은 느낌.  
서비스 운영이 중요하면 SRE, 서비스 개발 라이프사이클이 중요하면 DevOps에 "가까운" 것이 아닐까?

For example,  
인터넷 접속이 안될때, Google이나 GitHub 사이트로 접속 시도 + 해당 사이트가 문제가 있다기 보다는 사용자의 인터넷 환경이 문제가 있다고 생각이 들 정도로 서비스의 Site Reliability가 높음.  
이렇게 장애가 거의 느껴지지 않을 정도로 엔지니어링을 하는 것이 SRE Engineer라고 생각.

반면 배포까지 이어지는 개발 라이프사이클에 모든 영역을 책임지고 엔지니어링을 하는 것이 DevOps Engineer라고 생각.

규모가 크고 실시간 서비스를 하는 회사에서는 DevOps와 SRE가 분리되어 있을 수도 있지만, 보다 규모가 작은 회사에서는 DevOps와 SRE의 역할이 혼재되어 있을 수도 있을 것 같음.

## Statistical Figure

- Availability
- Latency
- Performance
- Efficiency
- Change Management
- Monitoring
- Emergency Response
- Capacity Planning

### Availability

> 개발로 인한 어느정도의 감수할 수 있는 불가용성 => error budget

무조건적으로 서비스의 안정성을 유지하는 것이 목표가 아님. 신뢰성 100%는 불가능에 가깝기도하며 가성비가 떨어질 수 있음.  
어느정도의 여유를 두고 "error budget"을 설정하여 해당 예산 안에 꾸준히 개발을 진행하여 발전시켜나가는 것이 중요.

### Monitoring

단순히 로그/메트릭 모니터링 시스템으로 점검하는 형태는 항상 지양.  
사람이 이메일을 읽어보고 대응을 해야할지 말아야할지 결정을 하는 것은 문제가 있다 => 저자의 관점이 보이는 부분

장애에 대한 판단은 소프트웨어가 하도록 엔지니어링

alert => 정말 긴급하게 처리해야할 것  
ticket => 긴급하게 처리할 필요가 없는 것
logging => 추후 누가 오더라도 쉽게 파악할 수 있도록 기록해야할 것

### Emergency Response

MTTF/MTTR => Mean Time To Failure / Mean Time To Recovery

얼마나 빨리 고치냐에 대한 지표.  
MTTR이 짧은 사람은 대체로 경험이 풍부한 사람이라고 생각할 수 잇을 듯

### Change Management

- 제품의 단계적 출시
- 문제를 빠르고 정확하게 도출하기
- 문제 발생 시 안전하게 원복

=> Kubernetes Resource의 Deployment 기능이 위의 관점을 base로 나온 것이 아닐까?

### Capacity Planning

변화에 대한 사용자의 수용력을 생각하는 것이 중요.  
자연적 수요/인위적 수요로 나눌 수 있는데, 이것들은 꼭 클라이언트 뿐만 아니라 새로운 정책/도구 등을 도입할 때도 고려해야하는 요소인듯.

### Provisioning

Provisioning은 빠르게 수행될 필요가 있는데, Terraform 등의 IaC 도구 없이 수작업으로 하는 경우를 생각하면 비교가 쉬울듯. (지금에야 매우 기본이지만)

### Efficiency

꾸준히 시스템을 관찰하여 개선할 여지를 찾아내 효율성을 향상시켜야한다 -> 소위 Terraform/GitHub Action workflow 코드 등을 "깎는" 것이 생각나는데, 중요한 덕목이라고 생각이 듦.
