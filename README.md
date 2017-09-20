# Vue.js basic
[Vue Korea 공식 홈페이지](https://kr.vuejs.org/v2/guide/)

## Setup
이 포스팅은 node와 npm은 설치되어있다고 가정한 다음 진행됩니다.

```bash
$ npm install -g vue-cli
# vue init [template name] [project name]
$ vue init simple vue-practice
# cd [project name]
$ cd vue-practice
```

프로젝트 세팅을 하기 위해서 `Vue-cli`를 사용합니다. 빈 프로젝트에서 webpack 설정부터 할 수 있지만 이 포스팅의 목적은 webpack이 아닙니다! 커맨드 하나로 쉽게 해결할 수 있습니다.

_cf) [Vue-cli Github repository](https://github.com/vuejs/vue-cli)_

#### vue-cli가 제공하는 템플릿은 총 여섯 가지입니다.
* webpack
* webpack-simple
* browserify
* browserify-simple
* pwa
  * 기본적으로 webpack 기반으로 프로젝트가 scaffolding되며 pwa 기능을 추가하기 위한 dependencies가 추가됩니다.
* simple
  * CDN으로 vue 라이브러리가 추가되어 있으며 `index.html` 파일 하나만 생성됩니다.

vue-cli에 대한 보다 자세한 설명은 다음 포스팅을 참고하시면 좋을 것 같아 공유드립니다.
* [Vue-CLI 로 Vue.js 시작하기 (browserify / webpack) - schemr
](https://medium.com/witinweb/vue-cli-%EB%A1%9C-vue-js-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-browserify-webpack-22582202cd52)

> HTML/CSS/JavaScript의 기본에 대해서 아직 부족하신 분들은 `simple` 템플릿으로 쉽게 익히실 수 있습니다. 이번 포스팅에서는 `simple` 템플릿을 사용하여 간단한 튜토리얼을 진행할 예정입니다.

`simple` 템플릿을 사용하여 scaffolding하게 되면 `index.html` 파일 딱 하나가 생성되는데요, (사실 vue-cli가 필요하진 않았지만, vue를 계속 공부하시려면 필요하실 겁니다!) 이를 바로 띄우기 위해 여러 가지 방법이 있지만 `live-server`이라는 npm을 통해서 바로 running 시킬 수 있습니다.
```bash
$ npm install -g live-server
# .../vue-practice
$ live-server
```
위 커맨드를 입력하면 `Serving "~~" at http://127.0.0.1:8080` 이 나타납니다. 해당 url로 브라우저에서 접속하시면 Vue로 작성된 페이지가 보여집니다. `live-server`는 자동으로 웹페이지가 reload되기 때문에 새로고침 해줄 필요가 없습니다 :)

개발 환경 준비가 모두 끝났습니다 :)

</br>

## index.html
```html
<!DOCTYPE html>
<html>
<head>
  <title>Welcome to Vue</title>
  <script src="https://unpkg.com/vue"></script>
</head>
<body>
  <div id="app">
    <h1>{{ greeting }}</h1>
  </div>

  <script>
    new Vue({
      el: '#app',
      data: {
        greeting: 'Welcome to your Vue.js app!',
      },
    });
  </script>
</body>
</html>
```
일단 위와 같이 가장 간단한 형태로 변경해줍니다. `<script src="https://unpkg.com/vue"></script>`코드가 vue 라이브러리를 CDN으로 불러와서 간단하게 vue를 사용할 수 있습니다.

### el
밑에 `Vue 인스턴스` 부분에서 다른 속성들과 함께 좀 더 자세히 설명하겠지만, `el`은 Vue가 렌더링할 root element의 `CSS Selector`를 작성해줍니다.

### data
이 `data` 객체는 `model`의 역할을 수행하게 됩니다. 생성된 Vue 인스턴스에서 화면을 렌더링할 때 참조하게 되는 데이터 객체인 셈입니다. 이 객체에 명시된 속성으로 데이터를 화면에 렌더링 할 수 있습니다. Vue에서는 데이터를 화면에 렌더링하기 위해 간단하게 `{{}}`처럼 Mustache Expression(콧수염 표현식)을 사용할 수 있고 `디렉티브`를 사용할 수 있습니다. (Mustache Expression은 `handlebars`라는 템플릿 엔진을 사용해보신 분이라면 익숙한 문법일겁니다!)

