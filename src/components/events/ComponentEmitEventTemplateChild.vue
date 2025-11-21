<script setup>
import { ref } from 'vue';

// 1-2. props로 받음
// 4-5. props로 받음
defineProps({
  color: String,
  isActive: Boolean,
});

const greet = ref('');
</script>

<!-- 
[템플릿에서 $emit]
- 인자 없음
- 검증 필요 없음
- 작은 컴포넌트 
-->

<template>
  <!-- 1-3. 부모 컴포넌트에게 받은 색상 적용 -->
  <div class="child" :style="{ backgroundColor: color }">
    <h3>Child 영역입니다</h3>

    <div class="div-btn">
      <!-- 4-6. 적용 -->
      <button @click="$emit('greetingEvent')" :disabled="isActive">
        인사해요
      </button>
    </div>

    <div class="div-btn">
      <input
        type="text"
        v-model="greet"
        @keyup.enter="$emit('greetingArgEvent', greet)"
      />

      <button @click="$emit('greetingArgEvent', greet)">
        인사해요(인자전달)
      </button>
      <br />

      <!-- 5-1. 토글하기 버튼 생성 -->
      <button @click="$emit('toggleEvent')">토글하기</button>
    </div>
  </div>
</template>

<style scoped>
.child {
  background-color: rgb(210, 236, 244);
  padding: 20px;
}
.div-btn {
  margin: 10px;
}
</style>
