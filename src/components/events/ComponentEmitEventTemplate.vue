<script setup>
import { ref } from 'vue';
import ComponentEmitEventTemplateChild from './ComponentEmitEventTemplateChild.vue';

defineProps({
  viewTitle: String,
});

const message = ref('');

// 4-1. 데이터를 담을 객체 생성
const isActive = ref(false);

// 4-3. 메서드 값을 적용
const changeActive = () => {
  isActive.value = !isActive.value;
};

const greet = () => {
  message.value = '지금 이 순간도 너의 성공 이야기의 한 페이지야~';
};

const greetArg = (greet) => {
  message.value = greet;
};

const toggleEvent = () => {
  message.value = '활성화 상태입니다.';
};
</script>

<template>
  <div>
    <h1>{{ viewTitle }}</h1>

    <!-- 
    1. 궁금증 - 자식 컴포넌트에서는 카멜케이스로 호출했는데 부모 컴포넌트의 이벤트는 케밥 표기임에도 불구하고 가능한 이유!
      이벤트명이 자식 컴포넌트에서 보냈을때 'greetingEvent'로 보냈는데, 부모 컴포넌트에서 greeting-event로 받을 수 있는 이유는
      vue 컴파일러가 카멜케이스에서 케밥으로 알아서 변환해주기 떄문에 따로 명시하지 않더라도 이벤트를 불러낼 수 있음 

    2. 궁금증 - v-on과 @의 차이
      v-on: vue 초창기부터 있던 문법이자 원래 정식 문법
      @: v-on을 축약하여 쓴 버전
      결과 = v-on과 @는 동일함!
    -->

    <!-- 1-1. 색값 자식 컴포넌트에게 보냄 -->
    <!-- 4-4. 자식 컴포넌트에게 isActive 데이터 전송 -->
    <ComponentEmitEventTemplateChild
      v-on:greeting-event="greet"
      @greeting-arg-event="greetArg"
      color="pink"
      :isActive="isActive"
      @toggle-event="toggleEvent"
    />

    <!-- 4-2. 버튼을 통해 메서드 실행 -->
    <button @click="changeActive">활성화/비활성화</button>

    <h3>{{ message }}</h3>
  </div>
</template>
