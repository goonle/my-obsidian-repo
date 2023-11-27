> [참고] SpringFox Swagger2에 대한 어노테이션

|Annotation|설명|
|---|---|
|@Tag|- Swagger UI에서 API를 그룹화할 수 있습니다.|
|@Operation|- 어노테이션을 사용하면 Swagger UI에서 API 작업에 대한 정보를 제공할 수 있습니다.- summary 속성은 API 작업의 간략한 설명을, description 속성은 API 작업의 상세한 설명을 작성합니다.|

```java
@RestController
@RequestMapping(value = "/api/v1/rest")
@Tag(name = "Restful", description = "restful API 구성")
public class RestfulController {

	/**
     * RESTful API의 GET을 이용한 방식
     *
     * @return
     */
    @GetMapping("/user")
    @Operation(summary = "사용자 조회", description = "사용자 아이디를 기반으로 사용자 정보를 조회합니다.")
    public ResponseEntity<ApiResponse<Object>> restfulGet(@RequestParam String userId) {
        String result = "";

        log.debug("userId :: " + userId);

        ApiResponse ar = ApiResponse.builder()
                .result(result)
                .resultCode(SuccessCode.SELECT.getStatus())
                .resultMsg(SuccessCode.SELECT.getMessage())
                .build();
        return new ResponseEntity<>(ar, HttpStatus.OK);
    }
}
```

#restful #api