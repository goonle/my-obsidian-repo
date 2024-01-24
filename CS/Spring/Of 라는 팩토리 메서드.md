
### 결론
---
>[!info]
>Of는 객체를 생성하는 함수다.


### 장점
---
1. 가독성 향상
2. 메소드 체이닝 가능
3. 유지 보수 편리
4. 사용 편리

### 비교
---
```java
# 기존 생성자
@Data
@Builder
public class PerformanceInfo {
    private UUID performanceId;
    private String performanceName;
    private String performanceType;
    private Date startDate;
    private String isReserve;
    private String placeAt;  // New attribute

    // Constructor without "of" method
    public PerformanceInfo(Performance entity) {
        this.performanceId = entity.getId();
        this.performanceName = entity.getName();
        this.performanceType = convertCodeToName(entity.getType());
        this.startDate = entity.getStart_date();
        this.isReserve = entity.getIsReserve();
        this.placeAt = entity.getPlaceAt();
    }
}
```

```java
# of 생성자를 사용한 코드
@Data
@Builder
public class PerformanceInfo {
    private UUID performanceId;
    private String performanceName;
    private String performanceType;
    private Date startDate;
    private String isReserve;
    private String placeAt;  // 새로운 속성 추가

    public static PerformanceInfo of(Performance entity) {
        return PerformanceInfo.builder()
            .performanceId(entity.getId())
            .performanceName(entity.getName())
            .performanceType(convertCodeToName(entity.getType()))
            .startDate(entity.getStart_date())
            .isReserve(entity.getIsReserve())
            .placeAt(entity.getPlaceAt())  // 새로운 속성 설정
            .build();
    }
}
```

### 사용 편의성
---
![[Pasted image 20240124200923.png]]

#java
#of