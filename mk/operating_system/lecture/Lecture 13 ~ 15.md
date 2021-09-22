# 운영체제 13 ~ 14강

전통적 동기화 예제
- 생산자 소비자 문제
- Reader, Writer 문제
- 식사하는 철학자 문제

생산자-소비자 문제
- 생산자가 데이터 생성, 소비자가 데이터 소비
- Bounded Buffer : 생산된 데이터를 일단 버퍼에 저장. 버퍼가 가득 찬 경우 push 불가(생산자), 버퍼가 빈 경우 pop 불가(소비자)

예시

class Buffer {
  int buf; // Maximum size
  int size; // 현재 버퍼에 push된 갯수
  int count; // 넣는 위치
  int in; // 빼는 위치
  int out;
}

in = (in + 1) % size
out = (out+1) % size

- 해당 코드는 잘못된 결과가 나올 확률이 높음(or 실행 불가)
- 동기화 필요 (공통변수 동시 업데이트로 인한 임계구역 문제)

busy wait 문제 : 생산자가 버퍼에 push하지 못하거나,  소비자가 버퍼에 pop하지 못하는 상태로 무한 루프
- 세마포를 사용하거나, 강제로 block 시켜 무한 루프 탈출시키는 조치가 필요함

Reader, Writer 문제
- Reader는 읽기만 가능.
- Writer는 읽기, 쓰기 모두 가능
- 이 경우 Reader는 임계구역에 다중 접근 허용 가능하지만, Writer는 Mutual Exclusion이 필요하다

Reader, Wrtier 우선권 정리
- first reader problem : reader 우선
- second reader problem : writer 우선
- third reader problem : 우선권을 알 수 없음

식사하는 철학자 문제
- 5명의 철학자, 5개의 젓가락(쌍 아님)
- 생각 -> 식사 -> 생각 -> 식사 -> ...
- 식사를 위해서는 두 개의 젓가락이 필요함

코드를 짜서 식사하는 철학자 문제를 돌려보면? : 모든 철학자에 대해 Starvation 현상 발생
- 이유 : Deadlock

교착상태 (DeadLock)

교착상태의 필요조건
- Mutual Exclusion
- Hold and Wait
- No preemption
- Circular wait

자원
- 동일 자원 : 동일 형식 자원이 여러 개 있을 수 있음(ex: CPU 2, printer 3)
- 자원의 사용 : 요청(request), 사용(use), 반납(release)
- 자원 할당도 : 어떤 자원이 어떤 프로세스에 할당되었는가? 어떤 프로세스가 자원을 할당받으려고 대기중인가?

![KakaoTalk_20210922_195447425](https://user-images.githubusercontent.com/32284527/134331468-9df673fe-b72e-44ec-bdde-7f1589fc4592.jpg)

- Deadlock이 발생하려면 화살표들이 원형을 구성해야 함 (환형 구조)
- 식사하는 철학자를 그림으로 표현하면 완벽한 환형 대기를 구성함

식사하는 철학자의 환형 대기를 파괴하는 예시
- 짝수 번 철학자는 오른쪽 pick -> 왼쪽 pick 순서로, 홀수 번 철학자는 반대 순서로 젓가락을 집도록 수정.

교착상태 처리 방법
1. 방지
2. 회피
3. 검출 및 복구
4. 무시


1. 방지
- 상호 배타를 파괴 (자원 공유를 가능하도록 수정) : 매우 어려워서 사실상 불가능.
- 보유 및 대기 조건을 수정 (Hold and Wait 조건을 까다롭게 수정): 성능 저하 발생 가능성이 있음.
- 비선점에서 선점으로 (자원 선점 가능하도록 수정) : 사실상 불가능.
- 환형 대기 붕괴 : 자원 활용율이 저하될 수 있음.

2. 회피
- 자원 요청 관리를 세심하게 하여 Deadlock 방지
- Safe Allocation, Unsafe Allocation
- OS는 Unsafe Allocation이 발생하지 않도록 조정함.(Banker's Algorithm 참고)

3. 검출 및 복구
- Deadlock을 허용
- 주기적으로 deadlock 검사, 발견 시 복구함
- OS에서 주기적으로 검사해야 해서 오버헤드 발생
- 복구 방법 : 프로세스 일부를 강제 종료, 자원 선점중인 일부 프로세스 할당

4. 무시 : 아무런 조치도 취하지 않음 (Deadlock은 희귀한 현상이라는 믿음에서 기인함)

