<script setup>
import { ref } from 'vue';

// 6-3. 부모컴포넌트에게서 객체 타입으로 받음
defineProps({
  userInfo: Object,
});

const greet = ref('');

// 2-1. 이름 입력 객체 생성
const name = ref('');

const emit = defineEmits({
  greetingEvent: null,

  greetingArgEvent: (payload) => {
    if (payload.trim().length != 0) {
      return true;
    } else {
      console.warn('인사말 입력 !!!');
      return false;
    }
  },

  // 2-3. 이름 입력 검증 후, 부모 컴퍼넌트로 전송
  welcomeEvent: (payload) => {
    if (payload.trim().length != 0) {
      return true;
    } else {
      console.warn('이름을 입력해주세요');
      return false;
    }
  },
});
</script>

<!--
[script의 defineEmits]
- 안전하고, 명확함
- “인자 전달 + 검증이 필요한 경우” 꼭 사용
-->

<template>
  <div class="child">
    <h2>Child Component</h2>

    <div class="div-btn">
      <button @click="emit('greetingEvent')">인자 없는 인사하기</button>
    </div>

    <div>
      <!-- 2-2. 이름 입력 -->
      <input v-model="name" placeholder="이름 입력" />
      <button @click="emit('welcomeEvent', name)">이름 입력</button>
      <br />

      <input v-model="greet" placeholder="인사말 입력" />

      <button @click="emit('greetingArgEvent', greet)">
        인자 포함 인사하기
      </button>
    </div>
  </div>
  <div>
    <!-- 6-4. 출력 -->
    <p>이름 : {{ userInfo.name }}</p>
    <p>나이 : {{ userInfo.age }}</p>
    <p>직업 : {{ userInfo.major }}</p>
  </div>
</template>

<style scoped>
.child {
  background-color: rgb(244, 210, 236);
  padding: 20px;
}
.div-btn {
  margin: 10px;
}
</style>
