# 양희재 운영체제 6강

## 프로세스
프로세스 : 실행 중인 프로그램
-프로세스의 구성 : Code(Text), Data, Stack

## 프로세스의 상태 구분
- New : 메인 메모리에 적재됨
- Ready : 실행 준비가 완료됨
- Running : 실행 (CPU)
- Wait : 대기 상태
- Terminated : 프로세스 종료

## 멀티프로그래밍 : 메모리에 복수의 프로그램을 올리는 것
- 현대 OS 구조
- Degree of Multiprogramming : 프로그램을 올릴 수 있는 정도 (개수)

## I/O Bound vs CPU Bound
### Bound : 주로 하는 일
- I/O Bound는 프로그램이 I/O 위주
- CPU Bound는 프로그램이 연산 위주
- OS의 Job Scheduler는 I/O Bound와 CPU Bound의 배합을 적절히 하여 효율적으로 스케줄링 해야 함 

## Medium-term Schedule
- 예시) 서버에 올라와 있는 한 사용자가 오랫동안 활동이 없을 때
- 서버는 해당 사용자의 프로세스 정보를 디스크에 저장하고 메인 메모리에서 내림 (Swap Out)
- 사용자가 복귀하면 디스크에서 메인 메모리로 올림 (Swap In)
- 이를 Swapping 기법이라 함

## Context Swtiching
현재 처리중인 프로세스에서 다른 프로세스로 넘어가는 것
- Scheduler에 의해 어떤 프로세스로 넘어갈 지 결정됨
- Dispatcher에 의해 처리중이었던 현재 프로세스 상태를 저장, PCB값을 교채되는 프로세스의 값으로 복원
- Context Switching은 순수한 오버헤드이다
