---
title: Kafka Assignor
categories: Kafka
---

컨슈머와 파티션 할당 정책은 컨슈머의 assignor에 의해 결정된다. 카프카에서는 RangeAssignor, RoundRobinAssignor, StickyAssignor를 제공한다. 카프카 2.5.0는 RangeAssignor가 기본값으로 설정된다.

- RangeAssignor : 각 토픽에서 파티션을 숫자로 정렬, 컨슈머를 사전 순서로 정렬하여 할당한다.
- RoundRobinAssignor : 모든 파티션을 컨슈머에서 번갈아가면서 할당한다.
- StickyAssignor : 최대한 파티션을 균등하게 배분하면서 할당한다.