# 프로세스 동기화 (Process Syncronization)

Processs Manager의 주 역할
- CPU Scheduling, 동기화

Co-operating Process : 다른 프로세스에 영향을 받거나 끼치는 프로세스
- 반대 : Independant Process
- Co-operating Process가 Independant Process보다 많다

Co-operating Process 예
- 프로세스 간 통신 : Email
- 프로세스 간 자원 공유 : 메모리 상의 자료, DB 등 (기차표 예매, 주식 매매 등)

동기화 : 공유 데이터 (여러 프로세스가 공유하는 데이터) 에 프로세스들이 접근할 때 순서를 정함으로써 데이터의 일관성을 지키는 것
- 동기화가 제대로 되지 않으면 멀티스레딩 환경에서의 Output이 달라질 수 있다 (일관성이 사라지는 심각한 문제)

임계구역 문제 (Critical Section Problem)
- 멀티 스레드 환경에서 스레드들이 공유하는 데이터(공통 변수, 테이블, 파일) 들을 업데이트 하는 부분을 임계구역이라 함
- 적절한 동기화 없이 무턱대고 임계 구역을 업데이트하면 일관성이 깨짐으로서 심각한 문제가 발생할 수 있음

임계구역 문제의 해결
- 상호 배타적 방법 (Mutual Exclusion) : 오직 한 스레드만 임계구역에 접근할 수 있도록 제한
- 진행 (Progress) : 어떤 스레드를 먼저 실행시킬 지 유한한 시간 내에 결정
- 유한 대기 (Bounded Waiting) : 모든 스레드들이 유한 시간 내에 실행되도록 설정 (무한 대기를 금지시킴)

임계구역 문제와 동기화
- 임계구역 문제를 해결
- 프로세스 / 스레드 실행 순서를 제어
- Busy wait 등의 비효율성을 제거

동기화를 위한 Tools
- Semaphore
- Monitors
- Misc

# 세마포어 (Semaphore)
철도의 신호기, 교대 수기 신호를 뜻함
- 동기화 문제 해결을 위한 SW 도구
- 정수형 변수 + 두 개의 동작 (P, V)로 구성됨

P, V
- P (Proberen) -> acquire()
- V (verhogen) -> release()

세마포어를 표현하는 간단한 Pseudo code

class Semaphore {

  int value; // 동시에 접근 가능한 프로세스의 수를 뜻함

  void acquire() {

    value--;

    if(value < 0)
      add this process or thread to list;
      block;

  }

  void release() {

    value++;

    if(value <= 0)
      remove a process P from list;
      wakeup P;

  }

}

세마포어의 사용 목적
1. 한 번에 접근가능한 프로세스 수를 제한함으로써 동기화 구현 (Mutual Exclusion)
2. 프로세스의 실행 순서를 제어
