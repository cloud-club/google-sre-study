# Chapter 3 - Embracing Risk

최상의 안정성 확보 -> 비용이 너무 많이 들게 되어 기능 구현에 방해가 됨.  
=> 신뢰성 확보를 위한 균형점을 찾아야함.

## 위험요소 관리하기

비용 발생 부분 => 1) machine resource 2) 기회비용

### 1) machine resource

시스템의 신뢰성을 위해 분산/이중화 등을 적용할 때 추가 자원이 필요하다는 것을 얘기하는 듯.
`Parity Code`를 언급하는 것이 그 근거.

> [!TIP] Parity?
> [RAID의 Parity Concept](https://www.pcmag.com/encyclopedia/term/raid-parity)이나 [MinIO의 Erasure Code Concept](https://min.io/docs/minio/linux/operations/concepts/erasure-coding.html)을 참고

### 2) 기회비용

프로덕트의 기능 개발에 들어가는 비용보다는 시스템의 신뢰성 보장을 위해 투입되는 비용.  
기업이 기꺼이 부담할 용의가 있는 위험 요소를 찾아내야함 => 합리적으로 근거를 찾아내야한다는 소리인 듯. 대개는 당장의 feature 개발으로 인한 이익을 추구하기 때문에

## 서비스 위험 측정하기

> [!NOTE] Core Formula
> `Availability = Succeed / Total`

`time based availability => uptime/(uptime + downtime)`  
다만 분산 시스템에서는 실제 서비스 일부가 다운되어도 전체 서비스가 다운되지 않도록 설계되기 때문에 time based availability만으로는 부족함.

`Aggregate availability => successful requests/total requests`  
request 단위로 측정하기 때문에 조금 더 세밀한 측정 가능

=> 이렇게 분산 시스템 및 request라는 하나의 단위를 고려하다보니 `Trace`라는 컨셉이 필요한 것이 아닐까  
ex) 하나의 request가 발생했을 때부터 처리되어 완료될 때까지를 하나의 `Trace(request lifecycle)`로 보고 세부 단계는 `Span`으로 구성.

Core Formula를 조금 변경하는 것만으로도 여러 시스템에 동일하게 적용가능하며,  
식이 단순하기 때문에 지속적인 Aggregation이 필요하지 않음. (Batch로 처리하는 것만으로도 충분)

## Risk Tolerance

**SRE는 반드시 Product Owner와 협업하여 Risk Tolerance를 결정해야함.**

Product 팀이 사용자/사업적 요소를 이해하기 때문에 같이 논의를 해야 함. 현실적으로 보아도 SRE가 단독 진행 불가.

### Prerequisite

- Target Level of Availability
  - 구글은 Target을 넘은 경우 보상
- Types of failures
  - 장애의 종류를 먼저 파악 후, 중요도/우선순위를 정해서 결정에 반영
- Cost
  - 신뢰성과 수익 사이의 단순한 방정식을 도출 -> Trade-off (이렇게 해도 당장의 수익이 우선시되는 경우가 많은 듯)
  - 최종 사용자 관점에서 에러 발생율을 고려 => QA 테스트 등으로 평소 발생 빈도를 유사하게 측정하는 것이 이 부분에 해당하지 않을까
- Service Metrics
  - 클라이언트 사이드 렌더링이 늦는 것을 이유로, 구글 애드센스는 Latency 지표를 덜 중요하게 여긴 듯.  
    (합리적이나 애플리케이션 렌더링이 빠르다면 문제지 않을까..? 당장 web frontend framework lifecycle 가장 앞에 애드센드가 온다면 금방 고객 단에서 측정이 되어 불만이..)

## Error Budget Forming

1. Product Owner와 SLO 산정
2. 내부 모니터링 시스템으로 실제 업타임 측정
3. SLO ~ 실제 업타임 간 차이를 기준으로 unreliability 측정 => Error Budget
4. 향후 업타임이 SLO를 초과 (Error Budget가 남아있다면) => 릴리즈 가능

문제는 **혁신을 위해 SLO를 희생**하는 경우가 많다는 것. (안정성을 덜 중요시하고 기능 개발에 집중)  
Error Budget의 경우 개발팀과 SRE팀이 공유(SRE의 Concept이 아닌)한다는 것을 상호 인지하는 것이 중요한듯
