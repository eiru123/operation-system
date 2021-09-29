# 주기억장치 관리

메모리의 역사
- Core Memory
- 진공관(약간 전자석?같은 구조)
- 트랜지스터
- 집적 회로(IC)

프로그램의 변천
- 기계어 / 어셈블리어
- C
- 자바 (객체 지향)
- 전제척으로 숫자 -> 문자 -> 멀티미디어 -> Big Data로 변화하는 큰 흐름

# 메모리의 최적화

1. 오버헤드를 줄인다
2. 가상 메모리(Virtual Memory)를 활용한다

메모리 구조 : 주소 + 데이터
프로그램 개발 : 
- 원천 파일(Source file) : 고수준 or 어셈블리 언어
- 목적 파일(Object file) : 컴파일 or 어셈블 된 결과
- 실행 파일(Executable file) : 링크까지 완료된 결과

빌드의 구성 : 컴파일러 + 어셈블러 + 링커 + 로더

MMU(Memory Management Unit)의 역할
1. 주소 할당
2. 재배치(Relocating)
- 프로세스가 메인 메모리에 올라올 때 마다 일정한 주소 대신 가변적으로 위치를 선정함

# 프로그램을 메모리에 올리기

MMU의 재배치 레지스터
- base(시작점), limit(종점)으로 구성
- if base, limit 사이에 다른 프로세스가 접근을 시도 -> 인터럽트
- 상대 주소(logical address)를 절대 주소(physical address)로 변환한다

상대 주소 : CPU가 보는 주소
절대 주소 : MMU가 보는 주소

# OS가 메모리를 아끼는 방법

동적 적재(Dynamic Loading) :  프로그램 실행에 반드시 필요한 루틴 / 데이터만 적재한다
- 정적 적재와(Static Loading)과 반대 개념
- 현재 Os는 동적 적재를 사용함

if 서로 다른 프로세스가 같은 라이브러리를 사용한다면?
- 동적 연결(Dynamic Linking) :  여러 프로그램에 공통으로 사용되는 라이브러리를 각 프로세스가 각각 메모리에 올리는 대신 하나만 골라서 올린다
- DLL(.dll) 파일의 존재 이유!

Swapping : 메모리에 적재됐지만 사용되지 않고 있는 경우, 현재 상태(이미지라고 한다) 그대로 backing store(=swap device)에 보내는 기법
- Backing Store의 크기는 메인 메모리 사이즈 정도면 적당하다
- Linux의 스왑 영역이 Swapping을 위한 공간
- 메인 메모리로 복귀할 때는 Relocating 됨
- 프로세스 사이즈가 크면 Backing Store에 넣기 어렵다 (느리다)
