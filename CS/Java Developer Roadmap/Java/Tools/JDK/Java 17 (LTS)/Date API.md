[출처 : Baeldung - java 8 date time intro ](https://www.baeldung.com/java-8-date-time-intro)

### Introduction to the Java 8 Date/Time API
---
#### 1. Overview
---
Java 8은 오래된 java.util.Date 와 java.util.Calendar의 단점을 개선하기 위해 Date와 Time을 위한 새로운 API들을 발표했습니다.

이 튜토리얼에서는 기존의 Date와 Calendar API의 문제점들과 새로운 Java 9의 Date와 TIME API를 통해 어떻게 개선했는지 이야기해 봅시다.

우리는 새로운 자바 8 프로젝트에 포함된 java.time 패키지의 주요 클래스( LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Period, duration과 이것들을 도와주는 APII들)에 대해서도 알아보겠습니다. 

#### 2. 기존 Date/Time API들의 문제점들
---
- 쓰레드 안전성 - Date와 Calendar 클래스들은 쓰레드 안정성이 확보되지 않았으며 개발자들에게 쓰레드 안정성을 다루기 위한 추가 코드를 작성하고 동시성 문제를 디버그하기 어렵게 하여 두통을 야기하는 문제들을 남겨두었습니다. 반면에 자바 8의 새로운 Date와 Time API들은 불변성과 쓰레드 안정성이 있습니다. 그러므로 개발자들은 동시성에 대한 골치아픔을 겪지 않아도 됩니다.

- API 디자인과 이해의 쉬움 - 이전의 Date와 Calendar API들은 부적절한 날짜 기능 매서드들과 함께 잘못 설계 되었습니다. 새로운 Date/Time API는 ISO 기준과 날짜, 시간, 기간에 대한 일관된 도메인을 따릅니다.

- 시차적용날짜(ZonedDate )와 시간(Time) - 기존 API들은 개발자들은 추가적인 타임존 로직을 작성을 작성해야 했습니다. 하지만 새로운 API들은 로컬 타임과 시차시간을 ZonedDate와 Time API를 통해 다룰 수 있습니다. 

#not-done-yet 
#java 
#date
#time