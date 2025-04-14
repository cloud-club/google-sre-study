# Chapter 12 - Effective Troubleshooting

## Troubleshooting Process

- Problem Report
  - "An effective report should tell you the expected behavior, the actual behavior, and, if possible, how to reproduce the behavior"
    - 오픈소스 리포지토리 중 잘 관리되는 것들의 이슈를 보면 이러한 조건을 기조로 포맷이 잡혀있는 듯
  - 모든 이슈에 대해서 조직 내 누구나 접근할 수 있어야한다.
    - 문제가 발생했을 때, 먼저 리포지토리의 issues를 통해 검색하는 것을 생각해보면 될듯.
- Triage
  - "should be to make the system work as well as it can under the circumstances."
    - Site Reliability의 value가 높다면 우선 시스템이 돌아가게 하는 것이 우선됨은 맞을듯.
    - 다만 이슈의 재현 방법 및 로그, 데이터 등을 확실히 확보한 상황에서 진행을 해야하지 않을까.
    - 조사해야할 항목 또한 포맷으로 만들어두거나 항목에 대해서 따로 모니터링 대시보드를 미리 만들어두면 좋을 듯.
- Examine
  - 로그, 메트릭 데이터 등을 통한 원인 조사
- Diagnose
  - "it’s often best to start systematically from one end of the stack and work toward the other end, examining each component in turn"
    - 처음부터 하는 것도 좋지만, 분석할 layer의 스타팅 포인트를 잘 정하면 시간을 크게 절약할 수 있을 듯.
    - 굳이 처음부터 하려면, 미리 메뉴얼 코드를 작성해둬서 한번 실행으로 파악하는게...
  - Ask "what," "where," and "why"
    - 대개 문제가 안되는 것에만 초점을 맞추는 '비엔지니어'적인 사고방식이 위의 것을 생각해보지 않는듯.
    - 결과적으로, 이슈를 완전히 해결했다 -> 정확히 어떻게 문제가 발생했는지, 어떻게 해결하는지, 어떻게 재현하는지 등을 포함한 문서가 도출되어야하는 것 아닌가
- Test/Treat + Cure

  - state를 바꿔버리는 조치는 다시 돌아오기가 힘드니, 바꾸지 않거나 다시 원복할 수 있는 조치를 우선적으로 시행해보는게 좋은 듯.
    - 문제 상황 재현성이 확보된다면 사실 크게 상관이 없는 것 같음.
    - 그래서 별도의 머신에 복제해서 테스트로 인한 추가적인 문제 발생을 격리하는 것을 선호.
  - 경험적인 부분이 좌우하는 파트인 것 같지만, 모든 시행을 독립적으로 생각하고 언제든 원복해서 처음부터 시작할 수 있는 상태로 만들어야함을 중시하는 것이 핵심인 것 같음.

## Negative Results Are Magic

- Negative results should not be ignored or discounted
- Experiments with negative results are conclusive
- Tools and methods can outlive the experiment and inform future work
- Publishing negative results improves our industry’s data-driven culture.
- Publish your results

=> 대충 학계에서 말하는 연구 윤리 및 가치 등과 유사한 것 같음.

- _**e.g.**_ Neural Network와 같이, 당시에는 큰 의미가 없던 연구들이 언젠가 가치를 가지게 되는 경우가 상당수 존재.

## Thoughts

- 석/박사 과정을 우대하는 이유를 문서로 설명한 느낌
  - (상대적으로) 연구 경험을 통해 합리적으로 문제를 분석하고 해결할 수 있는 능력을 기를 수 있다는 것?
- 기본적인 엔지니어 마인드가 잡혀있다면 당연한 것일 수도
- 귀찮아도 Postmortem을 잘 작성하자.
  - 논문처럼 리뷰어가 있는 것도 아니기 때문에, 문법적 오류/오타 등을 크게 신경쓰지 않아도 되므로 부담을 안느끼고 작성 가능.
  - 자료조사 부분이 논문조사가 아니어도 됨
  - 반대로 말하면 Postmortem을 공들여 작성하면 논문을 잘 쓸 수 있게 되는 건가
