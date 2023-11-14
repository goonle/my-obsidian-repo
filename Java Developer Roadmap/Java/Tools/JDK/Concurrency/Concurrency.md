---

---
### 뜻
---
동시성

### 오라클 자바 doc에서 발췌
---
컴퓨터 사용자들은 그들의 시스템이 동시에 더 많은 것들을 할 수 있다고 당연하게 여깁니다. 그들은 다른 어플리케이션에서 파일을 다운로드하고 프린트 순서를 관리하며 음악을 들으면서 워드프로세서로 일하는 것을 동시에 할 수 있다고 생각합니다. 

심지어 한개의 어플리케이션도 종종 한번에 한가지 이상을 할 수 있다고 생각합니다.

예를 들면, 말했던 음악을 듣는 어플리케이션은 반드시 동시적으로 디지털 오디오를 네트워크에서 꺼내 읽고 압축을 풀고 재생하고 화면에 업데이트합니다. 

워드 프로세서는 항상 키보드와 마우스 이벤트에 대해 반응하도록 준비되어야 합니다. 프로그램이 텍스트를 변환하고 화면에  업데이트하는게 얼마나 바쁘든 말입니다. 

이러한 일들을 할 수 있는 소프트웨어를 Concurrent 소프트 웨어라고 합니다.


자바 플랫폼은 자바 프로그래밍 언어와 자바 클래스 라이브러리에서 기본적인 동시성 지원을 통해 바닥부터 concurrent 프로그래밍까지 지원하도록 설계되어 있습니다.
버전 5.0부터 자바 플랫폼은 고성능의 concurrency API들이 탑재되어왔습니다.

---
# Oracle docs
The Java Tutorials have been written for JDK 8. Examples and practices described in this page don't take advantage of improvements introduced in later releases and might use technology no longer available.  
See [Java Language Changes](https://docs.oracle.com/pls/topic/lookup?ctx=en/java/javase&id=java_language_changes) for a summary of updated language features in Java SE 9 and subsequent releases.  
See [JDK Release Notes](https://www.oracle.com/technetwork/java/javase/jdk-relnotes-index-2162236.html) for information about new features, enhancements, and removed or deprecated options for all JDK releases.
## Lesson: Concurrency
---
Computer users take it for granted that their systems can do more than one thing at a time. They assume that they can continue to work in a word processor, while other applications download files, manage the print queue, and stream audio. Even a single application is often expected to do more than one thing at a time. For example, that streaming audio application must simultaneously read the digital audio off the network, decompress it, manage playback, and update its display. Even the word processor should always be ready to respond to keyboard and mouse events, no matter how busy it is reformatting text or updating the display. Software that can do such things is known as _concurrent_ software.

The Java platform is designed from the ground up to support concurrent programming, with basic concurrency support in the Java programming language and the Java class libraries. Since version 5.0, the Java platform has also included high-level concurrency APIs. This lesson introduces the platform's basic concurrency support and summarizes some of the high-level APIs in the `java.util.concurrent` packages.