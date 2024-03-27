# 신희원 202230313
## 4월 17일 강의
```

```
## 4월 10일 강의
```

```
## 4월 3일 강의
```

```
## 3월 27일 강의
#### JSX의 역할
* JSX는 내부적으로 XML/HEML 코드를 자바스크립트로 변환함
* React가 createElement함수를 사용해 자동으로 자바스크립트로 변환해줌
* 만일 JS로 작업할 경우 직접 createElement함수를 사용해야함
* 앞으로 설명하는 코드를 보면 JSX는 가독성을 높여주는 역할이라는 것을 알 수 있음

#### JSX의 장점
* 코드가 간결해짐
* 가독성 향상
* Injection Attack이라 불리는 해킹 방법을 방어함으로써 보안에 강함

#### JSX 사용법
* 기본적으로 모든 자바스크립트 문법 지원
* 자바스크립트 문법에 XML과 HTML을 섞어 사용
* 아래 코드의 2번 라인처럼 섞어서 사용
* 만일 html이나 xml에 자바스크립트 코드를 사용하고 싶으면 중괄호 사용
```
const name='소플';
const element = <h1>안녕, {name}</h1>

ReactDOM.render{
    element,
    document.getElementById('root)
}

```
-------------

#### 1. 엘리먼트 정의
* 엘리먼트는 리액트 앱을 구성하는 요소를 의미
* 공식페이지에는 "엘리먼트는 리액트 앱의 가장 작은 빌딩 블록들"이라고 설명
* 웹사이트의 경우 DOM 엘리먼트이며HTML요소를 의미

#### 리엑트 엘리먼트와 DOM 엘리먼트 차이
* 리앢트는 Virual DOM 형태
* DOM은 페이지의 모든 정보를 갖고 있어 무거움
* 리액트는 변화한 부분만 갖고 있어 가벼움
```
                           DOM                     vitual DOM

업데이트속도               느림                        빠름
element 업테이트 방식     DOM 전체를 업데이트     변화 부분을 가상DOM으로 만든 후 DOM과 비교하여 다룬 부분만 업데이트
메모리                    낭비가 심함                효율적
```

#### 2. 엘리먼트의 생김새
* 리엑트 엘리먼트는 자바스크립트 객체의 형태로 존재
* 컴포넌트(Butto 등), 속성(color 등) 및 내부의 모든 Children을 포함하는 일반 JS 객체
* 이 객체는 마음대로 변경할 수 없는 불변성을 가지고 있음

* 리엑트 엘리먼트의 예를 보면 Type에 태그 대신 리엑트 컴포넌트가 들어가 있는 것 외에는 차이가 없음
```
{
    type: Button,
    props: {
        color: 'green',
        children: 'Hello, element!'
    }
}
```
내부적으로 자바스크립트 객체를 만드는 역할을 하는 함수가 createElement() 입니다.
* 첫 번쨰 매개변수가 type, 이곳에 태그가 들어가면 그대로 표현, 만일 리엑트가 들어가면 이 것을 분해해 결국 태그로 만들게 됨
* 두 번쨰 매개변수 props는 속성
* 세 번쨰 매개변수 children, 자식태그
```
React.createElement{
    type,
    [props],
    [...children]
}
```
-------------
#### createELement 동작 과정
Button, ConfirmDialog 컴포넌트, ConfirmDialog가 Button 포함
```
function Button(props){
    return(
        <button className={`bg-$(props.color)`}>
            <b>
                {props.children}
            </b>
        </button>
    )
}

function ConfirmDialog(props){
    return(
        <div>
            <p>내용을 확인하셨으면 확인 버튼을 눌러주세요.</p>
            <button color='green>확인</Button>
        </div>
    )
}
```

#### 3. 엘리먼트의 특징
리엑트 엘리먼트의 가장 큰 특징은 불변성
즉, 한 번 생성된 엘리먼트의 Children이나 속성(attrivutes)을 바꿀 수 없음

만일 내용이 바뀌면,
* 컴포넌트를 통해 새로운 엘리먼트를 생성하면 됨

#### - 엘리먼트 렌더링
Root DOM node
다음 html 코드는 id 값이 root인 div태그로 단순하지만 리엑트에 필수로 들어가는 아주 중요한 코드
이 div 태그 안에 리엑트 엘리먼트가 렌더링 되며, 이 것을 Root DOM node라고 함

```
<div id="root></div>
```

엘리먼트를 렌더링 하기 위해선 다음과 같은 코드가 필요함
```
const element = <h1>안녕, 리엑트!</h1>
ReactDOM.render(element, document.getElementById('root));
```
이 때 render()함수를 사용하게 됨
첫 번째 파라미터 출력할 리액트 엘리먼트, 두 번쨰 파라미터는 출력할 타겟

