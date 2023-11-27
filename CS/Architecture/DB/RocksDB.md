[출처 : SJ BackEnd Log : 기본개념 RocksDB란?](https://well-made-codestory.tistory.com/8)
### RocksDB?
---
- RocksDB 는 빅데이터 처리를 관리하기 위해 만들어진 Key-value 엔진이다.
- RocksDB 는 LSM(로그 구조 병합 트리)를 기반으로 C++ Library 형태로 제공되며 Facebook에서 Google의 LevelDB를 기반으로 제작되어 **flash drive**에 data를 저장하는데 적합하다.
- RocksDB 는 open source software로 memory, falsh memory, hard disk 등 여러 환경에서 실행 가능하며, 여러 설정을 조정할 수 있다.