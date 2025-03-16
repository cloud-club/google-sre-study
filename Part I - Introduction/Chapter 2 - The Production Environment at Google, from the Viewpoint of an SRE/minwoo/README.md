---
writer: minwoo
date: 2025-03-10
---

# Chapter 1, 2 - The Production Environment at Google, from the Viewpoint of an SRE

## Summary
 - Google의 제품은 전 세계 수십억 명이 사용하며, 이 제품들이 안정적으로 작동하는 것이 중요함. 
 - Google의 SRE 팀은 서비스의 신뢰성을 높이기 위해 다양한 방법을 개발해 왔음.
 - 기존 SRE 기법(에러 버짓, 포스트모템 등)은 구글이 웹 서비스 규모를 확장하는 데 큰 기여를 해옴.

## Questions
SRE의 역할이 매우 방대해서 실제 현업자에게 어떤 업무를 하는지가 궁금함. 이전에 올리브영 SRE를 뵌적이 있는데, 주된 업무가 datadog 모니터링 서비스를 가지고 자사 온오프라인 트래픽을 추적 관리하는 시스템을 설계하는 것이었음.
책에서도 SRE의 역할이 결코 좁지않은데2025년 현재는 책에서보다도 더 역할이 크게 확대된 듯( AI/ML이 복잡해져서? )
현업자의 발표를 좀 더 찾아봐야 할 거 같다.

## Thoughts
- Questions과 같아서 생략.

## Difficulties

책 내용에 대한 어려움..은 아니고, SRE로 커리어를 점프하는 사례를 링크드인에서 몇번 목격한거 같은데 그냥 직군 이동 정도가 아니라 SRE에 대한 이해와 실력이 출중(?)해야할 듯.
책을 더 읽어보면서 공부를 해봐야겠다 (먼 미래에는 SRE 도전해보고싶다)

## References

1. 책을 읽다가 문득 궁금해진 사항들에 대해서 (SRE랑 데브옵스가 뭔차이지.. 교집합이 큰거같은데?)
 
perplexity에 parameter option : deep research로 선택하여 다음과 같이 프롬프트를 날려보았습니다.
<img width="802" alt="image" src="https://github.com/user-attachments/assets/f090e95b-a887-4d19-b1c5-b2183018c22c" />

[답변 전문] (다음부터는 짧은 요약만 올릴게요)

# 2025년 SRE와 DevOps의 차이점에 대한 종합 분석: 소프트웨어 엔지니어링 및 비즈니스 관점  

현대 소프트웨어 엔지니어링 생태계에서 SRE(Site Reliability Engineering)와 DevOps는 상호보완적이면서도 명확한 차별성을 갖는 체계로 진화했습니다. 2025년 기준으로 두 접근법의 차이를 다층적 관점에서 분석하면 다음과 같습니다.  

---

## 1. 소프트웨어 엔지니어링 관점의 차이  

### 1.1 개발 초점과 목표 설정의 차별화  
DevOps 팀은 **지속적 통합/배포(CI/CD)** 파이프라인 최적화에 집중하며, Jenkins와 ArgoCD를 활용해 시간당 50회 이상의 마이크로서비스 배포를 가능하게 합니다[1][3]. 반면 SRE는 **서비스 수준 목표(SLO)**를 정의해 "월간 99.99% 가용성 유지"와 같은 정량적 기준을 설정하고, 이를 달성하기 위한 엔지니어링 프로세스를 설계합니다[12][15].  

예를 들어 Google Cloud의 SRE 팀은 서비스 장애 시 자동 복구 시스템이 트리거되는 임계값을 $$ \text{MTTR} \leq 5\text{min} $$으로 설정하여 시스템의 자기치유 능력을 강화합니다[5]. 이는 DevOps의 "빠른 배포" 목표와 SRE의 "안정성 보장" 목표가 상호작용하는 전형적 사례입니다.  

