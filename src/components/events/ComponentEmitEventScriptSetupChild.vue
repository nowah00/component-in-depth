<script setup>
import { ref } from 'vue';

const greet = ref('');

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
      <input
        v-model="greet"
        placeholder="인사말 입력"
        @keyup.enter="emit('greetingArgEvent', greet)"
      />

      <button @click="emit('greetingArgEvent', greet)">
        인자 포함 인사하기
      </button>
    </div>
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
