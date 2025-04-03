---
writer: Mark Son
date: 2025-03-27
---

# Chapter 7 - The Evolution of Automation at Google

## Summary


- 자동화 value -> consistency, platform전환, change faster... 등에 있음
- 구글이 초창기 자동화 접근 방식은 단순 스크립트 자동화였는데, 이후 복잡한 워크플로우 시스템으로 진화함.
- Borg라는 클러스터 관리 시스템의 도입 이후가 자동화 발전이 확 늘어남.

## Questions

- 구글의 자동화 발전 과정에서 반발 같은건 없었을까? 이 책을 읽으면 읽을수록 구글이니까 가능하다는 생각이.. 
- 자동화와 인간(개발자, 운영)간의 사이에 균형은 어떻게.. -> devops~SRE의 퍼포먼스가 쭉 올라가면서 백엔드 부분 업무가 많이 줄어드는듯(회바회)


## Thoughts

Borg의 도입으로 클라우드 컴퓨팅의 기반을 마련

"자동화 자체를 자동화하라" ... 자동화를 자동화하는 재귀적 관점

꽤 옛날책인데.. 현재 국내에서 이정도 수준으로 SRE이 잡혀있는 회사가 얼마나 있을까

장표 Figure 7-1의 DNS서비스 테스트 & 수정 자동화
  - 이게 잘 돌아가면 상관없다.
  - 문제는 real-world 카오스.. 일관적이지도 않고, 갑작스러운 실패 사항 -> 이게 그림 시스템대로 흘러가면 시스템이 오히려 불안해짐.
  - Flaky 테스트 문제 -> CI/CD가 중단되거나 반복실행되어 개발 주기가 오히려 역으로.. 역생산성 나타날수도 있음
  - > Borg!

딱히 뭔가 찬반 내지는 토의거리가 좀 적은 챕터였는듯.

## Difficulties

지난번과 같은 언급인데 자동화의 수준을 결정하는 것이 어려울 것임. 그리고 자동화 수준이 무조건 높다고 해서 반드시 그것이 최선인지? 이것도 상황에 따라 다를듯.

## References

- [Google SRE Book](https://sre.google/sre-book/table-of-contents/) - 챕터 7
- [Borg: The Predecessor to Kubernetes](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/)

- https://cloud.google.com/sre
- https://m.yes24.com/Goods/Detail/106188260
- https://blog.outsider.ne.kr/1358
- https://jpub.tistory.com/756

## Discussion Topics

- 자동화와 인간의 역할 사이의 균형.. devops ~ SRE -> 
- 소규모 스타트업에서도 구글의 자동화 접근 방식을 적용할 수 있을까요? 어떤 방식으로 접근해야 할까요?
- 자동화로 인해 발생할 수 있는 새로운 위험


---