#### 렌더링된 엘리먼트 업데이트
* 다음 코드는tick()함수 정의
* 현재시간을 포함한 element를 생성해서 root div에 렌더링
* 1초에 한 번씩 element를 새로 만들고 교체함
```
function tick(){
    const element = (
        <div>
            <h1>안녕, 리액트!</h1>
            <h2>현재 시간: {new Date().toLocaleTimeString()}</h2>
        </div>
    );
    ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```
-----------------
#### 컴포넌트에 대해
* 리엑트는 컴포넌트 기반 구조
* 컴포넌트 구조란 작은 컴포넌트가 모여 큰 컴포넌트를 구성하고, 다시 이런 컴포넌트들이 모여 전체 페이지를 구성한다는 것을 의미
* 컴포넌트 재사용이 가능하기 때문에 전체 코드의 양을 줄일 수 있어 개발 시간과 유지 보수 비용 감소
* 컴포넌트는 자바스크립트 함수와 입력과 출력이 있다는 면에서 유사
* 다만 입력과 출력에서 입력은 Props가 담당, 출력은 리액트 엘리먼트의 형태로 출력
* 엘리먼트를 필요한 만큼 만들어 사용한다는 면에서는 객체 지향의 개념과 유사

#### 1. Props의 개념
* props는 prop(property:속성, 특성)의 준말
* 이 props가 컴포넌트의 속성
* 컴포넌트에 어떤 속성, props를 넣느냐에 따라 속성이 다른 엘리먼트 출력
* props는 컴포넌트에 전달 할 다양한 정보를 담고 있는 자바스크립트 객체
* 에어비엔비 
#### 2. props의 특징
* 읽기 전용, 변경할 수 없다는 의미
* 속성이 다른 엘리먼트를 생성하려면 새로운 props를 커모넌트에 전달하면 됨

Pure 함수 vs, Impure 함수
* Pure함수는 인수로 받은 정보가 함수 내부에서도 변하지 않는 함수
* Impure 함수는 인수로 받은 정보가 함수 내부에서 변하는 함수
```
//pure 함수, input 변경X 같은 input에 대해 하상 같은 output 지원
function sum(a, b){
    return a + b;
}

//impure 함수, input 변경
function withdraw(account, amount){
    account.total -=amount;
}
```



## 3월 20일 강의

#### 리액트 개념
* 복잡한 사이트르르 쉽고 빠르게 만들고, 관리하기 위해 만들어진 것이 바로 리액트
* 다른 표현으로는 SPA를 쉽고빠르게 만들 수 있도 록 해주는 도구

#### 리액트 장점
1. 빠른 업데이트와 랜더링 속도
* 이것을 가능하게 하는 것이 Virtual COM
* DOM(Document Object Model)이란 XML, HTML 문서와 가가 항목을 계층으로 표현하여 생성, 변형, 삭제할 수 있도록 돕는 인터페이스, W3C의 표준
* Virual DOM은 DOM 조작이 비효율적인 이유로 속도가 느리기 때문에 고안된 방법
* DOM은 동기식, Virual DOM은 비동기식 방법으로 랜더링

비동기식-파싱후 DOM를 만듬

2. 컴포넌트 기반 구조
* 리액트의 모든 페이지는 컴포넌트로 구성
* 하나의 컴포넌트는 다른 여러 개의 컴포넌트 조합으로 구성할 수 있음
* 리액트로 개발해보면, 레고 블록을 조립하는 것과 같이 컴포넌트를 조합해 웹사이트를 개발하게 됨

3. 재사용성
* 반복적인 작업을 줄여주기 때문에 생산성을 높여줌
* 유지보수 용이
* 재사용이 가능하려면 해당 모듈의 의존성이 있어야 함

4. 든든한 지원군
 메타(구 페이스북)에서 오픈소스 프로젝트로 관리하고 있어 계속 발전하고 있습니다.

 5. 활발한 지식 공유&커뮤니티

 6. 모바일 앱 개발가능
 리액트 네이티브라는 모바일 환경 UI프레임워크를 사용하면 크로스 플랫폼(cross-platform) 모바일 앱을 개발할 수 있습니다.

 #### 리액트 단점
 1. 방대한 학습량
 2자바스크립트를 공부한 경우 빠르게 학습할 수 있음

 2. 높은 상태 관리 복잡도
 state, component life cycle 등의 개념이 있지만 난이도가 높지 않음

## 3월 13일 강의
```
javascript
```