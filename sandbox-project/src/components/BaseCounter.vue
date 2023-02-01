<script>
export default {
  data: () => ({
    count: 10,
    counterTitle: "Counter Standard",
    incrementAmount: 8,
  }),
  computed: {
    displayTitle() {
      if (this.count > 20) {
        return "Conter Standard - Very Long";
      } else {
        return "Counter Standard";
      }
    },
    optimizedIncrementAmount() {
      return this.counterTitle.length * this.incrementAmount;
    },
  },
  methods: {
    incrementCount(newAmount, event) {
      console.log(newAmount);
      console.log(event);
      this.count += this.incrementAmount;
    },
  },
};
</script>

<template>
  <h1>{{ displayTitle }}</h1>
  <p :data-increment-by="incrementAmount">{{ count }}</p>
  <button @click="incrementCount">Increment Count</button>
  <h1>{{ incrementAmount }}</h1>
  <p>{{ optimizedIncrementAmount }}</p>
  <div>
    <label for="incrementAmount">Increment by:</label>
    <input type="number" v-model="incrementAmount" />
  </div>
</template>
