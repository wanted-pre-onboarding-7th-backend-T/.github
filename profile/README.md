# wanted-pre-onboarding-7th-backend-T

#  팀원 

<table>
  <tbody>
    <tr><th colspan="5">백엔드</th></tr>
    <tr>
      <td align="center"><a href="https://github.com/ffolabear"><img src="https://avatars.githubusercontent.com/u/65614734?v=4" width="130px;" alt=""/><br /><sub><b>김태현(팀장)</b></sub></a><br /></td>
      <td align="center"><a href="https://github.com/jkde7721"><img src="https://avatars.githubusercontent.com/u/65665065?v=4"
      width="130px;" alt=""/><br /><sub><b>김다은</b></sub></a><br /></td>
      <td align="center"><a href="https://github.com/kho903"><img src="https://avatars.githubusercontent.com/u/52434805?v=4" width="130px;" alt=""/><br /><sub><b>김지훈</b></sub></a><br /></td>
       <td align="center"><a href="https://github.com/Byeonghee-son"><img src="https://avatars.githubusercontent.com/u/96256807?v=4" width="130px;" alt=""/><br /><sub><b>손병희</b></sub></a><br /></td>     
      <td align="center"><a href="https://github.com/LEEGIHO94"><img src="https://avatars.githubusercontent.com/u/116015708?v=4" width="130px;" alt=""/><br /><sub><b>이기호</b></sub></a><br /></td>
    </tr>
    <tr></tr>
  </tbody>
</table>

<br/>

# 💾 문서
[팀 노션 페이지](https://jungle-blarney-312.notion.site/c7f263628ee8467cb24c44ed3f11b479?pvs=4)

<br/>

## Git Commit Convention

| 태그이름 | 설명                                                          |
| -------- | ------------------------------------------------------------- |
| feat     | 새로운 기능, 특징 추가                                          |
| style    | 스타일링                                                       |
| fix      | 버그 수정                                                      |
| refactor | 리팩토링 , 코드에영향을 주지 않는 수정                           |
| test     | 테스트 코드 수정, 누락된 테스트를 추가할 때, 리팩토링 테스트 추가  |
| chore    | 빌드 업무 수정                                                 |
| init     | 초기 설정                                                      |
| docs     | 문서 설정                                                      |
| update   | 간단한 수정 작업                                                |
| remove   | 클래스, 메서드 등 삭제                                           |
| comment  | 주석 작성                                                       |

<br/>

## Code Convention

[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) 준수

[XML 설정](https://github.com/google/styleguide/blob/gh-pages/intellij-java-google-style.xml)

<br/>

## Code Name Convetion
- Controller 메소드에서는 HTTP 메서드 이름으로 작성한다.
- Service 메소드는 HTTP 메서드와 중복되지 않는 적절한 이름으로 작성한다.

<br/>
### Controller
- 컨트롤러 메소드는 ResponseEntity<Dto> 리턴한다.
- 예시
```java
@PostMapping
public ResponseEntity<ResponseDto<UserIdResponseDto>> postUser(
        @RequestBody @Valid UserPostRequestDto post) {
    ResponseDto<UserIdResponseDto> result = service.saveUser(post);
    URI location = UriCreator.createUri(URL, result.getData().getUserId());
    return ResponseEntity.created(location).body(result);
}
```
<br/>
### Service
- 요청에 맞는 Dto 를 리턴
- Dto → Entity 클래스로 변환은 도메인별 Mapper 클래스가 담당
- 예시
```java
@Component
@RequiredArgsConstructor
public class UserMapper {

    public User toEntity(UserPostRequestDto post) {
        return User.builder()
                .userName(post.getUserName())
                .email(post.getEmail())
                .password(post.getPassword())
                .build();
    }

    public ResponseDto<UserIdResponseDto> toIdResponseDto(User user) {
        return ResponseDto.<UserIdResponseDto>builder()
                .code(HttpStatus.CREATED.value())
                .data(toIdResponse(user))
                .message(HttpStatus.CREATED.getReasonPhrase())
                .build();
    }

    private UserIdResponseDto toIdResponse(User user) {
        return new UserIdResponseDto(user.getId());
    }
}
```
<br/>

## 깃 브랜치 전략

- 이슈 별로 브랜치 관리

<br/>
