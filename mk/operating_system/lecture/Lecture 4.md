# 양희재 운영체제 4강 정리

## 이중 모드
한 컴퓨터를 동시에 많은 유저들이 사용할 때 한 사람의 실수가 다른 사람들에게 영향을 끼칠 수 있음
(STOP, RESET 명령어 등)
이러한 참사를 방지하기 위해 사용자는 STOP 명령과 같은 치명적인 명령을 사용하지 못하게 하고, 관리자만 사용하도록 함
-> 관리자 모드(Supervisor Mode)의 등장
### 특권 명령
관리자 모드에서만 실행 가능한 명령들. (STOP, RESET 등)

### 관리자 모드 구현
Flag 값에 관리자 Flag를 추가하여 관리자 모드인지 사용자 모드인지 식별할 수 있도록 함.
- OS가 서비스를 실행한다면 : Supervisor Mode
- 사용자가 서비스를 실행한다면 : User Mode

예시) 사용자 서비스가 OS에 무언가를 요청
- ISR (User Mode) -> OS에 의해 ISR 루틴 실행 (Supervisor Mode) -> 완료 (User Mode)

### 이중 모드의 의미
#### 1. I/O Device 보호
- In, Out 등의 IO Device 명령을 특권 명령으로 설정
- Int 명령을 통해 사용자 모드에서 관리자에게 서비스 요청
- if 사용자가 직접 In, Out 명령을 사용하려고 시도하면 : Previlaged Instruction Violation
#### 2. 메모리 보호
- OS 혹은 다른 유저가 우연으로, 혹은 고의로 메모리에 접근하는 것으로부터 보호
##### 메모리를 보호하는 방법
1. CPU로부터 Address Bus를 읽음
2. Address Bus에서 메모리 주소 적합도 평가 (MMU라고 불리는 유닛을 통해 base, limit을 파악 후 평가)
- if 잘못된 메모리에 접근을 시도한다면 : Segmentation Violation
#### 3. CPU 보호
여러 유저가 쓰는 CPU를 보호
- 예시) 어떤 유저가 CPU를 쓰는데 무한루프에 빠졌을 때 : 
- Timer를 두어 만료기한을 설정해 무한히 CPU를 사용하는 것을 방지
