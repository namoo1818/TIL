### 2023.10.23

# 복습
- 기존에는 Controller가 M&V 또는 String을 View Resolver로 보내서 view 화면을 만들고 이것을 클라이언트에게 보냈다. 
- 이제는 순수데이터 그자체를 JSON 형태로 클라이언트에게 바로 보낸다.(@ResponseBody)
- @RestController: @Controller와 @ResponseBody를 합친 것
- @Pathvariable: 메서드 매개변수 이름이 uri의 이름과 다르면 설정.
- @RequestBody: JSON 데이터를 객체로 바인딩해줌.
- ResponseEntity: 클래스 자체를 반환. 여러 생성자가 들어갈 수 있다.(상태코드, 헤더, 데이터)
- 상태코드
  - 1xx: 정보 
  - 2xx: 응답 성공
  - 3xx: 리다이랙션
  - 4xx: 클라이언트 실수
  - 5xx: 서버 실수
- URI와 HTTP Method를 합쳐서 쓸 수 있다
  
# URI
- 목록 GET: localhost:8080/contextroot/api/board
- 상세보기 GET: localhost:8080/contextroot/api/board/{id}
- 등록 POST: localhost:8080/contextroot/api/board
- 수정 PUT: localhost:8080/contextroot/api/board 또는 localhost:8080/contextroot/api/board/{id}
- 삭제 DELETE: localhost:8080/contextroot/api/board/{id}

# 실습
- 크롬에서 talend api tester, json viewer 다운로드
## BoardRestController
```java
@RestController
@RequestMapping("/api")
@Api(tags="게시판 컨트롤러")
@CrossOrigin("*")
public class BoardRestController {

	@Autowired
	private BoardService boardService;

	//1. 목록(검색조건 있을 수도 있고 없을 수도 있다.)
	@GetMapping("/board")
	@ApiOperation(value="게시글 조회", notes="검색조건도 넣으면 같이 가져온다.")
	public ResponseEntity<?> list(){
		List<Board> list = boardService.search(condition); // 검색 조건이 있다면 그것으로 조회
		
		if(list == null || list.size()==0)
			return new ResponseEntity<Void>(HttpStatus.NO_CONTENT);
		return new ResponseEntity<List<Board>>(list, HttpStatus.OK);
	}
	
	//2. 상세보기
	@GetMapping("/board/{id}")
	public ResponseEntity<Board> detail(@PathVariable int id){
		Board board = boardService.getBoard(id);
		if(board==null) {
			return new ResponseEntity<Void>(HttpStatus.NO_CONTENT);
		}
		return new ResponseEntity<Board>(board, HttpStatus.OK);
	}
	
	//3. 등록
	@PostMapping("/board")
	public ResponseEntity<Board> write(Board board){
		boardService.writeBoard(board);
		//ID는 어차피 중복이 안되서 무조건 게시글이 등록이 된다
		//문제 발생 시 게시글 등록이 안되는 경우도 있다
		// I/U/D 테이블의 행의 변환 개수를 반환해 주더라 이걸 이용해서 처리를 해볼 수도 있겠다
		return new ResponseEntity<Board>(board, HttpStatus.CREATED);
	}
	
	//4. 삭제
	@DeleteMapping("/boar/{id}")
	public ResponseEntity<Void> delete(@PathVariable int id){
		boardService.removeBoard(id);
		//반환 값을 통해서 지워졌는지 안 지워졌는지 확인
		//이상한 값(id) 못하게 막던지
		//다른 사람도 요청 주소를 통해 내 글을 지워버릴 수 있다.(권한체크 -> 인터셉터)
		return new ResponseEntity<Void>(HttpStatus.OK);
	}
	
	//5. 수정
	@ApiIgnore
	@PutMapping("/board") //JSON 형태의 데이터로 넘어왔을 떄 처리하고 싶은데?
	public ResponseEntity<Void> update(@RequestBody Board board){
		boardService.modifyBoard(board);
		//위와같은 상황 대비
		
		return new ResponseEntity<Void>(HttpStatus.OK);
	}
}
```

# Swagger를 이용한 REST API 문서화
- FrontEnd 개발자의 경우 화면에 집중하고 BackEnd 개발자가 만든 문서 API를 보며 데이터 처리를 하게 된다.
- 이때 개발 상황의 변화에 따른 API의 추가 또는 변경할 때마다 문서에 적용하는 불편함 발생
- 이 문제를 해결하기 위해 Swagger를 사용한다

# Swagger
- 기존 문서로 사용하던 문제를 해결하기 위해 Swagger를 사용.
- 간단한 설정으로 프로젝트의 API 목록을 웹에서 확인 및 테스트할 수 있게 해주는 Library
- Swagger를 사용하면 Controller에 정의되어 있는 모든 URL을 바로 확인할 수 있다.
- API 목록 뿐 아니라 API의 명세 및 설명도 볼 수 있으며, 또한 API를 직접 테스트해 볼 수도 있다.
- "설정이 반이다"

# Swagger 적용
- pom.xml에 swagger2, swagger-ui dependency 추가. 그리고 servlet-context.xml에 resources 매핑
- 스프링부트에서는 위에 두개 대신 springfox-boot-starter를 추가하면 된다
- http://localhost:8080/context-path/swagger-ui/index.html

# Swagger 설정
```java
//@Configuration 얘도 가능
@EnableSwagger2
public class SwaggerConfig {
	@Bean
	public Docket api() {
		return new Docket(DocumentationType.SWAGGER_2)
				.select()
				.apis(RequestHandlerSelectors.basePackage("com.ssafy.board.controller"))
				.paths(PathSelectors.ant("/*/api/**"))
				.build()
				.apiInfo(apiInfo());
	}
	
	private ApiInfo apiInfo() {
		return new ApiInfoBuilder()
				.title("SSAFY 10기 BOARD REST API")
				.description("엄청나게 대단한 게시판을 위한 레스트풀한 서버 입니다.")
				.version("0.1")
				.build();
	}
}
```

# Swagger 관련 Annotation
![annotation](https://github.com/namoo1818/TIL/assets/50236187/11bbcb31-074c-4ad2-94ca-e73504830452)

# CORS
- 하나의 서버에서만 데이터를 가지고 오면 좋겠지만 여러 사이트에서 다양한 데이터가 필요하단 말이야(CORS ERROR 발생)
- 교차 출처 리소스 공유
- CORS 해결하기
  - 프록시 서버 활용
  - 헤더 추가
  - @CrossOrigin 활용
- @CrossOrigin("*")를 막는 친구는 브라우저.
```java
@RestController
@RequestMapping("/api")
@Api(tags="게시판 컨트롤러")
@CrossOrigin("*")
public class BoardRestController {
...
```
