# 보호와 공유

보호 : 해킹 등을 방지
- 페이지 테이블 엔트리마다 r, w, x (Reader, Writer, Execute) 비트를 두어 접근 제어 가능
- if CPU가 w 권한이 없는 프레임에 w 명령을 시도하면 페이지 테이블이 interrupt -> 강제 종료시킴

공유 : 메모리 낭비 방지
- 같은 프로그램을 쓰는 복수의 프로세스는 Code 공유 가능 -> 프로세스의 페이지 테이블
- 코드 영역이 같은 주소값이 되도록 수정
- 이는 non-self modifying code(=reentrant code, pure code)가 아닌 경우만 해당함

# Segmentation

Segment : 뭉치

Segmentation : 프로세스를 논리적 내용(=Segment)로 잘라 메모리에 배치
- 이 떄 프로세스는 Segment의 집합
- Segment Size는 같지 않음

Segment를 메모리에 할당
- MMU 재배치 레지스터 값을 수정
- CPU는 프로세스가 연속된 공간에 있는 것으로 착각함
- 이 때 MMU는 Segment Table이 됨

페이징 vs 세그멘트
- 페이징 : 일정한 크기로 자름
- 세그멘테이션 : 일정하지 않은 크기(=의미 단위)로 자름

세그멘테이션 예
![image](https://user-images.githubusercontent.com/32284527/135752532-f6c6fc2f-9784-4e46-812b-0b27f9a5c470.png)

# 주소 변환
논리 주소 : CPU가 내는 주소. Segment 번호 S + 변위 D

논리주소 -> 물리주소
- Segment Table 내용 = base + limit
- S : Segment Table 인덱스값
- S의 내용으로 base, limit 파악
- limit을 넘어 액세스하는 경우 Segment Violation Interrupt
- 물리 주소 : base[s] + d

세그멘트는 페이징보다 보호와 공유에 우월하다
-> 의미 단위로 자르기 때문에 보호에 효과적 (r, w, x 엔트리 설정이 용이하다)

Segmentation 단점
- 외부 단편화 : 사이즈가 일정하지 않아 hole 사이즈도 일정하지 않음 -> 외부 단편화 유발 (사실상 페이징 하는 의미가 사라짐)
- 외부 단편화로 인해 세그멘테이션은 페이징보다 덜 쓰임

새로운 개념 : 세그멘테이션 + 페이징 : 세그멘트를 페이징한다
- intel의 80x86
- 페이지 테이블과 세그멘트 테이블 두 가지가 다 필요해 속도가 느려짐

# 가상 메모리

물리 메모리의 크기 한계를 극복
-> 물리메모리보다 크기가 큰 프로세스를 돌리기 위해 현재 실행에 필요한 부분만 돌린다
- 요구 페이지(Demanded page)만 돌림

![image](https://user-images.githubusercontent.com/32284527/135752742-6bd83e5c-c71a-4967-ac64-119e47d7c732.png)

if CPU가 invalid되있는 페이지를 요구하면 (Page fault)
->interrupt 후 빈 공간에 요구된 페이지를 올린다(Page fault routine)

현재 가상 메모리는 Demanded Paging 기법이라 봐도 무방

Demanded Paging을 위해 필요한 조건
- Swap Device
- Valid bit

Pure Demand Paging : 진짜 필요한 페이지만 가지고 오기
- 프로그램 실행 시 아무것도 메모리에 적재하지 않음
- 속도가 느림. but 메모리 절약성 좋음

Prepaging : 필요해 보이는 페이지 몇개를 프로그램 시작 시 미리 램에 적재
- 속도 빠름 but 메모리 절약성이 떨어짐

Swaping과의 차이점 : 단위 (프로세스 단위 vs 페이지 단위)
