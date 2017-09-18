# Vue.js basic tutorial
[Vue Korea 공식 홈페이지](https://kr.vuejs.org/v2/guide/)

## Setup
```bash
$ npm install -g vue-cli
# vue init [template name] [project name]
$ vue init webpack vue-playground
# cd [project name]
$ cd vue-playground
$ npm install
$ npm start
```
프로젝트 세팅을 하기 위해서 `Vue-cli`를 사용합니다. 빈 프로젝트에서 webpack 설정부터 할 수 있지만 이 포스팅의 목적은 webpack이 아닙니다!

vue-cli가 제공하는  webpack 기반 템플릿은 총 세 가지입니다.
* webpack
* webpack-simple
* pwa

그 외에도 여러 템플릿이 존재합니다.
* 가장 단순한 형태인 `simple` 템플릿
  * CDN으로 vue 라이브러리가 추가되어 있으며 `index.html` 파일 하나만 생성된다.

## Structure
`/build/webpack.base.conf.js`를 보시면 `entry`로 `/src/main.js`가 설정되있는 것을 알 수 있습니다. `vue-cli`가 생성해준 프로젝트 구조를 그대로 가져다가 쓰기 전에 해당 구조를 먼저 파악해봅니다.

`main.js`부터 시작하여 작성된 자바스크립트 코드는 `/index.html`을 기반으로 하여 동작하게 됩니다. `/index.html`을 보시면 다른 것은 아무것도 없고 `id`가 `"app"`인 `div`하나만 존재하는 것을 볼 수 있습니다. `SPA` 형식이 익숙한 사람은 대수롭지 않게 생각할 수 있지만, 하나의 `html`파일에 한 페이지의 마크업 코드가 전부 존재하는 상태에서 주로 작업을 하셨던 분이라면 낯설 수 있습니다.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>vue-playground</title>
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```

`Vue`는 컴포넌트 기반으로 화면을 렌더링 해주는 라이브러리입니다. 때문에 Vue에서는 `html`코드도 컴포넌트 형식으로 템플릿화 하여 작성됩니다.

### main.js
```js
import Vue from 'vue'
import App from './App'
import router from './router'
```
(저는 `vue-router`가 포함된 scaffolding을 진행하였습니다.) 총 세 가지를 import하고 있습니다.

`.vue`라는 확장자로 되어있는 파일은 컴포넌트 단위가 됩니다.






## 디렉티브(Directive)
> 단방향 디렉티브

### v-text
`innerText`라는 HTMLElement 속성과 같다.

### v-html
`innerHTML`라는 HTMLElement 속성과 같다.

### v-bind
HTMLElement 객체의 속성을 바인딩하기 위해 사용된다.
```
<img v-bind:src="imagePath" />
<input v-bind:value="message">
```

> 양방향 디렉티브

### v-model
요소에서 변경한 값이 모델 객체에 반영되기를 원할 경우 사용할 수 있는 디렉티브

### directive for logic
* v-show
* v-if
* v-else
* v-else-if
* v-for
  * array: (Object, idx) in array
  * object: (val, key, idx) in object

### template tag
```
<template></template>
```
template 태그로 감싸서 for문을 돌릴 수 있다.


### 기타 디렉티브
* v-pre
  * {{}}로 표현된 값을 컴파일하지 않고 text 그대로 출력한다.
* v-once
  * 처음 한 번만 렌더링을 수행한다.
  * 초기값이 주어지면 변경되지 않는 UI를 만들 때 사용할 수 있다.
* v-cloak
  * 컴파일되지 않은 템플릿은 나타나지 않도록 할 때 사용한다.
  * v-for 디렉티브를 사용하여 대량의 UI를 렌더링할 때 {{}}와 함께 렌더링되는 경우가 많은데 이를 방지하기 위해서 사용하는 디렉티브이다.
```
<style>
[v-cloak] { display: none; }
</style>
<div v-cloak></div>
```

* 계산형 속성(Computed Property)
```
data: {

},
computed: {
  sum: function() {
    //...
  }
}
```
특정 값을 주입할 때, 함수를 거쳐 적용되야하는 경우, `computed`라는 것을 넘겨주고 해당 객체의 key로 접근하여 사용할 수 있다.


---

## Vue 인스턴스 라이프 사이클
* beforeCreate
* create
* beforeMount
* mounted
* beforeUpdate
* updated
* beforeDestroy
* destroyed
