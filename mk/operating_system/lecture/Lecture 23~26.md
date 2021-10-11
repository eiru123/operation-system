# 지역성의 원리 (Locality of reference)
- 메모리 접근은 시간적, 공간적 지역성을 가진다
- 실제 page fault 확률은 따라서 매우 낮다 (자주 부르는 메모리 영역은 항상 비슷비슷하다)

# Page Replacement(페이지 교체)

Demand Page에서 메모리가 꽉 찼을 때
- 필요없는 페이지를 backing store로 몰아내고(page-out) 그 빈자리에 새로운 페이지를 올린다(page-in)
- page-out된 페이지를 victim page라고 한다

Victim Page
- 쫓아낸 페이지는 swap device에 새로 write해야할까? : Yes or No
- Yes인 경우 : 페이지가 메모리에서 변경된 이력이 있을 때, No : 없을 때.
- 페이지가 메모리에서 변경된 이력을 확인하기 위해 modified bit를 도입. 0이면 변경이력 없음, 1이면 있음
- victim page는 일반적으로 modified bit가 0인 페이지에서 선정한다

Page Reference String : CPU가 참조하는 페이지를 기록한 String.
- ex) CPU가 내는 주소가 100 101 102 432 612 103 104 611 612, page size는 100bytes일 때
- page num : 1 1 1 4 6 1 1 6 6
-> Page Reference String : 1 4 6 1 6

# 페이지 교체 알고리즘
FIFO : 선입선출. 가장 먼저 올라온 페이지를 victim page로 선정
- 간단함
- 초기화 코드는 앞으로 사용하지 않을 것이라는 믿음을 근거로 한다
- Belady's Amonaly : 메모리 사이즈가 증가함에도 불가하고(프레임 갯수가 늘어남에도 불구하고) 오히려 Page Fault가 증가하는 현상.

![image](https://user-images.githubusercontent.com/32284527/136777898-9a36d729-493f-4834-9d19-64226fda3b8b.png)

OPT(Optimal) : 앞으로 제일 쓰이지 않을 것 같은 페이지를 교체 (PRS를 참조)
- 현실성 없다 : 미래를 예측하기 어려움(SJF와 동일함)

LRU(Least-Recently Used) : 최근에 가장 안 쓰인 Page를 Victim으로 선정한다
- 최근에 쓰지 않았으면 앞으로도 쓰지 않을 것이라는 믿음에서 비롯
- 완전 최적은 아니나 쓸만하기 때문에 대중적으로 이용된다

Global vs Local Replacement
- Global : 메모리 상의 모든 프로세스 페이지 교체
- Local : 메모리 상의 자기 프로세스 페이지 교체
- 성능 : Global이 Local보다 효율적일 수 있다

# 프레임 할당

쓰래싱 현상(Thrashing) : 프로세스 개수가 일정 범위를 넘어서면 빈번한 page in and out으로 인해 CPU 이용률이 오히려 감소함
- 빈번한 I/O가 원인

![image](https://user-images.githubusercontent.com/32284527/136778432-16cf2283-73f5-4cbf-9c81-0116791327b8.png)

- 해결책 1 : Local Replacement를 사용한다
- 해결책 2 : 프로세스당 적절한 수의 메모리를 할당한다

Static한 할당과 Dynamic한 할당

Static
- Equal(동일할당): 모든 프로세스에 동일한 프레임 개수 할당
- Proportional(비례할당): 프로세스 사이즈에 비례하여 프레임 개수 할당

Dynamic
- Working Set Mode: Working Set만큼의 메모리를 할당
- 과거에 사용된 페이지 번호를 시간 단위로 묶어(Working Set) Working Set Size만큼 할당

![image](https://user-images.githubusercontent.com/32284527/136778854-e4a90988-863c-487a-9534-ad65a5559654.png)

- Page-Fault Frequency(PFF)
- page fault 발생 비율의 상한 / 하한선을 둠
- page fault ratio가 상한선을 넘으면 프레임을 더 할당
- 반대로 하한선 밑으로 떨어지면 프레임을 회수함

![image](https://user-images.githubusercontent.com/32284527/136779021-911949ae-9c31-412f-93e4-9e71eca5dc50.png)

# 페이지 크기

일반적으로 4KB -> 4MB 사용
- 점차 커지는 트렌드 (프로세스 사이즈가 커짐에 따라)

어떤 페이지 크기가 좋을까?
- 내부 단편화 측면에서 : Big < Small
- Page in-out 측면에서 : Big > Small
- 페이지 테이블 크기 측면에서 : Big > Small
- Memory Resolution(필요한 페이지만 메모리에 올라왔는지의 정도) 측면에서 : Big < Small
- Page Fault 발생 확률 측면에서 : Big > Small

페이지 테이블의 발전
- 원래는 별도 Chip을 사용(TLB 캐시)
- 기술이 발달함에 따라 캐시 메모리는 On-Chip(CPU 안에 들어가버림) 형태로 발전
- TLB 역시 On-Chip으로 발전함




