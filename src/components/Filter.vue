<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="formData.name" name="name" type="text" />
    <label for="status">Status:</label>
    <select v-model="formData.status" name="status" id="status">
      <option value="Alive">Alive</option>
      <option value="Dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button type="submit">
      Применить
    </button>
  </form>
</template>

<script setup>
import { reactive, defineEmits } from 'vue';

const formData = reactive({
  name: '',
  status: 'Alive'
});

const emit = defineEmits(['updateInfo']);

const handleSubmit = () => {
  emit('updateInfo', formData);
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  color: #fff;
}
</style>