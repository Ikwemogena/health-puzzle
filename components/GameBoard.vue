<template>
    <!-- {{ trials }} -->
    <div class="flex gap-3 justify-center items-center pb-2">
      <p>Score: {{ score }}</p>
    </div>
  <div class="grid grid-cols-6 gap-2">
    <!-- <Card
      v-for="(card, index) in cards"
      :key="index"
      :value="card.value"
      :isFlipped="card.isFlipped"
      @flip="handleCardFlip(index)"
    /> -->
    <Card
      v-for="(card, index) in cards"
      :key="index"
      :card="card"
      @flip="handleCardFlip(index)"
    />
  </div>
</template>

<script setup>
const cards = ref([
  { value: 'Exercise', isFlipped: false, image: '/images/exercise.jpg' },
  { value: 'Healthy Diet', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
  { value: 'Exercise', isFlipped: false, image: '/images/exercise.jpg' },
    { value: 'Healthy Diet', isFlipped: false, image: '/images/fruits.jpg' },
  { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Exercise', isFlipped: false, image: '/images/exercise.jpg' },
    { value: 'Exercise', isFlipped: false, image: '/images/exercise.jpg' },
  { value: 'Healthy Diet', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
    { value: 'Hydration', isFlipped: false, image: '/images/fruits.jpg' },
  { value: 'Exercise', isFlipped: false, image: '/images/exercise.jpg' },
  
  // Add more health-related habits
]);

// const cards = ref(generate());
const score = ref(0);

const selectedCards = ref([]);

const trials = ref(3);

const handleCardFlip = (index) => {
    // console.log('card flipped')
    const flippedCard = cards.value[index];
    // const flippedCard = cards.value.find((card) => card.value === value);
    console.log(flippedCard.value)

    if (!flippedCard.isFlipped) {
    flippedCard.isFlipped = true;
    selectedCards.value.push(flippedCard);

    if (selectedCards.value.length === 2) {
      checkMatch();
    }
  }
//   if (flippedCard.isFlipped === false) {
//     flippedCard.isFlipped = true
//     selectedCards.value.push(flippedCard);

//     if (selectedCards.value.length === 2) {
//       checkMatch();
//     }
//   }
};

const checkMatch = () => {
    console.log(selectedCards.value)

    if (
    selectedCards.value[0].value === selectedCards.value[1].value
  ) {
    // Match found, perform actions
    // For example, remove the matched cards
    // selectedCards.value.forEach((card) => {
    //   card.isFlipped = false;
        // });
    setTimeout(() => {
    //   selectedCards.value.forEach((card) => {
    //       card.isFlipped = false;
    //     // console.log(card)
    //   });
      selectedCards.value = [];
    score.value += 10;
        // selectedCards.value = [];
    //   score.value -= 5;
    }, 1000);
    //     selectedCards.value = [];
    // score.value += 10;
  } else {
    // No match, flip the cards back
    setTimeout(() => {
      selectedCards.value.forEach((card) => {
          card.isFlipped = false;
        // console.log(card)
      });
        selectedCards.value = [];
        score.value -= 5;
      trials.value -= 1;
    }, 1000);
  }
//   if (
            // selectedCards.value[0].value === selectedCards.value[1].value 
        // &&
//     selectedCards.value[0] !== selectedCards.value[1]
//   ) {
//     // Match found, perform actions
//     // For example, remove the matched cards
//     selectedCards.value = [];
//   } else {
//     // No match, flip the cards back
//     setTimeout(() => {
//       selectedCards.value.forEach((card) => {
//         card.isFlipped = false;
//       });
//       selectedCards.value = [];
//     }, 1000);
//   }
};
onMounted(() => {
  shuffleCards();
});

const shuffleCards = () => {
  cards.value = shuffleArray(cards.value);
};

const shuffleArray = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
};
</script>

<style scoped>
.game-board {
  display: flex;
  flex-wrap: wrap;
  max-width: 600px;
  margin: 0 auto;
}
</style>
