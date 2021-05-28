# 장민서 [201840130]

## [05월 25일]

# 응답과 요청

### express 모듈 설치

- $ npm install express@4

- express 모듈의 기본 메소드
    - express() : 서버 애플리케이션 객체를 생성
    - app.use() : 요청이 왔을 때 실행할 함수를 지정
    - app.listen() : 서버를 실행

---

### express 모듈로 서버 생성과 실행

```jsx
// 모듈 추출
const express = require('express');

// 서버 생성
const app = express();

//request 이벤트 리스너를 설정
app.use((request, response) => {
		response.send('<h1>Hello express</h1>');
});

// 서버 실행
app.listen(52273, () => {
		console.log('Server running at http://127.0.0.1:52273');
});

```

---

### 페이지 라우팅

- 페이지 라우팅 : 클라이언트 요청에 적절한 페이지를 제공하는 기술
- express 모듈의 페이지 라우팅 메소드
    - get(path, callback) : GET 요청이 발생했을 때 이벤트 리스너를 지정
    - post(path, callback) : POST 요청이 발생했을 때 이벤트 리스너를 지정
    - put(path, callback) : PUT 요청이 발생했을 때 이벤트 리스너를 지정
    - delete(path, callback) : DELETE 요청이 발생했을 때 이벤트 리스너를 지정
    - all(path, callback) : 모든 요청이 발생했을 때 이벤트 리스너를 지정
- 페이지 라우팅을 할 때 토큰을 활용함
    - ':<토큰 이름>' 형태로 설정
    - 토큰은 다른 문자열로 변환 입력가능, request 객체의 params 속성으로 전달됨.

### 페이지 라우팅 예제

```jsx
// 모듈 추출
const express = require('express');

// 서버 생성
const app = express();

//request 이벤트 리스너 설정
app.get('/page/:id', (request, response) => {
		 // 토큰을 꺼냄
		const id = request.params.id;

		// 응답
		response.send(`<h1>'${id} Page</h1>`);
});

// 서버 실행
app.listen(52273, () => {
		console.log('Server running at http://127.0.0.1:52273');
});

```

### response 객체

- response 객체의 기본 메소드
    - send() : 데이터 본문을 제공
        - send() 메소드 : 사용자에게 데이터 본문을 제공
        - send() 메소드는 가장 마지막에 실행해야 하며, 두 번 실행할 수 없음
    - status() : 상태 코드를 제공
    - set() : 헤더를 설정

### response 객체의 기본 메소드 예제

```jsx
// 모듈 추출
const express = require('express');

// 서버 생성
const app = express();

