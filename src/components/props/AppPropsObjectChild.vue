<script setup>
import { computed } from 'vue';

const props = defineProps({
  fruit: Object,
});

const imgSrc = computed(() => {
  return new URL(`../../assets/${props.fruit.id}.png`, import.meta.url).href;
});

const emits = defineEmits(['select-fruit', 'select-fruit-name']);

const select = () => {
  emits('select-fruit', props.fruit.id);
};

const onClick = () => {
  emits('select-fruit-name', props.fruit.name);
};
</script>

<template>
  <div class="div-fruit">
    <input
      type="checkbox"
      :id="fruit.id"
      :checked="fruit.checked"
      @change="select"
    />

    <label :for="fruit.id">
      <img :src="imgSrc" class="img-fruit" />
      <span @click="onClick">{{ fruit.name }}</span> ({{ fruit.price }}원,
      {{ fruit.origin }})
    </label>
  </div>
</template>

<style scoped>
.div-fruit {
  color: darkgray;
  margin-bottom: 5px;
  font-size: large;
}

.img-fruit {
  width: 20px;
  margin: 0 1px 0 5px;
}
</style>
