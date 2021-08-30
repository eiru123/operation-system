# MultiLevel Queue Scehduling

프로세스 그룹 짓기
- 시스템, 사용자, 대화형 프로세스 (like 게임), 배치 프로세스 등으로 구분할 수 있음

Single Ready Queue → Several Separate Ready Queue로 변형
- 각 Queue에 우선순위를 부여함
- 우선순위에 따라 CPU Time을 차등 분배함
- 각 Queue는 독립적인 Scheduling 정책을 가짐

# MultiLevel Feedback Queue Scheduling

- 복수의 Queue로 구성
- 마찬가지로 각 Queue는 우선순위를 가짐
- 모든 프로세스는 하나의 입구를 통해 Queue로 진입함
- 프로세스 수행 시간이 길면 다른 Queue로 점진적으로 이동함 (우선순위 밀림)
- 프로세스의 기아 상태가 우려되는 경우 우선순위가 높은 Queue로 이동시킴

그래서 현대의 OS는 어떤 기법을 사용하는가? -> 다양하게 사용 중이다
