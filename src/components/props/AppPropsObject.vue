<script setup>
import { computed, reactive } from 'vue';
import AppPropsObjectChild from './AppPropsObjectChild.vue';
import AppPropsObjectChildDestructure from './AppPropsObjectChildDestructure.vue';

const props = defineProps({
  viewTitle: String,
});

const fruits = reactive([
  { id: 'f1', name: '사과', checked: true, price: 1200, origin: '한국' },
  { id: 'f2', name: '파인애플', checked: false, price: 1500, origin: '미국' },
  { id: 'f3', name: '포도', checked: false, price: 1700, origin: '한국' },
  { id: 'f4', name: '딸기', checked: true, price: 1900, origin: '미국' },
  { id: 'f5', name: '아보카도', checked: false, price: 2100, origin: '한국' },
  { id: 'f6', name: '메론', checked: false, price: 2300, origin: '미국' },
  { id: 'f7', name: '수박', checked: true, price: 2500, origin: '한국' },
]);

const selectFruit = (id) => {
  const fru = fruits.find((fruit) => fruit.id === id);
  if (fru) {
    fru.checked = !fru.checked;
  }
};

const selectFruitName = (name) => {
  alert(`과일의 이름 : ${name}`);
};

const checkedFruitCount = computed(
  () => fruits.filter((f) => f.checked).length
);
</script>

<template>
  <div>
    <h2>{{ props.viewTitle }}</h2>

    <div class="fruits">
      <h3>일반 props 객체로 사용</h3>

      <AppPropsObjectChild
        v-for="fruit in fruits"
        :key="fruit.id"
        :fruit="fruit"
        @select-fruit="selectFruit"
        @select-fruit-name="selectFruitName"
      />

      <hr />

      <h3>props 구조 분해 할당 버전</h3>
      <AppPropsObjectChildDestructure
        v-for="fruit in fruits"
        :key="fruit.id"
        :fruit="fruit"
        @select-fruit="selectFruit"
        @select-fruit-name="selectFruitName"
      />
    </div>
    <p>선택된 과일 개수: {{ checkedFruitCount }}</p>
  </div>
</template>

<style scoped>
.fruits {
  display: inline-block;
  width: 250px;
  text-align: left;
}
</style>
