# Chapter 13 - Emergency Response

## Summary & Thoughts

- Keep a History of Outages
  - 또 postmortem을 잘 쓰자는 얘기 (안쓰는 사람이 워낙 많으니)
  - issue에 label을 `postmortem-bug`로 붙여두고, 추후 PR이나 해결된 부분에 해당 issue를 링크하고 `resolve` label을 달아두면 어떨까
- Ask the Big, Even Improbable, Questions: What If…?
  - 항상 발생 가능한 위험들을 최대한 고려를 해보라는 의미
  - 뭔가 이런 부분에서는 IT가 참 모호하다고 느껴짐
    - safety 관련해서는 고정적이더라도 확실한 절차/기준이 존재해야하고 그것을 시스템 관련 엔지니어들은 알아야하지 않을까
    - 정부/기관에서 발급하는 인증 시스템이 있으나 많은 회사에서 신경쓰지 않는 편.
- Encourage Proactive Testing
  - 크게는 Chaos Engineering 등이 해당.
  - 주변에서 금방 찾을 수 있는 것은, nightly tag가 붙어 매일 나오는 도커 허브 내 이미지들?
  - 귀찮지만 트러블 슈팅 후 해당 이슈와 관련된 state를 확인할 수 있는 스크립트를 작성해두고 모아서 추후 실행하는 것도 하나의 테스트로 쓰일 수 있을 듯.
- Attitude for Emergency Response?
  - 당황하지 말고 언제든 감당 못할 것 같으면 요청을 하자
    - 부담은 안 가지되 처리 능력을 기르도록 노력은 해야하는 걸 모르면 안됨.
    - 문제가 일어났을 때 얼마나 빠르게 대처하고 사후 처리도 깔끔한 지가 자신의 능력을 보여주는 것이라고 생각.

## Discussion Topics

- 각자 하루 이상 걸린 트러블슈팅 경험?
- 실제 운영 중인 시스템에서 발생한 장애 상황?