위 코드(`<h1>{{ greeting }}</h1>`)에서는 Mustache Expression으로 `greeting`이라는 데이터를 렌더링하고 있습니다.

---

</br>

---

## 디렉티브(Directive)
디렉티브를 통해 화면에 렌더링할 데이터를 정의할 수 있습니다. 디렉티브에는 **단방향 디렉티브**, **양방향 디렉티브** 가 존재합니다.

> 단방향 디렉티브 먼저 살펴봅니다.

### v-text
`innerText`라는 HTMLElement 속성과 같습니다.
```js
data: {
  htmlText: "<span>Hello Vue!</span>",
},
```
위와 같은 데이터(data)가 존재한다고 했을 때, 이를 `v-text`디렉티브로 렌더링해보겠습니다.
```html
<h2 v-text="innerText"></h2>
```
화면에는 `<span>Hello Vue!</span>`라고 html 태그가 text로 인식되어 그대로 렌더링됩니다.

### v-html
`innerHTML`라는 HTMLElement 속성과 같습니다. 위에서 사용했던 `htmlText`라는 데이터를 `v-html` 디렉티브를 사용하여 렌더링 해보겠습니다.
```html
<h2 v-html="innerText"></h2>
```
화면에는 `Hello Vue!`라고 `span`태그가 html 태그로 인식돤 후 적용된 상태로 렌더링됩니다.

### v-bind
`v-bind` 디렉티브는 HTMLElement 객체의 **속성** 을 바인딩하기 위해 사용됩니다.
```
<img v-bind:src="imagePath" />
<input v-bind:value="message">
```
`img` 태그의 `src` 속성이나 `input` 태그의 `value`속성을 넘겨줄 때 사용합니다.

> 양방향 디렉티브

### v-model
요소에서 변경한 값이 모델 객체에 반영되기를 원할 경우 사용할 수 있습니다.

### 로직을 위한 디렉티브(directive)
* v-show
  * 주어진 조건에 따라 css 속성 중 `display`를 컨트롤하여 화면에 보일지 말지를 결정합니다.
  * 주어진 조건이 거짓일 경우, `display: none;`을 통해 화면에서 보이지 않게 합니다.
```html
<span v-show="count < 0">Newbie</span>
```

* v-if / v-else-if / v-else
  * 일반 `if-else`와 같은 역할을 합니다.
  * `v-if`와 `v-else-if` 그리고 `v-else`는 같은 계층에 존재해야 합니다.
```html
<div>
  <span v-if="count >= 0 && count <= 3">Bronze</span>
  <span v-else-if="count > 3 && count <= 6">Silver</span>
  <span v-else>Gold</span>
</div>
```

* v-for
  * array: (Object, idx) in array
  * object: (val, key, idx) in object
  * Array와 Object에 대해서 for문을 돌며 렌더링할 수 있고 얻을 수 있는 값들은 위와 같이 얻을 수 있습니다.
```html
<ul v-for="(contact, index) in contacts">
  <li>
    <div>
      <span>ID: </span><span>{{index}}</span>
    </div>
    <div>
      <span>Name: </span><span>{{contact.name}}</span>
    </div>
    <div>
      <span>Age: </span><span>{{contact.age}}</span>
    </div>
    <div>
      <span>Favorite</span><span>{{contact.favorite}}</span>
    </div>
  </li>
</ul>
```
```js
<script>
data: {
  contacts: [{
    name: "jbee",
    age: "25",
    favorite: "VanillaJS"
  }, {
    name: "jbee",
    age: "25",
    favorite: "VanillaJS"
  }, {
    name: "jbee",
    age: "25",
    favorite: "VanillaJS"
  }],
}
</script>
```

### 기타 디렉티브
* v-pre
  * `{{}}`로 표현된 값을 컴파일하지 않고 text 그대로 출력합니다.
  * Mustache Expression을 무시하는 용도로 사용합니다.
* v-once
  * 처음 한 번만 렌더링을 수행합다.
  * 초기값이 주어지면 변경되지 않는 UI를 만들 때 사용할 수 있습니다.
* v-cloak
  * 컴파일되지 않은 템플릿은 나타나지 않도록 할 때 사용합니다.
  * v-for 디렉티브를 사용하여 대량의 UI를 렌더링할 때 `{{}}`와 함께 렌더링되는 경우가 많은데 이를 방지하기 위해서 사용합니다.
```
<style>
[v-cloak] { display: none; }
</style>
<div v-cloak></div>
```

