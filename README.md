# manual-javascript
for me


즉시함수호출식 IIFE 이피

이름충돌
자바스크립트 파일 두개 페이지 -> 전역 범위 내의 변수들 이름 충돌

객체란?
여러분이 현실 세계에서 인지하는 물체에 대한
모델을 만들기 위해 변수와 함수를 그룹화한 것을 말한다.

var hotel = new Object();
hotel.name = 'quay';
hotel.rooms = 40;
hotel.booked = 25;
hotel.checkAvailability = function() {
          return this.room - this.booked;
};

```javascript
function Hotel ( name, rooms, booked) {
   this.name = name;
   this.rooms = rooms;
 this.booked = booked;
  this.checkAvailability = function () {
       return this.rooms - this.booked;
 };

}
```

전역 컨텍스트 내에 선언된 함수 내에서 this 키워드를 사용하면
이 키워드는 window 객체를 가리키게된다.

브라우저 객체 모델
window : 현재 브라우저 창이나 탭
document : 현재 로드된 웹 페이지
history : 히스토리에 기록한 웹페이지들
location : 현재 페이지의 URL
navigator : 브라우저 관련정보
screen : 장치의 디스플레이 ㅓㅇ보

문서 객체 모델
전역 자바스크립트 객체

length는 코드단위를 셈. 따라서 한글이나 중국어의 경우 글자당 두개의 코드단위를 사용하기도함

var today = new Date();
var est = new Date('Apr 16, 1996 15:45:55');
var difference = today.getTime() - est.getTime();
difference = (difference / 31556900000);

== 같은 값인지
=== 같은 데이터 타입인지

var highScore = 'false' -> true
var highScore = '0' -> true

var highScore = 0 -> false
var highScore = '' -> false

4 뽀모도르

false == 0 -> true
false == '' -> true
0 == '' -> true
undefined == null -> true
null == false -> false
undefined == false -> false
NaN == null -> false
NaN == NaN ->false

문서객체모델 (DOM, Document Object model)
브라우저는 웹 페이지를 로드할 때 해당 페이지에 대한 모델을 생성한다.

이벤트핸들링?
DOM노드에 이벤트를 바인딩.
이벤트 이름앞에 on을 붙임
var el = document.getElementById('username');
el.onblur = checkUsername;

이벤트 리스너
하나의 이벤트로 여러 개의 함수를 실행가능.
제이쿼리로 대체
var el =document.getElementById('username');
el.addEventListener('blur', checkUsername, false);
el.addEventListener('blur', function() {
checkUsername(5);
}, false);

IE5 ~ IE8 지원안됨
if( el.addEventListener) {
  el.addEventListener('blur', function() {
     checkUsername(5)
  }, false);
else {
  el.attachEvent('onblur', function() {
    checkUsername(5)
  });
}

헬퍼 메서드
적절한 이벤트 핸들러를 생성하는 함수

이벤트 버블링 : <a> -><li> ->html> -> DOCUMENT
이벤트 캡처링 :  IE8 이전 버전에서 지원되지않음

바인딩? 이벤트에 대해 어떻게 처리할것인지를 정의하는 과정
이벤트는 브라우저가 어떤 일이 발생했음을 알리는 수단

이벤트 객체는 이벤트의 요소와 정보를 전달

function checkUsername(e) {
   var target = e.target; // 이벤트 요소를 가져옴
}

var el = document.getElementById('username');
el.addEventListener('blur', checkUsername, false);

function checkUsername(e, minLength) {
   var target = e.target;
}

var el = document.getElementById('username');
el.addEventLisetner('blur', function(e) {
     checkUsername(e, 5);
}, false);

이벤트 객체는 자동으로 전달되지만, 익명으로 함수를 호출할경우
매개변수 이름을 명시해줘야함.

function getEventTarget(e) {
      if(!e) { // IE 5 ~ IE 8의 경우
         e = window.target; 
     }
      return e.target || e.srcElement;
}

event.preventDefault(); event.returnValue = false;
// 같은 페이지에 머무름

이벤트는 다음 문서에 ㅓㅇ의
- W3C DOM 명세
- HTML5 명세
- 브라우저 객체모델(BOM : Browser Object Model)

String.fromCharCode(event.keyCode);

click보다 change를 사용해야하는 이유
사용자가 상호작용하는 방법은 탭키, 화살표키, 엔터키
