# Vue.js
: 사용자 인터페이스를 구축하기 위한 JavaScript 표준 프레임워크
<br> 표준 HTML, CSS, JS를 기반으로 구축되며 컴포넌트 기반 프로그래밍 모델 제공

### Introduction

**핵심 기능**

- 선언적 렌더링(Declarative Rendering) : 표준 HTML을 템플릿 문법으로 확장하여 JavaScript 상태(State)를 기반으로 화면에 출력될 HTML을 선언적(declaratively)으로 작성할 수 있음
- 반응성(Reactivity) : JavaScript 상태(State) 변경을 추적하고, 변경이 발생하면 DOM을 효율적으로 업데이트하는 것을 자동으로 수행


**Progressive Framework**

- 빌드 과정 없이 Static HTML에 적용
- 모든 페이지에 웹 컴포넌트로 추가
- SPA (Single Page Application)
- SSR (Server Side Rendering)
- SSG (Static Site Generation)

**SFC**
: Single File Component : 컴포넌트의 논리(JS), 템플릿(HTML) 및 스타일(CSS)을 하나의 파일에 캡슐화
``` html title="Example"
<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
```

### API Style

: 정확히 동일한 기본 시스템에 의해 구동되는 서로 다른 인터페이스이며, 옵션 API는 컴포지션 API 위에 구현된다



**Options API**
: 옵션의 `data`, `methods` 및 `mounted` 같은 객체를 사용하여 컴포넌트의 로직 정의
<br> 옵션으로 정의된 속성은 컴포넌트 인스턴스를 가리키는 함수 내부의 this에 노출됨
``` js
<script>
export default {
  // data()에서 반환된 속성들은 반응적인 상태가 되어 `this`에 노출됩니다.
  data() {
    return {
      count: 0
    }
  },

  // methods는 속성 값을 변경하고 업데이트 할 수 있는 함수.
  // 템플릿 내에서 이벤트 헨들러로 바인딩 될 수 있음.
  methods: {
    increment() {
      this.count++
    }
  },

  // 생명주기 훅(Lifecycle hooks)은 컴포넌트 생명주기의 여러 단계에서 호출됩니다.
  // 이 함수는 컴포넌트가 마운트 된 후 호출됩니다.
  mounted() {
    console.log(`숫자 세기의 초기값은 ${ this.count } 입니다.`)
  }
}
</script>

<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>
```

**Composition API**
: `import`해서 가져온 API 함수들을 사용하여 컴포넌트의 로직 정의
<br> SFC에서 컴포지션 API는 일반적으로 `<script setup>`과 함께 사용된다
``` js
<script setup>
import { ref, onMounted } from 'vue'

// 반응적인 상태의 속성
const count = ref(0)

// 속성 값을 변경하고 업데이트 할 수 있는 함수.
function increment() {
  count.value++
}

// 생명 주기 훅
onMounted(() => {
  console.log(`숫자 세기의 초기값은 ${ count.value } 입니다.`)
})
</script>

<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>
```



---

## Pinia


- `storeToRefs` : 

**Example 1**
=== "vue-1"
    ```html
    <template>
        <h3>현재 값: {{ counter.count }}</h3>
        <h3>{{ counter.name }}</h3>
        <h3>{{ counter.myInfo }}</h3>
        <img :src="counter.logo" />
    </template>

    <script setup>
    import { useCounterStore } from "@/stores/counter";

    const counter = useCounterStore();
    counter.increment();
    counter.increment();
    counter.increment();
    </script>
    ```
=== "vue-2"
    ``` html hl_lines="13"
    <template>
        <h3>현재 값: {{ count }}</h3>
        <h3>{{ name }}</h3>
        <h3>{{ myInfo }}</h3>
    <img :src="logo">        
    </template>

    <script setup>
    import { useCounterStore } from '@/stores/counter'
    import { storeToRefs } from 'pinia'

    const counter = useCounterStore()
    const {count, name, myInfo} = storeToRefs(counter); // 반응형 객체에 사용
    const {logo, increment} = counter;

    increment();
    increment();
    increment();
    </script>
    ```
=== "stores/counter.js"
    ``` js
    import { defineStore } from 'pinia'
    import { ref, computed } from 'vue'

    export const useCounterStore = defineStore('counter', () => {
        const count = ref(0);
        const name = ref('유니코');
        const logo = '/src/assets/pinialogo.png';
        
        const myInfo = computed(() => `이름은 ${name.value} 입니다`);
    
        function increment() {
        count.value++
        }
        return { count, name, logo, myInfo, increment }
    },
    )
    ```

**Example 2 - click**
=== "vue"
    ``` html
    <template>
        <div>
            <input type="text" v-model="text" />
            <button @click="addList(text)">추가</button>
            <h3>[ 추가된 목록 ]</h3>
            <p v-for="(item, index) in getDataAll" :key="index">
            {{ item }}
            </p>
        </div>
    </template>
    <script setup>
        import { ref } from 'vue';
        import { useListStore } from '@/stores/liststore';
        import { storeToRefs } from 'pinia';

        const text = ref("");
        const list = useListStore();
        const { getDataAll } = storeToRefs(list);
            
        function addList() {
            if (!text.value) 
            return;
            list.addList(text.value);
            text.value = "";
        }
    </script>
    ```
=== "liststore.js"
    ``` js
    import { defineStore } from "pinia";
    import { ref, computed } from "vue";

    export const useListStore = defineStore("list", () => {
        const list = ref([]);
        function addList(param) {
            list.value.push(param);
        }
        const getDataAll = computed(() => list.value);
        return { list, addList, getDataAll };
    });
    ```
**Example 3 - watch**

``` html
<template>
    <h2>watch와 watchEffect 테스트</h2>
    <div>
        <h3>{{ num1 }}</h3>
        <button @click="num1++">increase num1</button>
        <h3>{{ num2 }}</h3>
        <button @click="num2++">increase num2</button>
    </div>
</template>

<script setup>
import { ref, watch, watchEffect } from 'vue';
const num1 = ref(10);
const num2 = ref(100);

// watch : num1 값의 변경이 감지되어야 실행이됨.
watch(num1, (after, previous) => {
    console.log(`[W]현재값 : ${after}`);
    console.log(`[W]이전값 : ${previous}`);
});

watchEffect(() => {
    console.log("num1 이나 num2 가 변경됨!!!");
    console.log(`[WE]num1 : ${num1.value}`);
    console.log(`[WE]num2 : ${num2.value}`);
});        
</script>
```




---
!!! quote
    - [Vue.js DOCS-ko](https://ko.vuejs.org/guide/introduction.html#api-styles)
    - 김정현 강사님
