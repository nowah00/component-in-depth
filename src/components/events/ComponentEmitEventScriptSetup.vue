<script setup>
import { ref, reactive } from 'vue';
import ComponentEmitEventScriptSetupChild from './ComponentEmitEventScriptSetupChild.vue';

defineProps({
  viewTitle: String,
});

// 6-1. 객체 생성
const userInfo = reactive({
  name: '신세계',
  age: 20,
  major: 'Computer Science',
});

const message = ref('');

// 3-1. 메세지 배열 생성
const messages = reactive([]);

const greet = () => {
  message.value = '지금 이 순간도 너의 성공 이야기의 한 페이지야~';
};

const greetArg = (greet) => {
  message.value = greet;
  // 3-2. 메세지를 입력할 때마다 배열에 입력
  messages.push(greet);
};

// 2-4. 이벤트를 통해 이름을 받아 message 객체값에 입력
const welcome = (name) => {
  // alert(`[${name}]님 환영합니다!`);
  message.value = `[${name}]님 환영합니다!`;
};
</script>

<template>
  <div>
    <h1>{{ viewTitle }}</h1>

    <!-- 6-2. 객체 자식 컴포넌트에게 전송 -->
    <ComponentEmitEventScriptSetupChild
      v-on:greeting-event="greet"
      @greeting-arg-event="greetArg"
      @welcome-event="welcome"
      :userInfo="userInfo"
    />

    <h3>{{ message }}</h3>

    <!-- 3-3. 메세지 배열 출력 -->
    <p v-for="msg in messages">{{ msg }}</p>
  </div>
</template>