</br>

---

</br>


## Vue 인스턴스
```js
new Vue({
  el: ...,
  data: {
    //...
  },
  computed: {
    //...
  },
  watch: {
    //...
  },
  methods: {
    //...
  },
});

```
### el
`el`은 Vue가 렌더링할 root element의 selector를 작성해줍니다. 보통 `id`로 작성하고 `class`로 작성하게 될 경우, class에 해당하는 element중 가장 최상단에 존재하는 element가 root element가 됩니다.

### data
이 `data` 객체는 `model`의 역할을 수행하게 됩니다. 생성된 Vue 인스턴스에서 화면을 렌더링할 때 참조하게되는 데이터 객체인 셈입니다. 이 객체에 명시된 속성으로 데이터를 화면에 렌더링 할 수 있습니다. Vue에서는 데이터를 화면에 렌더링하기 위해 간단하게 `{{}}`처럼 Mustache Expression(콧수염 표현식)을 사용할 수 있고 `디렉티브`를 사용할 수 있습니다. (Mustache Expression은 handlebars라는 템플릿 엔진을 사용해보신 분이라면 익숙한 문법일겁니다!)

### computed
계산형 속성(Computed Property)
```
data: {

},
computed: {
  sum: function() {
    //...
  }
}
```
특정 값을 주입할 때, 함수를 거쳐 적용되야하는 경우, `computed`라는 것을 넘겨주고 해당 객체의 key로 접근하여 사용할 수 있습니다. 동기적인 계산을 처리할 때 사용합니다. 결과값만을 필요로 할 경우, 함수를 호출하는 형식이 아닌 변수처럼 단순히 `{{}}` 만으로 렌더링할 수 있습니다.

### watch
`computed` 속성과 거의 비슷합니다. 하지만 주로 `watch`에서는 비동기적으로 처리해야할 작업들을 명시합니다.
```html
<div>
  <div>
  x: <input type="text" v-model="x" />
  </div>
  <div>
  y: <input type="text" v-model="y" />
  </div>
  <div>
    sum: <span>{{sum}}</span>
  </div>
</div>
```
```js
data: {
  x: 0,
  y: 0,
  sum: 0,
},
watch: {
  x: function(val) {
    const result = Number(val) + Number(this.y);
    if (isNaN(result)) this.sum = 0;
    else this.sum = result;
  },
  y: function(val) {
    const result = Number(val) + Number(this.x);
    if (isNaN(result)) this.sum = 0;
    else this.sum = result;
  }
}
```
`computed`와 마찬가지로 결과값만을 필요로 할 경우, 함수를 호출하는 형식이 아닌 변수처럼 단순히 `{{}}` 만으로 렌더링할 수 있습니다.

---

## Vue 인스턴스 라이프 사이클
1. beforeCreate
2. create
3. beforeMount
4. mounted
5. beforeUpdate
6. updated
7. beforeDestroy
8. destroyed

