# Chapter 10 - Practical Alerting

## Summary
이번 챕터는 구글에서 사용하는 모니터링 시스템인 보그몬이 어떤 식으로 데이터를 수집하고 수집한 데이터를 저장하는지 등 전반적으로 보그몬에 대한 설명이 주를 이뤘다.

구글 특성 상 단순히 평균 응답 시간 측정을 위한 것 보다는 대규모 분산 시스템의 복잡한 동작을 이해하고 잠재적 문제를 예측하는 것이 모니터링의 주요 목적이기 때문에 여러 측도를 기준으로 데이터를 복합적으로 수집한다. 

시스템의 이상을 감지하는 것보다 사용자에게 영향을 미칠만한 상황을 감지하는 것에 더 초점을 두었다는 말을 이전 챕터에서도 본 것 같은데, 아마 이러한 기준으로 알람 조건을 설정한듯

수집한 데이터를 시계열 데이터로 변환하여, 이를 규칙으로 알람 규칙을 설정한다. 
## Questions

## Thoughts
전반적으로 보그몬에 대한 이야기가 주를 이뤘기 때문에, 뭔가 잘 와닿지 않는 느낌이었다. 보그몬 자체가 구글의 대규모 분산 시스템을 위해 개발된 툴이기에 더욱 그랬는지도..?

중간과 마무리 쯤에 데이터 라벨링에 대한 이야기가 몇 번 정도 언급됐는데, 데이터 라벨링을 통해 로그나 메트릭에 의미있는 태그를 붙여서 정확한 필터링 하는 방식을 이번 프로젝트에 도입하고 싶긴한데..흠 쉽지 않을 것 같다.

단순히 CPU나 메모리 사용량 같은 시스템 지표에만 치중에서 메트릭을 수집해오고 알람을 설정해왔는데, 실제로 사용자에게 영향을 미칠만한 메트릭 지표가 어떤게 있을지 고민해보는 것도 좋을 것 같다. CPU나 메모리 사용량도 물론 중요하긴 하지만서도..
## Difficulties

