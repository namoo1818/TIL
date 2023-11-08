# 동기와 비동기
- 동기 : 요청과 결과가 동시에 일어나는 방식으로 요청을 보낸 후 응답을 받아야 다음 동작이 진행된다.
- 비동기 : 요청과 결과가 동시에 일어나지 않는 방식으로 요청과 결과가 동시에 일어나지 않는다.

# AJAX (Asynchronous JavaScript and XML)
- 비동기식 JS와 XML
- 서버와 통신하기 위해 XMLHttpeRequest 객체 사용
- 페이지 전체를 새로고침하지 않고서도 수행되는 "비동기성" (일 부분만 업데이트 가능)

# XMLHttpRequest 객체
- JavaScript Object
- 서버와 상호작용하기 위해 사용
- URL로부터 데이터(key-value)를 받아올 수 있다

# AJAX 프로그래밍 순서
1. 클라이언트 이벤트 발생
2. XMLHttpRequest 객체 생성
3. XMLHttpRequest 객체 콜백함수(OnReadyStateChange) 설정
   - 상태(0,1,2,3,4)가 바뀔 때마다 함수 실행
4. XMLHttpRequest 객체를 통한 비동기화 요창
5. 서버 응답결과를 생성하여 클라이언트로 전송
6. XMLHttpRequest 객체는 서버 결과를 처리할 콜백함수 호출
7. 결과를 클라이언트 화면에 반영

# 순차적인 비동기 처리
- Web API로 들어오는 순서는 중요하지 않고, 어떤 이벤트가 먼저 처리되느냐가 중요(실행 순서 불명확)
- Async Callbacks
- Promise-Style
```html
  const URL = "https://dog.ceo/api/breeds/image/random";

  function getDog1(){
    const xhr = new XMLHttpRequest();

    xhr.onreadystatechange = function(){
      // 완벽하게 통신이 끝났다면
      if(xhr.readyState == xhr.DONE){
        if(xhr.status==200){
          // console.log(JSON.parse(xhr.response).message)
          // console.log(JSON.parse(xhr.response)['message'])

          const imgSrc = JSON.parse(xhr.response)['message']

          const imgTag = document.querySelector("#dog-img")
          // img 기본속성이라서 imgTag.src로 불러오기 가능
          imgTag.src = imgSrc 

          // 존재하지 않는 속성을 넣고싶다면
          // imgTag.setAttribute("src",imgSrc)
        }
      }
    }

    xhr.open("GET",URL)
    xhr.send();
  } 
```
# fetch API
```html
const URL = "https://dog.ceo/api/breeds/image/random";

function getDog2(){
  fetch(URL)
    .then((response)=>{
      // console.log(response)
      return response.json()
    })
    .then((imgData)=>{
      const imgSrc = imgData.message
      document.querySelector("#dog-img").setAttribute("src", imgSrc)
    })
}

const btn2 = document.querySelector('#btn2');
btn2.addEventListener('click',getDog2);
```

# axios
- 브라우저와 node.js에서 사용할 수 있는 Promise 기반 HTTP 클라이언트 라이브러리
- Vue에서 권고하는 HTTP 통신 라이브러리
- https://github.com/axios/axios
- https://axios-http.com/kr/docs/intro
```html
const URL = "https://dog.ceo/api/breeds/image/random";

function getDog3(){
  axios.get(URL)
  .then((response)=>{
    const imgSrc = response.data.message
    document.querySelector("#dog-img").setAttribute("src", imgSrc)
  })
}

const btn3 = document.querySelector('#btn3');
btn3.addEventListener('click',getDog3);
```

# 고양이 API
- fetch 방식 
```html
const catImageSrc = ref('')

const getCat = function(){
  fetch(URL)
  .then((response)=> response.json())
  .then((imgData)=>{
    catImageSrc.value = imgData[0].url
  })
  .catch((error)=>{
    console.log(" 실패했다")
  })
}

return { catImageSrc, getCat }
```
-axios 방식
```html
const catImageSrc = ref('')

const getCat2 = function(){
  axios({
    url:URL,
    method: 'GET'
  })
  .then((response)=>{
    catImageSrc.value = response.data[0].url
  })
  .catch((error)=>{
    console.log(" 실패했다")
  })
}

return { catImageSrc, getCat2 }
```
- Vue lifecycle
- onMounted(): 기본적으로 고양이 사진을 하나 시작할 때 불러와줘~
```html
onMounted(()=>{
  getCat2()
})
````

# YouTube API를 활용한 실습
1. 구글 로그인
2. google console developer 검색 > Google 클라우드 플랫폼
3. YouTube Data API v3 검색 > 사용
4. 사용자 인증 정보 > 사용자 인증 정보 만들기
5. API 키 생성 완료