### 1.2 운영 접근 방식의 차이  
DevOps 엔지니어는 **Infrastructure as Code(IaC)**를 통해 Terraform으로 클라우드 리소스를 프로비저닝하는 반면, SRE는 **에러 예산(Error Budget)** 개념을 도입해 "허용 가능한 장애 시간"을 계산합니다. 2025년 Netflix 사례에서 SLO 99.95% 달성을 위해 월 21.6분의 다운타임을 예산으로 할당하고, 이를 초과할 경우 기능 배포를 중단하는 전략을 적용했습니다[15].  

```python
# SLO 기반 배포 승인 로직 예시
error_budget = 1 - (uptime_SLO / 100) 
remaining_budget = error_budget - actual_downtime
if remaining_budget > 0:
    approve_deployment()
else:
    trigger_reliability_improvement()
```
이 코드는 SRE의 핵심 원칙인 위험 기반 의사결정 프로세스를 구현한 사례입니다[12].  

### 1.3 모니터링 체계의 진화  
DevOps 팀은 **APM(Application Performance Monitoring)** 도구를 사용해 트랜잭션 처리량을 실시간 추적하는 반면, SRE는 **eBPF(Extended Berkeley Packet Filter)** 기술을 활용한 커널 레벨 모니터링으로 3ms 이하의 마이크로 레이턴시 변동까지 감지합니다[15]. 2025년 AWS의 사례에서는 SRE 팀이 **AI 기반 이상 탐지 모델**을 개발해 기존 규칙 기반 알림보다 62% 빠른 장애 예측을 달성했습니다.  

---

## 2. 비즈니스 운영 관점의 영향 비교  

### 2.1 조직 구조와 비용 최적화  
DevOps 도입 기업은 **기능 팀(Functional Team)** 구조에서 **프로덕트 팀(Product Team)** 구조로 전환하며, 개발-운영 간 커뮤니케이션 비용을 40% 절감합니다[3][14]. 반면 SRE를 채택한 기업은 **신뢰성 엔지니어링 전담 조직**을 구성해 MTTR(Mean Time to Repair)을 75% 단축하고, 연간 예상치 못한 인프라 비용을 $2.3M 절감한 사례가 있습니다[5][15].  

| 지표                | DevOps 영향                 | SRE 영향                    |
|---------------------|----------------------------|----------------------------|
| 배포 빈도           | 300% 증가                  | 150% 증가 (안정성 우선)    |
| 인시던트 처리 비용  | 25% 감소                   | 68% 감소                   |
| 고객 이탈률         | 15% 개선                   | 32% 개선                   |  

### 2.2 위험 관리 전략의 차이  
DevOps 조직은 **블루/그린 배포** 전략으로 신기능 출시 리스크를 분산시키는 반면, SRE는 **카오스 엔지니어링**을 시스템화해 연간 200회 이상의 의도적 장애 주입 실험을 수행합니다[12]. 2025년 Microsoft Azure의 SRE 팀은 **양자 컴퓨팅 환경**에서의 장애 시뮬레이션 도구를 개발해 기존 클라우드 시스템 대비 89% 높은 내결함성을 입증했습니다.  

### 2.3 수익 모델 영향 분석  
DevOps 중심 기업은 **기능 출시 주기 단축**으로 ARPU(Average Revenue Per User)를 18% 상승시킨 반면, SRE 강조 기업은 **서비스 가용성 개선**으로 LTV(Lifetime Value)를 27% 증가시켰습니다[14]. 특히 금융科技(fintech) 분야에서는 SRE의 **실시간 거래 검증 시스템**이 0.0001초 단위의 거래 무결성을 보장하며, 연간 $450M 규모의 결제 실패 비용을 방지하고 있습니다.  

---

## 3. 2025년 기술 트렌드의 상호작용  

### 3.1 AIOps의 융합 양상  
DevOps 파이프라인에 **MLOps 프레임워크**를 통합해 코드 리뷰 시간을 53% 단축하는 반면, SRE는 **예측적 장애 분석(Predictive Failure Analysis)** 모델을 개발해 PagerDuty 알림보다 22분 빠른 대응이 가능해졌습니다[15]. 2025년 Gartner 보고서에 따르면, AI 기반 SRE 도구 시장이 전년 대비 140% 성장하며 $7.8B 규모에 도달했습니다.  

