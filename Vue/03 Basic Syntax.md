# computed()
> 계산된 속성을 정의하는 함수. 불필요한 반복 연산을 줄임.
- 반응성 데이터를 포함하는 복잡한 로직의 경우 computed를 활용하여 미리 값을 계산할 수 있다

# computed 특징
- 반환되는 값은 computed ref이며 일반 refs와 유사하게


# 실습
- todos, restOfTodos, getRestOfTodos 다 같은 기능을 한다
- computed는 한 번만 출력, 메서드는 호출한 횟수만큼 호출
- computed는 계산이 끝났으면 그 값을 저장했다가 의존된 반응형 데이터가 변경이 되지 않는 한 이전 결과를 반환(캐시)
- 메서드는 렌더링이 발생할 때마다 항상 함수를 실행
```html
        <div id="app">
            <h2>남은 할 일</h2>
            <p>{{todos.length > 0 ? '아직 남았다' : '퇴근'}}</p>
            <h2>계산된 속성</h2>
            <p>{{restOfTodos}}</p>
            <p>{{restOfTodos}}</p>
            <h2>메서드 호출</h2>
            <p>{{getRestOfTodos()}}</p>
            <p>{{getRestOfTodos()}}</p>
        </div>
        <script>
            const { createApp, ref, computed } = Vue; //구조분해할당

            const app = createApp({
                setup() {
                    const todos = ref([
                        { text: "Vue 공부하기" },
                        { text: "Vue 실습하기" },
                        { text: "Spring 복습하기" },
                        { text: "춤추기" },
                    ]);

                    const restOfTodos = computed(() => {
                        console.log(computed);
                        return todos.value.length > 0
                            ? "아직 퇴근 못해"
                            : "퇴근";
                    });

                    const getRestOfTodos = function () {
                        return todos.value.length > 0
                            ? "아직 퇴근 못해2"
                            : "퇴근2";
                    };

                    return {
                        todos,
                        restOfTodos,
                        getRestOfTodos,
                    };
                },
            });
            app.mount("#app");
        </script>
```
![computed](https://github.com/namoo1818/TIL/assets/50236187/093723f1-ddf3-4c58-b5ca-895b6fca4a98)

# Cache(캐시)
- 데이터나 결과를 일시적으로 저장해두는 임시 저장소
- 이후에 같은 데이터나 결과를 다시 계산하지 않고 빠르게 접근할 수 있도록 함

# computed vs method
## computed
- 의존하는 데이터에 따라 결과가 바뀌는 계산된 속성을 만들 때 유용
- 동일한 의존성을 가진 여러 곳에서 사용할 때 결과를 캐싱하여 중복 계산 방지
- 남은 할 일, 전시회 단체 결제
## method
- 단순히 특정 동작을 수행하는 함수를 정의할 때 사용
- 데이터에 의존하는지 여부와 관계없이 항상 동일한 결과를 반환하는 함수

# v-if
> 표현식 값의 T/F를 기반으로 요소를 조건부로 렌더링
- 'v-else' directive를 사용하여 v-if에 대한 else 블록을 나타낼 수 있다


# 여러 요소에 대한 v-if 적용
- v-if는 directive이기 때문에 단일 요소에만 연결 가능

# v-show
- 항상 렌더링되어 DOM에 남아있다
- CSS display 속성만 전환되기 때문에

# v-if vs v-show
## v-if
- 초기 조건이 false인 경우 아무 작업도 수행하지 않음
- 토글 비용이 높음
## v-show
- 초기 조건에 관계없이 항상 렌더링
- 초기 렌더링 비용이 더 높음
### 무엇가를 자주 전환하는 경우에는 v-show를,
### 실행 중에 조건이 변경되지 않는 경우에는 v-if 권장

# v-for 구조
> 소스 데이터를 기반으로 요소 또는 템플릿 블록을 여러 번 렌더링
- v-for는 alias in expression 형식의 특수 구문을 사용하여 반복되는 현재 요소에 대한 별칭

# 중첩된 v-for
- 각 v-for 범위는 상위 범위에 접근할 수 있다

# v-for with key
> 반드시 v-for와 key(식별키)를 함께 사용한다
- key는 반드시 각 요소에 대한 고유한 값을 나타낼 수 있는 식별자
- index는 값이 변할 수 있기 때문에 key로 사용하지 않는다

# v-for with v-if
> 동일 요소에 v-for와 v-if를 함께 사용하지 않는다
- v-if가 우선순위가 더 높아서 문법적 오류
## 해결법 1
- computed를 활용해 필터링된 목록을 반환하여 반복하도록 설정
## 해결법 2
- v-if가 더 높은 우선순위를 가지므로 v-for의 todo 요소를 v-if에서 사용할 수 없다


# computed와 watchers
- 
- 의존이고 자식 특정 데이터가 바뀌면 이것 좀 해야겠는데? -> watch
- 데이터 변경에 따른 특정 작업을 하고 싶을 때 사용
- 비동기 API 요청

- 둘 다 원본 데이터를 변경하지 마


# Lifecycle Hooks    
https://vuejs.org/guide/essentials/lifecycle.html
- onMounted, onUpdated 정도만 알아도 된다

https://ko.vuejs.org/api/composition-api-lifecycle.html   
- Vue는 Lifecycle Hooks에 등록된 콜백 함수들은 인스턴스와 자동으로 연결

# Vue Style Guide   
https://ko.vuejs.org/style-guide/
## 우선순위별 특징
### A:필수(Essential)
- 오류를 방지하는데 도움이 되므로 어떤 경우에도 규칙을 학습하고 준수
### B:적극 권장(Strongly Recommended)
- 가독성 및 개발자 경험을 향상시킴
- 규칙을 어겨도 코드는 여전히 실행되겠지만, 정당한 사유가 있어야 규칙을 위반할 수 있음
### C:권장(Recommended)
- 일관성을 보장하도록 임의의 선택할 수 있음
### D:주의 필요(Use with Caution)
- 잠재적 위험 특성을 고려함
