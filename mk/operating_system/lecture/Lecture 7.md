# 양희재 운영체제 7강

## CPU Schduling
- 선점 : CPU 서비스가 끝나지 않았어도 강제로 스케줄링 할 수 있음
- 비선점 : CPU 서비스가 I/O 서비스 등을 만나 끝나기 전에는 스케줄링 불가능

## 스케줄링 기준
- CPU 이용률
- 처리율
- 반환 시간
- 대기 시간
- 응답 시간

## 스케줄링 알고리즘 종류
- FCFS
- SJF
- Priority
- Round Robin
- MultiLevel Queue
- MultiLevel Feedback Queue

## FCFS
- 먼저 온 프로세스를 먼저 처리
- 겉보기에 가장 공정
- 재수없이 처리시간이 긴 프로세스가 짧은 프로세스 앞에 오면 손해가 크다 (평균 대기시간의 증가) -> 호위 효과(Convey Effect)
