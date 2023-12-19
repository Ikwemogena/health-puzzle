<template>
  <div class="card" @click="flipCard">
    <div v-if="!card.isFlipped" class="card-back rounded-md"></div>
    <div v-else class="card-front rounded-md transition-opacity" :style="{backgroundImage: `url(${card.image})`}"></div>
    <!-- <img :src="card.image"/> -->
  </div>
</template>

<script setup>
// defineProps({
//     value: String,
//     isFlipped: Boolean
// })
defineProps({
    card: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['flip']);
// console.log(props);

const flipCard = () => {
    console.log('flip card')
    emit('flip');
};
</script>

<style scoped>
.card {
  width: 200px;
  height: 200px;
  /* margin: 5px; */
  /* position: relative; */
  cursor: pointer;
}

.card-back {
  background-color: #ccc;
  width: 100%;
  height: 100%;
  /* position: absolute; */
  /* top: 0;
  left: 0; */
}

.card-front {
  width: 100%;
  height: 100%;
  /* background-image: url('/images/fruits.jpg'); */
    background-size: cover;

    /* background-color: #ccc; */

  /* position: absolute;
  top: 0;
  left: 0; */
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  font-size: 16px;
}
</style>
