# SJF (Shortest-Job First)
- 가장 짧은 프로세스를 우선적으로 처리
- 이론적으로 제일 최적 (증명됨)
- But 현실성이 없음 (프로세스 수행 시간을 예측해야 할 필요가 있음)
- 선점, 비선점 모두 가능
- 선점이냐 비선점이냐에 따라 프로세스의 평균 대기 시간이 변함
- 선점 SJF = Shortest Remaining Time First (최소 잔여시간 우선)

# Priority (우선순위)
우선순위를 기준으로 프로세스의 수행 순서를 결정함
- Linux / Unix의 경우 Priority Integer의 작을수룩 높은 우선순위를 가짐

우선순위 결정 요소
- 내부적 : 시간제한, 메모리 요구량, I/O to CPU Burst
- 외부적 : 유료 서버의 경우 돈을 많이 낸 순서대로, or 정책에 따라 결정됨

- 선점, 비선점 모두 가능
- 문제점 : 기아 현상 (프로세스의 장기간 대기 현상)
- 기아 현상의 해결 방법 : Aging 전략 (대기시간에 비례해 우선순위가 높아짐)

# Round Robin
- 모든 프로세스를 Time Quantum(Time Slice) 만큼씩 처리
- 선점 방식만 가능
- 프로세스의 평균 대기 시간은 Time Quantum 사이즈에 민감하게 반응함
- if Time Quantum이 무한일 경우 = FCFS와 같은
- if Time Quantum이 0일 경우 : Process Sharing 형태 (But Context Switching이 매우 빈번히 발생해 Overhead 유발)
- Time Quantum은 일반적으로 10 ~ 100ms로 설정함