### 3.2 지속가능성 목표의 통합  
DevOps 팀은 **그린 코딩(Green Coding)** 원칙을 도입해 CPU 사용률을 18% 낮추는 반면, SRE는 **탄소 배출량 SLO**를 신규 지표로 추가해 데이터센터 에너지 소비를 650MWh/yr 절감했습니다[5][15]. Google의 경우 지역별 재생에너지 비율을 배포 전략에 반영하는 **Carbon-Aware SRE** 시스템을 가동 중입니다.  

---

Citations:
[1] https://www.splunk.com/en_us/blog/learn/sre-vs-devops-vs-platform-engineering.html
[2] https://www.ibm.com/think/topics/devops-vs-sre
[3] https://www.moontechnolabs.com/blog/devops-vs-sre/
[4] https://f-lab.kr/insight/devops-sre-difference-20240801
[5] https://www.purestorage.com/kr/knowledge/what-is-a-site-reliability-engineer.html
[6] https://brunch.co.kr/@@5KoQ/604
[7] https://www.pagerduty.com/resources/learn/sre-vs-devops/
[8] https://last9.io/blog/sre-vs-devops/
[9] https://www.andrewhowden.com/p/the-problem-of-sre-vs-devops-vs-whatever
[10] https://learn.microsoft.com/ko-kr/azure/site-reliability-engineering/articles/devops
[11] https://newrelic.com/kr/blog/best-practices/adopting-sre-practices
[12] https://spacelift.io/blog/sre-vs-devops
[13] https://www.reddit.com/r/devops/comments/mxol7f/devops_vs_sre/
[14] https://f-lab.kr/insight/devops-and-sre-in-modern-it
[15] https://insight.infograb.net/blog/2025/02/26/2025-sre-trends
[16] https://sre.google/workbook/how-sre-relates/
[17] https://www.linkedin.com/pulse/sre-better-than-devops-2025-detailed-career-path-devraj-sarkar-9qaoc
[18] https://www.atlassian.com/devops/frameworks/sre-vs-devops
[19] https://www.godeltech.com/the-differences-between-devops-and-site-reliability-engineering/
[20] https://github.com/resources/articles/devops/sre-vs-devops
[21] https://www.netdata.cloud/academy/sre-vs-devops-what-are-the-main-differences-between-them/
[22] https://bluexp.netapp.com/blog/cvo-blg-sre-benefits-and-business-impact-of-the-sre-mindset
[23] https://www.coursera.org/articles/sre-vs-devops
[24] https://brokee.io/blog/sre-vs-devops
[25] https://www.statuspal.io/blog/top-devops-tools-sre
[26] https://roadmap.sh/devops
[27] https://www.youtube.com/watch?v=Gt3EiVCpmlg
[28] https://potato-yong.tistory.com/121
[29] https://post.naver.com/viewer/postView.naver?volumeNo=36224183&memberNo=25379965
[30] https://tech1.tistory.com/106
[31] https://insight.infograb.net/blog/2025/01/17/2025-devops-trends/
[32] https://www.youtube.com/watch?v=1VQvEZLBkq8
[33] https://www.netapp.com/ko/devops-solutions/what-is-site-reliability-engineering/
[34] https://www.cio.com/article/3532554/%EB%8C%80%EA%B7%9C%EB%AA%A8-%EB%8D%B0%EB%B8%8C%EC%98%B5%EC%8A%A4-%EC%9A%B4%EC%98%81%EC%9D%98-%EC%A0%95%EC%84%9D%C2%B7%C2%B7%C2%B7-%EC%A0%80%EC%8A%A4%ED%8A%B8%EC%9E%87%EC%9D%98-sre-%ED%8C%80.html
[35] https://www.spaceone.megazone.io/blog/devops-vs-sre
[36] https://blog.skby.net/%ED%94%8C%EB%9E%AB%ED%8F%BC-%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81-platform-engineering/
[37] https://tech.devsisters.com/posts/the-human-scalability-of-devops/
[38] https://www.redhat.com/ko/topics/devops/platform-engineering-vs-devops
[39] https://brunch.co.kr/@delight412/750
[40] https://newdeal123.tistory.com/105

