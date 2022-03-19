---
layout: single
title: "[Nomad Coders] 바닐라 JS로 크롬 앱 만들기"
categories: Front-end
tag: [Javascript, VanillaJS]
toc: true
author_profile: false
sidebar:
    nav: "docs" 
---

[바닐라 JS로 크롬 앱 만들기](https://nomadcoders.co/javascript-for-beginners) 강의 메모입니다.

---

```javascript
alert("hi"); //알림창 출력
console.log("hi"); //콘솔 출력
const age = prompt("How old are you?"); //입력받기

const title = document.getElementById("title");
console.dir(title); //요소 모두 출력

//문자열 연결
greeting.innerText = "Hello " + username;
greeting.innerText = `Hello ${username}!`;
```



---

## 자바스크립트 기본 문법

### 데이터 타입

```javascript
//자바스크립트는 카멜방식으로 작성
const vertLongVariableName = "True"; //상수, string
let a = 1; //변수, integer
var b = 2; //변수, 규칙x, 옛날방식
const a = true; //boolean
const a = null;

//배열
const nonsense = [1, 2, "hello", false, null, true, undefined, ''];
console.log(nonsense[3]);

const daysOfWeek = ["mon", "tue", "wed", "thu", "fri", "sat"];
daysOfWeek.push("sun"); //추가 const지만 가능
console.log(daysOfWeek);

typeof(변수명) //변수 타입 확인
변수명 = parseInt(변수명) //변수 타입 변경
```

### 오브젝트

```javascript
const player = {
    name: "Uju",
    points: 10,
    fat: true,
};
player.fat = false; //const지만 가능
player.lastName = "potato"; //const지만 가능
player.points += 15; //const지만 가능
console.log(player);
```

### 함수

```javascript
//함수
function sayHello(nameOfPerson, age){
    console.log("Hello my name is " + nameOfPerson + "and I'm " + age);
}
sayHello("nico", 10);

//오브젝트 안에 함수
const player = {
    name: "nico",
    sayHello: function(){
        console.log("hello!");
    },
};
console.log(player.name);
player.sayHello();
```



---

## HTML과 연동하기

### HTML요소 지정하기

```javascript
const title = document.getElementById("hello") //id가 hello인것 모두
const title = document.getElementByClassName("hello") //class가 hello인것 모두
const title = document.querySelector(".hello h1"); //첫번째 요소만
const title = document.querySelector(".hello:first-child h1");
```



### 이벤트 리스너 설정

```javascript
//html요소 클릭이벤트
const title = document.querySelector(".hello:first-child h1");
function handleTitleClick(event){
		//event.preventDefault();
    console.log("title was clicked!");
}
title.addEventListener("click", handleTitleClick);
title.onclick = handleTitleClick; //위랑 같음
```

```javascript
//윈도우 이벤트
function handleWindowResize() {
    document.body.style.backgroundColor = "tomato";
}
function handleWindowCopy() {
    alert("cooier!");
}
window.addEventListener("resize", handleWindowResize);
window.addEventListener("copy", handleWindowCopy);
```



---

## 클래스 네임 설정

### 클래스 네임으로 CSS 설정하기

```css
body {
    background-color: beige;
}
h1 {
    color: cornflowerblue;
    transition:color .5s ease-in-out;
}
.clicked {
    color: tomato;
}
```

```javascript
const h1 = document.querySelector(".hello:first-child h1");

function handleh1Click(){
    const clickedClass = "clicked";
    if(h1.classList.contains(clickedClass)){
        h1.classList.remove(clickedClass); //클래스 네임 지우기
    } else {
        h1.classList.add(clickedClass); //클래스 네임 추가
    }
}

h1.onclick = handleh1Click;
```

```javascript
//위와 같은 코드
const h1 = document.querySelector(".hello:first-child h1");

function handleh1Click(){
    const clickedClass = "clicked";
    h1.classList.toggle(clickedClass);//있으면 지우고 없으면 추가
}

h1.onclick = handleh1Click;
```



---

## 기타 설정

### 시계

```javascript
const clock = document.querySelector("h2#clock");
function getClock(){
    const date = new Date();
		//시, 분, 초를 받아오고, 글자가 2개가 아니면 앞에 0을 추가
    const hours = String(date.getHours()).padStart(2, '0');
    const minuets = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');
    clock.innerText = `${hours}:${minuets}:${seconds}`;
}
getClock() //시계 초기화
setInterval(getClock, 1000); //1초마다 실행
```



### 이미지 삽입, 랜덤 함수

```javascript
const images = ["0.jpg", "1.jpg", "2.jpg"];
const chosenImage = images[Math.floor(Math.random()*images.length)];

const bgImage = document.createElement("img");
bgImage.src = `img/${chosenImage}`;
console.log(bgImage);

document.body.appendChild(bgImage); //뒤에 삽입
//document.body.prepend(bgImage) //앞에 삽입
```



### 리스트 추가, 삭제

```html
<form id="todo-form">
    <input type="text" placeholder="Write a To Do and Press Enter"/>
</form>
<ul id="todo-list"></ul>
```

```javascript
const toDoForm = document.getElementById("todo-form");
const toDoInput = document.querySelector("#todo-form input")
const toDoList = document.getElementById("todo-list");

function deleteToDo(event){
    const li = event.target.parentElement; //클릭된 요소의 부모 찾기
    li.remove();
}

function paintToDo(newTodo){
    const li = document.createElement("li");
    const span = document.createElement("span");
    span.innerText = newTodo;
    const button = document.createElement("button");
    button.innerText = "X";
    button.addEventListener("click", deleteToDo)
    li.appendChild(span);
    li.appendChild(button);
    toDoList.appendChild(li);
}

function handleToDoSumbit() {
    event.preventDefault();
    const newTodo = toDoInput.value;
    toDoInput.value = "";
    console.log(newTodo, toDoInput.value);
    paintToDo(newTodo)
}

toDoForm.addEventListener("submit", handleToDoSumbit);
```

