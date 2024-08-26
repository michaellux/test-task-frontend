<script setup>
import HolderThingItems from '@/components/HolderThingItems.vue';
import ThingItem from '@/components/ThingItem.vue';

import { ref } from 'vue';
import userThingsData from '@data/user-things.json';
import chooseThingsData from '@data/choose-things.json';

const userThings = ref(userThingsData);
const chooseThings = ref(chooseThingsData);

const selectedUserThings = ref([]);
const chooseThing = ref({});

const addToSelectedUserThings = (id) => {
  const targetItem = userThings.value.find((item) => item.id === id);
  if (selectedUserThings.value.length < 6 || 
  (selectedUserThings.value.length === 6 && targetItem.isSelected === true)) {
    targetItem.isSelected = !targetItem.isSelected;
    selectedUserThings.value = userThings.value.filter((item) => item.isSelected === true);
  }
}

const addToSelectedChooseThings = (id) => {
  chooseThing.value = chooseThings.value.find((item) => item.id === id);
}
</script>

<template>
  <header>
   
  </header>

  <main>
    <div class="container">
      <div class="left">
        <HolderThingItems :items="selectedUserThings"/>
        <HolderThingItems :items="userThings" @toggle-select="addToSelectedUserThings"/>
      </div>
      <div class="right">
        <ThingItem :item="chooseThing"/>
        <HolderThingItems :items="chooseThings" @toggle-select="addToSelectedChooseThings"/>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
  display: flex;
  gap: 10vw;
}
.left, .right {
  display: flex;
  flex-direction: column;
  gap: 20px;
  width: 50%;
}
</style>
