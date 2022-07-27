<template>
<div class="home"> 
  <h2> {{ appTitle }}</h2>
  <h3>{{ counterData.title }}: </h3>
  <div>
    <button @click="decreaseCounter(1)" class="btn">-</button>
    <span class="counter">{{ counterData.count }}</span>
    <button @click="increaseCounter(1)" class="btn">+</button>
  </div>

    <div class="edit">
      <h4>Edit counter title:</h4>
      <input v-model="counterData.title" type="text"/>
    </div>

    <p>This counter is {{ oddOrEven }}</p>

</div>
</template>

<script setup>
  import { reactive, computed, watch } from 'vue';

  // non-reactive
  const appTitle = 'My counter app';

  // reactive
  const counterData = reactive({
    count: 0,
    title: 'My title',
  })

  // Note that you can't watch a property of a reactive object that is nested
  // so used a getter to get it, 2nd param method
  watch(() => counterData.count, (newCount) => {
    if(newCount == 10) alert('Awwww yeah boi!')
  }) 

  const oddOrEven = computed(() => {
    if (counterData.count % 2 === 0) return 'even'
    return 'odd'
  })

  const increaseCounter = amount => {
    counterData.count += amount;
  }

  const decreaseCounter = amount => {
    counterData.count-= amount;
  }
</script>

<!-- Options api computed property 
export default {
  data() {
    return {
      count: 0
    }
  }
  computed: {
    myComputedProperty() {
      // perform logic based on data prop
      return 'my result';
    }
  },
  watch: {
    count(newCount, oldCount) {
      if newCount == 20 alert('awww yeah boi!')
    }
  }
}

-->

<style>
.home {
  text-align: center;
  padding: 20px;
}
.btn, .counter {
  font-size: 40px;
  margin: 10px;
}
.edit {
  margin-top: 60px;
}
</style>