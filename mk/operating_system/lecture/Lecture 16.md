# 운영체제 16강

모니터 : 고수준의 동기화 구조
- 공유 자원 + 공유 자원 접근 함수
- 배타 동기 + 조건 동기의 2가지 Queue를 가짐
- 공유 자원 접근함수에는 최대 1개의 스레드만 진입 가능
- 진입 스레드가 조건 동기로 블록되면 세 스레드 진입 가능
- 새 스레드는 조건동기로 블록된 스레드를 깨울 수 있음
- 깨워진 스레드는 현재 스레드가 나갔을 때 진입할 수 있음

자바의 모든 객체는 모니터가 될 수 있다 -> synchronized 키워드

모니터의 사용 목적 
1. Mutual Exclusion
2. Ordering
= 세마포어와 같은 목적. but 좀 더 고수준으로 구현된 것이 특징이다
