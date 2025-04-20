# Chapter 14 - Managing Incidents

## Summary & Thoughts

작은 장애 상황이 아닌, 긴급하게 대처해야하는 매우 큰 규모의 장애 상황을 어떤 프로세스로 대처해야할까

- Elements of Incident Management Process
  - Recursive Separation of Responsibilities
    - Incident Command
      - 전체 상황을 제어할 수 있는 임시 지휘권을 가지게 되는 사람
      - 임시로 TF를 구성하는 것도 좋음.
    - Operational Work
      - Commander와 협력하여 해당 상황을 해결하기 위한 작업을 수행하는 사람들
      - 작업에만 집중
    - Communication
      - 해당 TF의 상황에 대해 문서를 정리하며 외부와의 소통을 담당하는 사람.
    - Planning
      - 오로지 모두가 상황 해결에 몰두 할 수 있도록 전체적인 계획을 세우는 사람.

=> 이렇게 구성되면 정말 이상적일 것 같음. 즉, Operational Worker 입장에서는 문제 해결 이후 추가적인 잡무를 해야함에 대한 스트레스를 덜 받지 않을까 (밤샘 후 이메일 작성 등등)

- [Example Incident State Document](https://sre.google/sre-book/incident-document/)
  - 실제 문제가 생겼을 때 이 포맷으로 작성하자고 제안해봐야할 듯.
  - 추적은 필요하되 긴급하여 git commit 등을 하기 어려운 상황에서, 내부 작업자/외부 관계자 모두 만족할 수 있는 포맷인 것 같음.
  - 추후 해당 상황을 처음 들여다보는 사람도 쉽게 흐름을 이해할 수 있을 것 같음.

```markdown
Shakespeare Sonnet++ Overload: 2015-10-21
Incident management info: https://incident-management-cheat-sheet

**(Communications lead to keep summary updated.)**
Summary: Shakespeare search service in cascading failure due to newly discovered sonnet not in search index.

Status: active, incident #465

Command Post(s): #shakespeare on IRC

Command Hierarchy (all responders)

- Current Incident Commander: jennifer
  - Operations lead: docbrown
  - Planning lead: jennifer
  - Communications lead: jennifer
- Next Incident Commander: to be determined

**(Update at least every four hours and at handoff of Comms Lead role.)**
Detailed Status (last updated at 2015-10-21 15:28 UTC by jennifer)

Exit Criteria:

- New sonnet added to Shakespeare search corpus TODO
- Within availability (99.99%) and latency (99%ile < 100 ms) SLOs for 30+ minutes TODO

TODO list and bugs filed:

- Run MapReduce job to reindex Shakespeare corpus DONE
- Borrow emergency resources to bring up extra capacity DONE
- Enable flux capacitor to balance load between clusters (Bug 5554823) TODO

Incident timeline (most recent first: times are in UTC)

- 2015-10-21 15:28 UTC jennifer
  - Increasing serving capacity globally by 2x
- 2015-10-21 15:21 UTC jennifer
  - Directing all traffic to USA-2 sacrificial cluster and draining traffic from other clusters so they can recover from cascading failure while spinning up more tasks
  - MapReduce index job complete, awaiting Bigtable replication to all clusters
- 2015-10-21 15:10 UTC martym
  - Adding new sonnet to Shakespeare corpus and starting index MapReduce
- 2015-10-21 15:04 UTC martym
  - Obtains text of newly discovered sonnet from shakespeare-discuss@ mailing list
- 2015-10-21 15:01 UTC docbrown
  - Incident declared due to cascading failure
- 2015-10-21 14:55 UTC docbrown
  - Pager storm, ManyHttp500s in all clusters
```

## Discussion Topics

- 장애 상황 처리 시, 이렇게 추적가능한 문서를 남기는 지.
- 대개 큰 규모의 장애 상황에서 어떤 식으로 TF가 꾸려지는 지
