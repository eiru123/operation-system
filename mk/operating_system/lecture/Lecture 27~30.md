# 파일 할당


보조기억장치

- 하드디스크 : track(cylinder), Sector로 구분.
- 하드디스크에 접근할 때 블록 단위로 Read / Write함
- 디스크 : pool of free blocks
- 파일은 디스크의 블록 단위로 저장되기 때문에, 파일 사이즈와 디스크 할당 크기는 다르다

파일 할당 종류

- 연속할당
- 연결할당
- 색인할당

연속할당

- 각 파일에 대해 연속된 블록에 할당
- 빠르다 (디스크의 헤더 이동이 최소화되기 때문)
- 순차 Read, 특정부분 Read 모두 가능하다(Sequential access, Direct access)
- 동영상, 음악, VOD에 적합하다
- IBM VM/CMS에서 사용 중
- 단점 : 디스크에서 파일을 삭제할 때 외부 단편화가 발생한다 (Compaction 가능하나 시간 매우오래걸림)
- 단점 2 : 파일을 만들 때 이 파일의 크기를 알 수 없다
  -> 어느 hole에 배치해야 하는지 결정하기 쉽지 않다
  -> 파일의 크기가 계속 증가할 가능성이 있기 때문에 기존 hole 배치로는 불가능하다
  
 연결할당
  
 - 파일 : Linked list of data blocks
 - 파일 디렉토리는 제일 처음 블록을 가리킨다
 - 각 블록은 포인터 저장을 위해 4byte 이상을 추가로 사용해야 함
  
 연결할당에서 새로운 파일 만들기
 - 비어있는 임의의 블록을 첫 블록으로 설정
 - 파일이 커지면 다른 블록을 할당받고 연결 (linked list)
 - 따라서 외부 단편화가 없다
 - 단점 : Direct Access 불가능, 포인터 저장을 위한 추가 공간 낭비
 - 단점 2 : 블록 포인터가 끊어지면 나머지 블록에 접근할 수 없음 -> 신뢰성 낮음
 - 단점 3 : 느리다 (헤더가 오락가락)
 
 FAT 파일 시스템 (File Allocation Table)
 - MS/DOS, OS/2, Windows 등에서 사용 중
 - 포인터들만 모은 테이블(FAT)를 별도 블록에 저장함
 - FAT 손실 시 복구를 위해 이중으로 저장
 - Direct Access 가능
 - FAT는 일반적으로 메모리 캐싱
 
 색인할당
 - Unix/Linux에서 사용
 - 파일 당 한개 이상의 index block을 추가로 사용
 - 인덱스 블록은 포인터의 모음
 - 디렉토리는 인덱스 블록을 가리킴
 
 ![image](https://user-images.githubusercontent.com/32284527/137625932-6248c148-3316-4699-85f3-816ab84fda95.png)

- Direct Access 가능
- 외부 단편화 없음
- 단점 : 공간낭비
- 단점 2 : 인덱스 블록을 하나만 사용하면 파일의 최대 크기에 한계가 있음
-   ex) 블록 사이즈가 1KB -? 4 * 256 -> 256개의 인덱스 -> 파일 사이즈가 256KB로 고정.
-   이를 해결하기 위해 Linked, MultiLevel, Combined index를 사용한다

Linked, MultiLevel, Combined
- Linked : 다른 블록을 Linked List 형식으로 연결해 추가적인 인덱스 블록을 사용
- MultiLevel : tree 형태로? 블록의 계층 구조를 두어 사용
- Combined : 두 방식을 혼합하여 사용

# 디스크 스케쥴링

디스크 접근 시간 : Seek Time + Rotational Delay + Transfer Time
- Seek Time이 제일 길다
- 다중 프로그래밍 환경에서 디스크 큐를 처리하는 법 (=Seek Time을 최소화 하는 법)

FCFS
- 선입선출
![image](https://user-images.githubusercontent.com/32284527/137626079-7aec0f55-db8f-4877-beb5-580ed2b4a870.png)


SSTF(Shortest Seek Time First)
- Seek Time이 가장 작은 요청부터 처리
- 모든 경우에 Optimal 하지는 않다
- Starvation 위험이 있음(Priority Queue 방식과 동일한 문제점)

![image](https://user-images.githubusercontent.com/32284527/137626112-2272b739-e3d9-4a65-b8ee-edc8a77c343a.png)

SCAN
- 헤드가 디스크 전체를 계속 훑음
- 
![image](https://user-images.githubusercontent.com/32284527/137626131-a2168361-c5b6-45c1-ab73-8162534c1fdb.png)

Circular SCAN(C-SCAN), LOOK

![image](https://user-images.githubusercontent.com/32284527/137626152-dddb62d0-700d-49ce-9c7b-be5f9dc4ae09.png)








 
 
 