[Vue.js 라이프사이클 이해하기 - Jeong Woo Ahn](https://medium.com/witinweb/vue-js-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-7780cdd97dd4)

</br>

---

</br>

## 이벤트 처리
### v-on 디렉티브를 이용한 인라인처리
```html
<div>
  <span>clicked:</span><input type="text" v-model="clicked" />
  <button v-on:click="++clicked">Up</button>
  <button v-on:click="--clicked">Down</button>
</div>
```
vue 인스턴스에 연결된 data model 속성으로 `clicked`라는 속성이 존재하는 경우, 이 코드는 `Up` 버튼을 클릭했을 때, 숫자가 올라가게 되고, `Down` 버튼을 클릭했을 때, 숫자가 내려가게 됩니다.

### 이벤트 핸들러 메소드
```html
<div>
  <span>Only number clicked:</span><input type="text" v-model="clickedCount" />
  <button @click="plus">PLUS</button>
  <button @click="minus">MINUS</button>
</div>
```
```js
data: {
  //...
  methods: {
    plus: function() {
      if (this.clickedCount >= 10) {
        alert('더이상 늘릴 수 없습니다.');
        return;
      }
      this.clickedCount += 1;
    },
    minus: function() {
      if (this.clickedCount <= 0) {
        alert('더이상 뺄 수 없습니다.');
        return;
      }
      this.clickedCount -= 1;
    },
  },
}
```
추가적인 팁으로 클릭 이벤트에 대해서는 `@click`으로 줄여 사용할 수 있습니다.

### 이벤트 수식어(Event Modifier)
* .prevent
기존에는 html 태그에서 기본적으로 제공하는 이벤트의 실행을 막기 위해 `e.preventDefault()`를 코드상에 추가했었습니다. 하지만 vue에서 제공하는 이벤트 수식어를 통해 이를 간단하게 해결할 수 있습니다.
```html
<div>
  <div><a href="www.facebook.com">페이스북으로 이동하기 링크</a></div>
  <div><a href="www.facebook.com" v-on:click.prevent>페이스북으로 이동할 수 없는 링크</a></div>
  <!-- or @click.prevent-->
</div>
```
이외에도 여러 가지 수식어가 존재합니다.
* `.stop`  
이벤트 전파를 중단시킨다.

* `.capture`  
캡쳐링 단계에서만 이벤트 발생시킨다.

* `.self`
버블링 단계에서만 이벤트 발생시킨다.

* `.once`  
이벤트를 한 번만 발생시킨다.

* [keyc event].[keycode]  
`keycode`에 해당하는 key event가 발생했을 때만 event를 발생시킨다.
```html
<input type="text" v-model="number" v-on:keyup.13="search" />
```
위 코드는 enter key(key code: 13)가 눌렸을 경우에 대해서만 `search` 메소드를 실행합니다. 본래는 `e.keycode === 13`과 같은 분기 작업을 수행해줬어야만 했는데, 이벤트 수식어로 코드가 간결해졌습니다. 하지만 Vue는 여기서 끝내지 않습니다! `13`이 enter key라는 것과 다른 key에 대한 keycode값을 기억할 수 없습니다. 따라서 Vue에서는 주로 사용되는 key에 대한 이벤트 수식어를 별도로 제공합니다! (`.enter`, `.tab`, `.delete`, `.esc`)

* [mouse event].[.left || .right || .middle]
마우스에 대해서도 이벤트 수식어를 제공합니다.

</br>

---

</br>

## 스타일
### 인라인 스타일
`v-bind:style`을 통해 인라인으로 style을 적용할 수 있습니다. (권장되는 방식은 아닙니다.) 이 때 style 객체를 작성할 때는 케밥 표기법(- 표기법)이 아닌 카멜 표기법으로 작성해야 합니다. 만약 여러 style 객체를 적용할 경우에는 `v-bind:style` 값으로 배열을 넘겨줍니다.
```html
<button v-bind:style="[buttonLayout, buttonColor]"></button>
```

### CSS 클래스 바인딩
`v-bind:class`를 사용합니다. 이 때 class가 특이하게 먹힙니다.
```html
<button v-bind:class="{style1: s1, style2: s2, style3: s3}">버튼1</button>
```
`style1`, `style2`, `style3` 각각의 클래스에 대해서 `s1`, `s2`, `s3`의 값이 매핑되어 있는 것을 확인하실 수 있습니다. 이 값들은 `data: { ... }`에 존재하는 값으로 boolean 타입의 값입니다. 그래서 매핑되어 있는 값이 true 일 경우에만 class가 적용됩니다. style각각에 해당하는 값을 data에 추가할 수 없으니 스타일 객체를 만들 수도 있습니다.

```html
<button v-bind:class="btnStyle">버튼</button>
<div>
  <input type="checkbox" v-model="btnStyle.option1" value="true" />option1 </br>
  <input type="checkbox" v-model="btnStyle.option2" value="true" />option2 </br>
  <input type="checkbox" v-model="btnStyle.option3" value="true" />option3 </br>
</div>

<script>
data: {
  //...
  btnStyle: {
    option1: false,
    option2: false,
    option3: false,
  }
}  
</script>
<style>
  .option1 {color: red;}
  .option2 {color: blue;}
  .option3 {color: green;}
</style>
```

</br>

---

</br>

## 컴포넌트
Vue.js는 여러 컴포넌트들을 조합해 전체 애플리케이션을 작성합니다. 컴포넌트들은 각각 부모-자식 관계의 트리 구조로 형성됩니다. 자식 컴포넌트는 부모 컴포넌트로부터 `Props`라는 속성을 통해 정보를 전달받을 수 있습니다. 이 전달 방향은 부모에서 자식으로만 향하게 됩니다.

Vue 인스턴스에서 사용했던 옵션들(data, methods, computed, watch)은 컴포넌트 수준에서도 사용할 수 있습니다. 단 `data` 옵션은 각 컴포넌트가 관리해야하는 상태에 대해서만 사용하게 됩니다. 컴포넌트를 재사용하는 경우, 각기 다른 곳에서 사용되는 컴포넌트가 하나의 data 객체를 참조하는 것을 막고자 data를 함수로 작성(객체를 반환하는)합니다.

컴포넌트는 다음과 같이 작성합니다.
```
Vue.component(tagname, options)
```
* tagname: 컴포넌트를 렌더링할 때 사용하는 태그명입니다.
  * 태그명은 대소문자를 구분하지 않습니다. 그렇기 때문에 케밥 표기법(`-`사용)을 사용하여 작성합니다.
* options: 컴포넌트에서 렌더링한 template 등을 지정하게 됩니다.

### my-first-component
우선, 인라인 템플릿(inline-template)으로 컴포넌트를 작성해보겠습니다.
```js
Vue.component("my-first-component", {
  template: "<div>Hello Vue!</div>",
});
```
그런 다음 `my-first-component` 컴포넌트를 렌더링하겠습니다.
```html
<div id="app">
  <my-first-component></my-first-component>
</div>
```
화면에 `Hello Vue!`가 찍힌 것을 확인하실 수 있습니다 :)

