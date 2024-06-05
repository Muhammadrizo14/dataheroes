<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const props = defineProps(['info'])

const {name, image,species, status, location, episode} = props.info
const episodeInfo = ref()

onMounted(()=> {
  let url = episode[0]
  axios
    .get(url)
    .then(response => {
      episodeInfo.value = response.data;
    })
    .catch(error => {
      console.error(error);
    });
})
</script>


<template>
  <div class='card'>
    <img :src='image' alt=''>
    <div class='card__info'>
      <div class='card__info-section'>
        <h2 class='card__info-section-name'>{{ name }}</h2>
        <span class='card__info-section-status'>
          <span class='card__info-section-status__icon'></span>
          {{ status }} - {{species}}
        </span>
      </div>
      <div class='card__info-section'>
        <p class='card__info-section-gray'>Last known location:</p>
        <h3>{{ location.name }}</h3>
      </div>
      <div class='card__info-section'>
        <p  class='card__info-section-gray'>First seen in:</p>
        <h3>{{episodeInfo?.name}} </h3>
      </div>
    </div>
  </div>
</template>


<style lang='scss' scoped>
.card {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
  &__info {
    flex: 3 1 0%;
    position: relative;
    padding: 0.75rem;
    color: rgb(255, 255, 255);
    display: flex;
    flex-direction: column;

    &-section {
      flex: 1 1 0%;
      display: flex;
      flex-direction: column;
      -webkit-box-pack: center;
      justify-content: center;
      &:first-child {
        -webkit-box-pack: start;
        justify-content: flex-start;
      }
      &:last-child {
        -webkit-box-pack: end;
        justify-content: flex-end;
      }

      &-name {
        font-size: 1.5rem;
      }

      &-gray {
        font-size: 16px;
        color: rgb(158, 158, 158);
      }

      &-status {
        font-size: 16px;
        font-weight: 500;
        display: flex;
        -webkit-box-align: center;
        align-items: center;
        text-transform: capitalize;
        &__icon {
          height: 0.5rem;
          width: 0.5rem;
          margin-right: 0.375rem;
          background: rgb(85, 204, 68);
          border-radius: 50%;
        }
      }
    }

  }
}
</style>