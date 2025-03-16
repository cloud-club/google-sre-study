# Chapter 4 - Service Level Objectives

## SLI

Service Level Indicator

- 대개는 latency, error rate, throughput 등을 핵심 지표로 사용
- 이외에는 서비스에 맞게 커스텀해야함.
  - 상당히 어려운 부분인데, Aggregate Availability 와 같은 식이 외에도 자주 사용되는 공식이 있는지 궁금
- SRE는 Availability를 가장 중요하게 여김.

## SLO

Service Level Objective

- SLI의 Threshold 값으로 보는 것이 외우기 쉬운듯.
- "명확한 SLO가 설정되어 있지 않다면 서비스를 디자인하고 운영하는 사람들의 생각과는 전혀 다른, 자신들이 희망하는 성능을 기대"
  - Product Owner와 협의를 해야하는 이유. 엔지니어가 중요하게 보는 부분과 사용자/사업자가 중요하게 보는 부분은 항상 다른 것 같음

## Google Chubby Outage

Chubby는 Google의 분산 락 서비스. Chubby가 오랜시간 신뢰성이 높았기 때문에 다른 서비스들의 chubby 서비스 의존성(coupling)이 높아진 상태에서 일어난 대규모 장애.

> [!NOTE]
> 유사하게 2주 전에 Docker가 오랜 시간 신뢰성이 높았고, Docker의 핵심 feature는 항상 동일했기 때문에 LTS 버전과 관계없이 그냥 최신을 사용했었다가 큰코 다침.  
> 항상 의심을 하면서 사용해야한다는 것을 느꼈지만, 모든 것을 일일히 신경쓰긴 어려워서 Mirantis의 Docker Enterprise Edition 버전을 기준으로 Community Edition 버전을 사용하는 게 좋다고 생각.  
> Reference: [endoflife docker-engine](https://endoflife.date/docker-engine)

## SLA

Service Level Agreement

SLO를 기반으로 사용자와의 계약을 맺는 것. (달성하지 못하면 어떤 조치를 취할 것인지)  
=> 엔지니어와 크게 관계는 없지 않을까. 매니저나 PM, 리드가 중요하게 여기는 부분인 듯.

## Setting Indicators

가장 기본적으로 고려하는 지표들인듯.
Node Exporter 및 SDK 사용으로 요즘은 어느정도 쉽게 측정 가능한 metric이지 않을까.

- User-facing
  - Availability
  - Latency
  - Throughput
- Storage
  - latency
  - availability
  - durability
- Big Data
  - throughput
  - latency (pipeline ended)

### Collecting Indicators

Server Side뿐만 아니라 Client Side에서도 측정해야 사용자 실제 경험을 판단한다고 하는데, Google Analytics 같은 것을 의미하는 것 같음.

### Aggregating Indicators

지표는 은연 중에 합산되어 고려될 수 있기 때문에, 평균보다는 분포(distribution)를 고려해야한다고 함.  
=> 일반적인 연구 방법론과 유사한 부분이 있는 것 같은데, 분포를 확인함으로써 "현재 시스템의 경향을 파악한다"가 더 와닿는 듯.

### Standardizing Indicators

intervals, regions, frequencies, data list, data source, response 등을 표준화하기를 권장.

=> Prometheus Data Source에서 거의 유사한 방식으로 정의를 하는 것 같은데, 현재 어느정도 오픈소스까지 표준화가 되어서 이미 반영되었다가 맞는듯.

## Choosing Targets

- 현재 퍼포먼스를 기준으로 목표 설정 x
- 최대한 단순하게
- "절대적"인 것은 없다
- SLO는 적을수록 좋다
- 처음부터 완벽 x

=> SLO가 사용자의 사고를 반영하기 위한 노력이기 때문에, 크게보면 개발자/SRE 상호 모두에게 좋은 지표.  
의견이 나뉘더라도 SLO를 통해 합리적인 주장을 할 수 있다는 것이 큰 장점인 것 같음. 상호 합의를 통해 나온 지표이기 때문에 반박의 여지가 없지 않을까라는 생각.  
SRE는 이런 지표에 의지해서 신뢰성을 향상시키기 위한 인프라/플랫폼 도입을 주장할 수 있을 듯.  
(과하지만 않게)