### <template></template>
인라인 템플릿으로 HTML코드를 작성하는 것은 권장되지 않습니다. 별도의 template 태그를 통해서 따로 작성해줍니다.
```js
Vue.component("nav-about", {
  template: "#nav_about",
});
```
```html
<template id="nav_about">
   <div>About</div>
 </template>
```
이렇게 작성할 수 있습니다. `template`에 `id`를 부여하여 컴포넌트에서 접근할 수 있도록 합니다. 여기서 주의할 점은 `template`태그 안에는 하나의 루트 엘리먼트가 존재해야 합니다. 같은 계층의 엘리먼트가 존재할 경우 에러가 발생합니다. 부득이하게 같은 계층의 엘리먼트를 렌더링해야 하는 경우에는 `div`태그로 감싸줘야 합니다.

### `data` of Vue.component
바로 위에서도 언급했듯이, 컴포넌트 내부에서 local data를 관리하기 위한 data 옵션은 함수로 작성되어야 합니다. 일반 객체로 작성할 경우 다음과 같은 warning이 발생합니다.
```
[Vue warn]: The "data" option should be a function that returns a per-instance value in component definitions.
```
data로 사용하고자하는 객체를 반환하는 함수로 작성해줍니다.
```js
Vue.component("data-component", {
  template: "#data_component",
  data: function() {
    return { name: "jbee" };
  },
  // data: { name: "jbee" } => warning!!
});
```
함수가 호출될 때마다 만들어진 객체가 리턴되기 때문에 컴포넌트를 재사용하더라도 같은 data 객체를 참조할 일이 없습니다.

### Props

### Event Bus

### .vue의 정체

</br>

</br>

---

>>연재형 포스팅>>

---

# Vue.js TODO Application project## Structure

[Vue Korea 공식 홈페이지](https://kr.vuejs.org/v2/guide/)
이 포스팅은 Vue.js 라이브러리로 간단한 TODO 애플리케이션을 만들어보는 연재형 포스팅입니다 :)

## Setup
이 포스팅은 node와 npm은 설치되어있다고 가정한 다음 진행됩니다.

```bash
$ npm install -g vue-cli
# vue init [template name] [project name]
$ vue init webpack vue-todo-project
# cd [project name]
$ cd vue-todo-project
$ npm install
$ npm start
```
`vue-cli`를 사용하여 webpack 기반의 프로젝트를 scaffolding 합니다. `/build/webpack.base.conf.js`를 보시면 `entry`로 `/src/main.js`가 설정되있는 것을 알 수 있습니다. `vue-cli`가 생성해준 프로젝트 구조를 그대로 가져다가 쓰기 전에 해당 구조를 먼저 파악해봅니다.

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

</br>

---


### main.js
```js
import Vue from 'vue'
import App from './App'
import router from './router'
```
(저는 `vue-router`가 포함된 scaffolding을 진행하였습니다.) 총 세 가지를 import하고 있습니다.

`.vue`라는 확장자로 되어있는 파일은 컴포넌트 단위가 됩니다.


### template tag
```
<template></template>
```
template 태그로 감싸서 for문을 돌릴 수 있습니다.
