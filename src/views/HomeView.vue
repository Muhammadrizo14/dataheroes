<template>
  <main class="list__card">
    <Filter @updateInfo="updateInfo" />

    <div class='df' style='gap: 30px'>
      <button @click="prevPage" :disabled="count === 1">
        назад
      </button>
      <p style='color: #fff'>{{count}}</p>
      <button @click="nextPage" :disabled='!info.info.next'>
        сдед
      </button>
    </div>

    <Card v-for="data in info.results" :info="data" :key="data.id" />
  </main>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios';
import Filter from '../components/Filter.vue';
import Card from '../components/Card.vue';

const info = ref({ results: [], info: {} });
const count = ref(1);

const nextPage = () => {
  count.value++;
  fetchCharacters()
};

const prevPage = () => {
  if (count.value > 1) {
    count.value--;
    fetchCharacters()
  }
};
const fetchCharacters = (params = {}) => {
  let url = 'https://rickandmortyapi.com/api/character/?page=' + count.value;

  const query = new URLSearchParams(params).toString();
  if (query) url += `&${query}`;

  axios
    .get(url)
    .then(response => {
      info.value = response.data;
    })
    .catch(error => {
      console.error('Error fetching characters:', error);
    });
};

onMounted(() => {
  fetchCharacters();
});

const updateInfo = (formData) => {
  const params = {};
  count.value = 1
  if (formData.name) params.name = formData.name;
  if (formData.status) params.status = formData.status;
  fetchCharacters(params);
};
</script>


<style scoped>
.list__card {
  padding: 40px 0;
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  background: rgb(39, 43, 51);
  min-height: 100vh;
}
</style>