//request 이벤트 리스너 설정
app.get('*', (request, response) => {
		 response.set('methodA','ABCDE');
		 response.set({
				'methodB1': 'FGHIJ',
				'methodB2': 'KLMNO'
});

// 서버 실행
app.listen(52273, () => {
		console.log('Server running at http://127.0.0.1:52273');
});
```

### HTTP 상태 코드 : 404 Not Found

- 많이 보는 오류
    - 4XX : 클라이언트 오류 : 400 Bad Request
    - 5XX : 서버 오류 : 500 Internal Server Error

### 리다이렉트 : 3XX, 특수한 상태 코드

- 웹 브라우저가 리다이렉트를 확인하면 화면을 출력하지 않고, 응답 헤더에 있는 Location 속성을 확인해서 해당 위치로 이동
- 특정 경로로 웹 브라우저를 인도 할 때 사용

# 미들웨어

### morgan 미들웨어

- express 모듈의 미들웨어로 사용할 수 있는 외부 모듈을 확인
- 설치 > npm install morgan

### body-parser 미들웨어

- 요청 본문을 분석함
- 보안에 취약함
- 설치 > npm install body-parser

# RESTful 웹 서비스 개요

- REST 규정에 맞게 만든 ROA(**Resource Oriented Architecture)**를 따르는 웹 서비스 디자인 표준
- 예) 사용자 관련 정보
    - GET /user : 사용자 전체를 조회
    - GET / user/273 : 273번 사용자를 조회
    - POST /user : 사용자를 추가
    - DELETE /user/273 : 273번 사용자를 삭제

## [05월 18일]

문자열 자료형의 전역 변수
-  _ _filename : 현재 실행 중인 코드이 파일 경로를 나타냄
- _ _dirname : 현재 실행 중인 코드의 폴더 경로를 나타냄

※ Node.js는 process 전역 객체를 제공
-
※ process 객체는 프로세스 정보를 제공하며, 제어할 수 있게 하는 객체
-

※ process 객체의 속성
- env : 컴퓨터 환경 정보를 나타냄
- version : Node.js 버전을 나타냄
- versions : Node.js와 종속된 프로그램 버전을 나타냄
- arch : 프로세서의 아키텍처를 나타냄
- platform : 플랫폼을 나타냄

※ process 객체의 메소드
- exit([exicCode = 0]) : 프로그램을 종료
- memoryUsage() : 메모리 사용 정보 객체를 리턴
- uptime() : 현재 프로그램이 실행된 시간을 리턴

※ Node.js가 제공하는 객체의 이벤트 : https://nodejs.org/en/docs/

※ process 객체 : https://nodejs.org/dist/latest-v6.x/docs/api/process.html

※ os 모듈의 메소드
- hostname() : 운영체제의 호스트 이름을 리턴
- type() : 운영체제의 이름을 리턴
- platform() : 운영체제의 플랫폼을 리턴
- arch() : 운영체제의 아키텍처를 리턴
- release() : 운영체제의 버전을 리턴
- uptime() : 운영체제가 실행된 시간을 리턴
- loadavg() : 로드 에버리지 정보를 담은 배열을 리턴
- totalmem() : 시스템의 총 메모리를 리턴
- freemem() : 시스템의 사용 가능한 메모리를 리턴
- cpus() : CPU의 정보를 담은 객체를 리턴
- getNetworkInterfaces() : 네트워크 인터페이스의 정보를 담은 배열을 리턴

※ Url 모듈의 메소드
- parse(urlStr [, ParseQueryString = false, slashesDenoteHost = false]) : URL 문자열을 URL 객체로 변환하여 리턴
- format(urlObj) : URL 객체를 URL 문자열로 변환하여 리턴
- resolve(from,to) : 매게 변수를 조합하여 완전한 URL 문자열을 생성해 리턴

※ File System 모듈
※ 파일읽기
- 실행할 자바스크립트 파일이 있는 폴더에 textfile.txt 이름의 파일을 생성

※ 파일 읽기의 메소드
- fs.readFileSync(<파일 이름>) : 동기적으로 파일을 읽음
- fs.readFile(<파일 이름>,<콜백 함수>) : 비동기적으로 파일을 읽음

※ 비동기 처리의 장점
- 웹 서버를 C++ 프로그래밍 언어로 만들면 무척 빠르지만, 개발과 유지 보수는 어려움
- 전 세계 웹 서비스 기업도 C++로 웹 서버를 개발하지 않고 PHP, 자바, 루비, 파이썬 Node.js 등 프로그래밍 언어로 개발
- 프로그래밍 언어 자체는 느리지만 큰의미가 없다고 판단해 개발 속도와 유지 보수성이 좋은 프로그래밍 언어를 사용
- 자바스크립트 프로그맹 언어는 C++,자바 보다 느리지만 Node.js를 사용하면 손쉽게 비동기 처리를 구현하여 빠른 처리가 가능

※ 파일 쓰기
메소드
- fs.writeFileSync(<파일 이름>,<문자열>) : 동기적으로 파일을 씀
- fs.writeFile(<파일 이름>,<문자열>,<콜백 함수>) : 비동기적으로 파일을 씀

※ 노드 패키지 매니저
- Node.js는 npm패키지 매니저를 사용

※ request 모듈
- 웹 요청을 쉽게 만들어 주는 모듈로 외부 모듈임

설치 방법 : npm install request 를 터미널에 입력


## [05월 11일]
※ Date 객체
- new Date() : 현재 시간으로 Date 객체를 생성
- new Date(<유닉스 타임>) : 유닉스 타임(1970년 1월 1일 00시 00분 00초부터 경과한 밀리초)으로 Date 객체를 생성
- new Date(<시간 문자열>) : 문자열로 Date 객체를 생성
- new Date(<년>, <월 -1>, <일>, <시간>, <분>, <초>, <밀리초>) 시간 요소를 기반으로 Date 객체를 생성
- Month를 나타내는 '월'은 0부터 시작 = 0 -> 1월 11 -> 12월

※ 메소드 활용
- Date 객체
    - getOO() 형태 메소드, setOO() 형태 메소드 : FullYear, Month, Day Hours, Minutes, Seconds 등 사용

시간 더하기
- 현재 시간에 1년, 11개월, 7일을 더해 출력

시간 간격 구하기 에제 풀이
- getTime() 메소드 : 유닉스 타임
- 2개의 시간을 빼고, 일 단위(1000밀리초 * 60초 * 60분 * 24시간)로 나누어 시간 간격을 구함

※ Array 객체

Array 객체의 기본 메소드
- 대부분 파괴적 메소드로 자기 자신을 변경

    - *표시가된 메소드는 자기 자신을 변화시킨다.
    - concat() : 매개 변수로 입력한 배열의 요소를 모두 합쳐 배열을 만들어 리턴
    - join() : 배열 안의 모든 요소를 문자열로 만들어 리턴
    - pop()* : 배열의 마지막 요소를 제거하고 리턴
    - push()* : 배열의 마지막 부분에 새로운 요소를 추가
    - reverse()* : 배열의 요소 순서를 뒤집음
    - slice() : 배열 요소의 지정한 부분을 리턴
    - sort() : 배열의 요소를 정렬
    - splice()* : 배열 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴

배열 선언

    let array [{
        name = '고구마'
        price = 1000
    }, {
        name = '감자'
        price = 1000
    }];
    // 배열 요소를 꺼냄.
    let popped = array.pop();
    console.log(popped); 

    결과

    {
        "name = "감자"
        "price = 1000
    }

    //배열에 요소를 넣음

    array.push(popped);
    array.push({
        name : '바나나'
        price : 1500
    });
    console.log(array);

    결과

    {
        name = "고구마"
        price = 1000
    }, {
        name = "감자"
        price = 1000
    }, {
        "name = "감자"
        "price = 1000
    }

ECMAScript5 에서 추가된 메소드
- forEach() : 배열의 요소를 하나씩 뽑아 반복을 돌림
- map() : 콜백 함수에서 리턴하는 것을 기반으로 새로운 배열을 만듬
- filter() : 콜백 함수에서 true를 리턴하는 것으로만 새로운 배열을 만들어 리턴

※ 프로토타입에 메소드 추가
- 프로토타입에 메소드를 추가하면 해당 자료형 전체에 추가 가능
- String 생성자 함수의  prototype 속성에 contain() 메소드를 추가

※ Json 객체
- 자바스크립트 객체를 사용한 데이터 표현 방법

제약 사항
- 문자열은 큰따옴표로 만듬
- 모든 키는 큰따옴표로 감싸야 함
- 숫자, 문자열, 불 자료형만 사용할 수 있음

Json 객체의 메소드
- JSON.stringify(<객체>, <변환 함수>, <공백 개수>) : 문자열 리턴
- JSON.parse(<문자열>) : 객체 리턴

※ 예외와 기본 예외 처리
- 예외 : 실행에 문제가 발생하면 자동 중단. 이렇게 발생한 오류
- 예외 처리 : 오류에 대처할 수 있게 하는 것

TypeError 기본 예외 처리
- undefined 자료형을 일반적인 객체 또는 함수처럼 다루면 TypeError 예외가 발생
- 사전에 해당 데이터가 undefined인지 조건문으로 확인

고급 예외 처리
- try catch finally 구문    
    - try {<br>
        //예외가 발생하면<br>
    } catch {exception} {<br>
        //여기서 처리합니다.<br>
    } finally {<br>
        //여기는 무조건 실행합니다.<br>
    }
    - catch, fanally 생략 가능
- 배열을 생성할때 길이를 음수로 지정하면 RangeError가 발생

예외 객체
- 예외가 발생하면 어떤 예외가 발생했는지 정보를 전달함
- catch 구문의 괄호 안의 변수
- name 속성과 message 속성이 있음

예외 강제 발생
- throw 키워드 사용
- throw 키워드 뒤에는 문자열 또는 Error 객체를 입력
- 문자열을 사용할 때는 catch 구문의 예외 객체에 간단한 문자열만 전달됨

## [05월 04일]

표준 내장 객체

기본 자료형 숫자, 문자열, 불

    let number = 20;
    let string = '안녕';
    let boolean = true;

객체 자료형 숫자, 문자열, 불

    let number = new Number(20);
    let string = new String('안녕');
    let boolean = new Boolean(true);

기본 자료형과 객체 자료형의 차이
- 기본 자료형의 속성 또는 메소드를 사용할 때 기본 자료형이 자동으로 객체 변환이됨. 즉, 기본 자료형과 객체 자료형 모두 속성과 메소드를 사용함
- 차이점 : 기본 자료형은 객체가 아니므로 속성과 메소드를 추가할 수 없음

<br>
기본 자료형에 프로토타입으로 메소드 추가

// 변수 생성

    let primitiveNumber = 20;
//메소드 생성
    
    Number.prototype.method = function () {
        return 'Primitive Method';
    }    

※ Number 객체
- 자바스크립트에서 숫자를 표현할 때 사용

메소드
- toExponential() - 숫자를 ★지수★ 표시로 나타낸 문자열을 리턴
- toFixed() - 숫자를 고정소수점 표시로 나타낸 문자열을 리턴
- toPrecision() - 숫자를 길이에 따라 지수 표시 또는 고정소수점 표시로 나타낸 문자열을 리턴

toFixed() 메소드를 이용해 소수점 자릿수를 짜르는 방법

    let number = 273.5210332
    console.log(number.toFixed(1));

    결과: 273.1

Number 생성자 함수의 속성
- MAX_VALUE
- MIN_VALUE
- NaN
- POSITIVE_INFINITY
- NEGATIVE_INFINITY

※ String 객체

속성과 메소드
- length - 문자열의 길이를 나타냄
- String 객체의 메소드는 변경된 값을 리턴함

메소드 활용
- indexOf() 메소드 : 특정 문자열이 있는지 확인, 위치를 리턴함. 문자열이 포함되어 있지 않을 때는 -1을 리턴
- split() 메소드를 사용하면 특정한 기호를 기반으로 문자열을 분해함











## [04월 27일]
표준 내장 함수
- clearInterval() 함수

익명 함수와 선언적 함수의 생성 순서
- 변수 덮어쓰기, 함수 덮어쓰기 예제 풀이

익명 함수와 화살표 함수의 차이
- 내부에서 this 키워드가 가지는 의미

※ 객체 기본

- 배열 : 요소에 접근할 때 인덱스를 사용하고, 객체는 키를 사용함
    - 배열 선언 
    
            let array = ['사과', '바나나']

    - 배열 접근  
                
                array[0] -> '문자'
                array[1] -> '바나나'
- 객체 
    - 객체 선언
          
           let product = {
            제품명: '7D 건조 망고',
            유형: '당절임'
            }

            console.log(product);

    - 객체 접근

            product['제품명'] -> '7D 건조 망고'
            product['유형']   -> '당절임' 
for in 반복문을 사용해 객체에 반복문 적용 예제 풀이

※ 속성과 메소드

- 요소 : 배열 내부에 있는 값 하나하나
- 속성 : 객체 내부에 있는 값 하나하나
- 메소드 : 객체의 속성 중 자료형이 함수인 속성

※ 생성자 함수
- 배열과 객체를 사용하면 여러 개의 데이트를 쉽게 다룰 수 있다. 
- 객체를 만드는 함수, 대문자로 시작하는 이름 사용

※ 프로토타입
- 생성자 함수로 만든 객체는 프로토타입 공간에 메소드를 지정해서 모든 객체가 공유 하도록함, 해당 함수를 생성자 함수로 사용했을 때만 의미가 있음

※ 조금 더 나아가기
- '아예 값이 없는 상태'를 구분할 때 null을 활용



## [04월 13일]

함수 생성 방법

익명 함수
- 이름을 붙이지 않고 함수 생성
- 함수를 호출하면 함수 내부의 코드 덩어리가 모두 실행
- let <함수 이름> = function () {};

선언적 함수
- 이름을 붙여 함수를 생성

화살표 함수
- () => {}
- '하나의 표현식을 리턴하는 함수'를 만들 때는 중괄호 생략 가능

함수의 기본 형태
- function <함수 이름>(<매개변수>) {
    <함수 코드>
    return <리턴 값> <- 필수 X
}

함수 매개 변수 초기화
- 실행하면 undefined가 출력됨

콜백 함수
- 함수의 매개 변수로 전달되는 함수

표준 내장 함수
- 자바스크립트에서 기본적으로 지원하는 함수

숫자 변환 함수
- parselnt() = 문자열을 정수로 변환
- parseFloat() = 문자열을 실수로 변환

타이머 함수
- '특정 시간 후에' 또는 '특정 시간마다' 어떤 일을 할 때 사용
- 시간은 밀리초로 지정. 1초를 나타내려면 1000(밀리초)을 입력

타이머 제거 함수
- clearInterval()함수 특정 시간마다 실행하던 함수 호출을 정지


## [04월 06일]
while 반복문

for 반복문 

역 for 반복문

for in 반복문과 for of 반복문

중첩 반복문

break 키워드 <br>
- 반복문을 벗어날 때 사용

continue 키워드 <br>
- 반복문 내부에서 현재 반복을 멈추고 다음 반복을 진행함

스코프Scope <br>
- 변수를 사용할 수 있는 범위
- 스코프 == 블록

호이스팅 Hoisting <br>
- 해당 블록에서 사용할 변수를 미리 확인해서 정리하는 작업

push는 배열의 끝에 원하는 값을 추가해주는 함수

pop는 배열의 마지막 주소에 있는 값을 제거해주는 함수.

shift는 배열의 첫번째 주소에 있는 값을 제거한 후에 반환 해주는 함수.

push와 pop를 이용하면 stack으로 이용할 수 있다.

push와 shift를 이용하면 queue로 이용할 수 있다.

concat은 두개의 배열을 합쳐주는 함수.

reverse은 배열을 역순으로 재배치.

sort는 배열을 정렬

join은 배열값들 사이에 원하는 문자를 삽입하는 함수







## [03월 30일]
if else if조건문

switch 조건문

삼항 연산자

짧은 초기화 조건문

웹 브라우저에서 작동하는 자바스크립트 : prompt()이름의 함수를 받음

Node.js에서 작동하는 자바 스크립트 : 단순한 코드로 입력을 받을 수 없음

배열
- 여러 개의 자료를 한꺼번에 다룰 수 있는 자료형
- 대괄호 내부의 각 자료는 쉼표로 구분
- 배열에는 여러 자료형이 섞여 있을 수 있음
- 요소 : 배열 안에 들어 있는 각 자료

Type script 관련 오류
- Settings(왼쪽 하단 톱니바퀴)에서 'javaScript validate'검색 > disable

while 반복문

for 반복문

역 for 반복문
## [03월 23일]
> 오늘 배운 내용 요약 <br>

문자 선택 연산자

템플릿 문자열

참과 거짓의 표현

비교 연산자

논리 연산자

논리합 연산자

논리곱 연산자

논리 연산자가 많이 사용되는 부분은 '범위 판단'

변수 : 값을 저장할 때 사용하는 식별자, 변수 선언 후 변수에 값을 할당

복합 대입 연산자

자료형 확인 연산자

undefined 자료형

강제 자료형 변환 함수

Number(), String(), Boolean()

Number() 함수와 NaN

NaN의 특징

-NaN은 무조건적으로 다름

-NaN인지 확인할때는 isNaN() 함수를 사용

NaN의 고찰

-표현 불가능한 수치형 결과를 나타내는 값

-자기 자신과 일치하지 않는 유일한 값

자기 자신과도 일치하지 않기 때문에 nan == nan이 false이다.

Boolean() 함수

-Boolean() 함수를 사용하면 5개의 요소는

false로 변환

-0, NaN, "[빈 문자열]", null, undefined

숫자와 문자열 자료형 자동 변환

-숫자와 문자열에 '+' 연산자를 적용하면 자동으로 숫자가 문자열로 변환

불 자료형 자동 변환

일치 연산자
-자료형 까지 검사 

상수
-상수 : '항상 같은 수', 변수와 반대 개념

-const : 상수constant를 만드는 키워드

-변하지 않을 대상에 상수를 적용

조건문
if
if else
중첩 조건문
>요약

