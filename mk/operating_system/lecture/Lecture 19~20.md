# 연속 메모리 할당

다중 프로그래밍 환경
- 부팅 직후의 메모리 상태 : OS + big single hall
- 프로세스 새성 & 종료를 반복하면 : 여러개의 작은 메모리 구멍이 생기기 시작함(Scattered hole)
- 메모리 단편화( Memory fragmentation) : hole들이 불연속하게 흩어져 절대적인 메모리 사용 가능 공간은 충분하지만, 실제로는 프로세스를 적재할 수 없는 상황

# 연속 메모리 할당 방식
First fit : 최초적합. 넣을 수 있는 최초의 공간에 할당
Best fit : 최적적합. 넣을 수 있느 hole 중 사이즈가 비슷한 곳에 할당
Worst fit : 최악적합. Best fit과 반대로 수행.
- 성능 비교했을 때 속도는 first fit이 우수, 이용률은 first fit, best fit이 우수.
- 주로 Best fit을 사용함

외부 단편화로 발생하는 메모리 낭비량 : 전체 메모리의 1/3 수준이다

# 페이징

페이징 : 하나의 프로세스를 쪼개서 hole에 할당한다 (코끼리를 냉장고에 넣기)

Q) 프로세스 메모리가 연속되지 않아도 작동하게 하려면?
-> MMU의 Relocation 레지스터를 복수로 두어 처리한다
- 복수의 Relocation 레지스터를 Page Table이라 칭함.

페이징 메모리
 - 프로세스를 일정 크기로 잘라 메모리에 할당
 - 프로세스는 페이지의 집합
 - 메모리는 프레임의 집합
 - MMU 내의 재배치 레지스터를 통해 페이지를 프레임에 할당한다
 - CPU는 프로세스 메모리가 연속되었다고 착각함

# 주소 변환

논리 주소
- CPU가 내는 주소는 2진수 표현 (m비트)
- 하위 n 비트는 offset 또는 변위(displacement)(n값은 페이지 사이즈가 결정한다)
- 상위 m - n 비트는 페이지 번호를 의미

주소변환 : 논리 주소 -> 물리 주소
- 페이지 번호 p는 페이지 테이블 인덱스 값.
- p에 해당하는 테이블 내용이 프레임 번호 f
- 변위 d는 변하지 않는다

내부 단편화 (internal fragmentation)
- 프로세스 크기가 페이지 크기의 배수가 아니라면 마지막 페이지는 한 프레임을 채우지 못함
- 만약 프로세스 크기가 15bytes이고, 페이지 사이즈가 4bytes라면 -> 마지막 프레임은 1byte가 빈다
- 남은 공간만큼 메모리가 낭비되지만, 매우 미미하다 (낭비 최대량 : 페이지 사이즈 - 1byte)

페이지 테이블을 만드는 방법
- CPU 레지스터로 (장점 : 빠르다 단점 : 작다)
- 메모리 안에 할당(장점 : 크다 단점 : 느리다)
- TLB(Translation Look-Aside Buffer) : 캐시의 한 종류. 위 두가지의 중간 포지션으로 주로 이용됨

Effective Memory access time(TLB에서 유효 메모리 접근 시간)
ex)
메모리 접근 시간 Tm - 100ns
메모리 읽는 시간 Tb = 20ns
캐시 히트비율 hit ratio = 80%

이때 유효 메모리 접근 시간 Esms
(Tb + Tm) * h + (1 - h)(Tb + 2Tm)
= 120ns * 0.8 + 220ns * 0.2 = 140ns

# 문제 예시

![image](https://user-images.githubusercontent.com/32284527/135238389-7a439bd8-9a62-4796-9ae1-3ad5c94452ed.png)

![image](https://user-images.githubusercontent.com/32284527/135238427-6cf7e5cf-a00e-4a12-9af4-699f1aa45718.png)
