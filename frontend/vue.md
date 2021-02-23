### Vue 인스턴스

뷰 인스턴스는 뷰로 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위입니다.

``new Vue()``와 같이 생성자 함수를 통해 인스턴스를 생성합니다. 생성자를 사용하는 이유는 뷰로 개발할 때 필요한 기능들을 생성자에 미리 정의해놓고 이를 재정의, 확장하여 사용하기 위함입니다.



#### 뷰 인스턴스 옵션 속성 

* el : 화면이 그려질 위치의 돔 요소
* data : 화면에 사용될 데이터들
* template : 화면에 표시할 마크업 요소들
* methods : 화면 로직 제어와 관련된 메소드들 ex) 클릭이벤트
* created : 생성되자마자 실행할 로직 . react의 useEffect와 유사
* watch : data에서 정의한 속성이 변화할때 추가동작을 정의할 수 있는 속성


#### 인스턴스가 적용되는 과정

1. 인스턴스 객체 생성 

2. 특정 화면 요소(el에서 지정한 DOM 요소)에 인스턴스를 붙임

   이 때 인스턴스의 유효범위는 DOM 요소 안으로 한정됨. 

3. 인스턴스의 내용이 화면 요소로 변환 (data, methods 등)



#### 라이프사이클

![콘솔에서 확인한 인스턴스 내용](https://joshua1988.github.io/vue-camp/assets/img/lifecycle.dcbe29f6.png)

크게 나누면 **생성**, **부착**, **갱신**, **소멸**의 4단계로 이루어집니다.

* beforeCreate : 인스턴스 생성 직후에 실행. data와 methods 속성이 아직 정의되지 않음.
* created : data와 methods등이 정의된 단계. 아직 화면에 부착되기 전.
* beforeMount : template 속성에 지정한 마크업 속성을 render() 함수로 변환한 후 DOM에 부착하기 직전.
* mounted : 화면에 부착된 이후. 하위 컴포넌트나 외부 라이브러리에 의해 화면 요소들이 최종 HTML코드로 변환되는 시점과는 다를 수 있다.
* beforeUpdate : 관찰하고 있는 데이터가 변경되면 가상 돔으로 화면을 그리기 전에 호출되는 단계. 데이터 값을 갱신하는 로직을 추가하면 좋다.
* updated : 데이터가 변겨오디고 가상돔으로 화면을 다시 그리고 난 뒤. 변경데이터의 화면과 관련된 로직을 추가하면 좋다.
* beforeDestroy : 인스턴스가 파괴되기 직전
* destroyed : 인스턴스가 파괴된 뒤.

### Reference
* https://joshua1988.github.io/vue-camp/



### 이벤트 수식어

- `.stop` : stopPropatation. 버블링을 막는다.
- `.prevent` : default event를 막는다 (form, a tag)
- `.capture` : 이벤트 캡처링을 사용한다. 
- `.self : ` 엘리먼트 자체인 경우에만 이벤트를 트리거.
- `.once` : 한 번만 트리거
- `.passive` : 메인스레드를 기다리지 않고 컴포지트 스레드에서 바로 composite를 수행 ( layout, paint를 안거치고 composite)



### slot

컴포넌트 안의 하위 컴포넌트 마크업을 확장하여 컴포넌트를 재사용할 수 있는 기능.

컴포넌트 안에 슬롯으로 선언된 부분을 바꿔가면서 컴포넌트의 재사용성을 높일 수 있다.



#### Named Slot

이름이 있는 슬롯으로 여러개의 슬롯을 사용할때 유용합니다.

```jsx
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
// base-layout.vue

```

```
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```



#### Scoped Slot

슬롯에 필요한 데이터를 가져올때 사용합니다.

```jsx
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>

```

```vue
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

