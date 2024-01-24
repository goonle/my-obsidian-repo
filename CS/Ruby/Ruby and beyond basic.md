언어로서 Ruby는 몇몇 다른 구현체가 있다. 본문에서는 커뮤니티에서 자주 거론되는 MRI(마츠의 Ruby 인터프리터)나 CRuby(C로 작성된 Ruby) 같은 래퍼런스 구현체에 대해 서술하고 있지만, 다른 것도 있다.

이들은 특정 상황에서 유용할 떄가 있는데, 다른 언어 호긍ㄴ 환경과의 추가 통합을 지원하거나 MRI가 지원하지 않는 특별한 기능을 가지거나 한다.
- [JRuby](http://jruby.org/)는 JVM(Java 가상 머신) 위에서 구동되는 Ruby입니다. JVM의 최적화 JIT 컴파일러, 가비지 컬렉터, 병렬 스레드, 툴 에코시스템, 그리고 다양한 라이브러리 집합을 활용합니다.
- [Rubinius](http://rubini.us/)는 ‘Ruby로 쓰인 Ruby’입니다. LLVM 위에 구축되어, Rubinius는 다른 언어 역시 구축된 멋진 가상 머신 위에서 활동합니다.
- [mruby](http://www.mruby.org/)는 Ruby의 경량 구현체로 애플리케이션 안에 링크되거나 포함시킬 수 있습니다. Ruby의 창시자인 유키히로 “Matz” 마츠모토가 개발을 이끌고 있습니다.
- [IronRuby](http://www.ironruby.net/)는 “.NET Framework과 강력하게 통합된” 구현체입니다.
- [MagLev](http://maglev.github.io/)는 “통합된 개체 지속성과 분산 공유 캐시를 가진 빠르고, 안정적인 Ruby 구현체”입니다.
- [Cardinal](https://github.com/parrot/cardinal)는 “[Parrot](http://parrot.org/) 가상 기기을 위한 Ruby 컴파일러”(Perl 6)입니다.