---
Perplexity로부터의 답변: pplx.ai/share


2. https://careerly.co.kr/comments/101362


> [!NOTE]
> 당근 SRE분(링크드인에 아주 자주뜨죠?)의 아티클도 참고했습니다. 앞으로도 계속 챕터별로 매칭되는 내용이 있다면 계속 찾아볼게요.

3. Catchpoint의 SRE Report 2025

> [!TIP]
> 업계에서 자주 회자되는 보고서라고 합니다.. 참고

아래는 SRE Report 2025 10줄 요약

# Catchpoint SRE Report 2025 핵심 요약  

1. **"Slow is the new down"**: 53% 기업이 성능 저하를 다운타임과 동등한 위험으로 인식[1][7], 사용자 경험이 핵심 신뢰성 지표로 부상[4][8].  
2. **운영 토일(Toil) 증가**: AI 도입에도 불구, 토일 작업 비중이 2024년 25% → 2025년 30%로 5년 만에 역전[1][7]. 자동화 효용성에 의문 제기[5].  
3. **릴리스 vs 신뢰성 갈등**: 67% 조직이 안정성보다 출시 일정 우선시하는 압력 경험[1][8], 개발 속도와 시스템 안정성 간 균형 필요성 대두.  
4. **다중 모니터링 도구 활용**: 2~10개 도구 병용이 일반화[1][3], "비용보다 가치" 중심의 옵저버빌리티 전략 강조[7].  
5. **AI 교육 수요 증가**: 응답자 30%가 AI 기술 교육 요구[1], 코드 작성(37%)이 주요 활용 사례이나 실전 적용은 제한적[7].  
6. **인시던트 빈발 현상**: 40% 기업이 월 1~5건 장애 처리[1], 사고 후 스트레스 지속(28%) 등 인적 영향 관리 필요성[7].  
7. **신뢰성 목표 불일치**: 관리자-실무자 간 인식 차이 발생[8], 전략적 정렬 미흡이 운영 효율성 저해 요인으로 분석.  
8. **생산성 압박 가중**: DORA 리포트와 연계 분석 결과 AI가 오히려 업무 부담 증가시킨다는 역설적 결론[5][7].  
9. **성능 기반 의사결정**: 99.95% 이상 SLO 달성 기업이 고객 이탈률 32% 개선[2][7], 정량적 지표 운영의 중요성 재확인.  
10. **탄력적 조직 문화**: 포스트모템 분석과 무비난 문화 도입이 장기적 신뢰성 향상의 열쇠로 제시[5][8].  

(※ 모든 통계 및 인용은 Catchpoint 공식 보고서[1][4][7] 및 관련 분석[3][8] 기반)

Citations:
[1] https://www.catchpoint.com/press-releases/the-sre-report-2025-highlighting-critical-trends-in-site-reliability-engineering
[2] https://www.youtube.com/watch?v=SQsJNsV0A_E
[3] https://insight.infograb.net/blog/2025/02/26/2025-sre-trends
[4] https://www.catchpoint.com/learn/sre-report-2025
[5] https://www.catchpoint.com/blog/the-sre-report-2025s-call-to-action
[6] https://www.catchpoint.com/asset/2025-sre-report
[7] https://rootly.com/blog/sre-report-2025---key-takeaway
[8] https://www.linkedin.com/posts/adhorn_the-sre-report-2025-catchpoint-activity-7286391405940248576-nS8s
[9] https://www.linkedin.com/posts/gerrowadat_the-sre-report-2025-catchpoint-activity-7284578236884254720-JxBD
[10] https://finance.yahoo.com/news/sre-report-2025-highlighting-critical-133000036.html

---
Perplexity로부터의 답변: pplx.ai/share



## Discussion Topics

on study
