<template>
  <div ref="wrapper" class="name-wrapper">
    <div v-for="(solution, index) in solutions" :key="index"
         :class="{ 'solution-item': true, 'active': index === activeIndex }"
         @click="setActive(index); saveDataToLocalStorage()">
      <p>{{ solution.name }}</p>
    </div>
  </div>

</template>

<script>
import solutions from '@/assets/data/solutions.json';

export default {
  data() {
    return {
      solutions: solutions,
      activeIndex: 1,
      dataField: solutions
    };
  },
  methods: {
    setActive(index) {
      console.log('setActive method called with index:', index);
      this.activeIndex = index;
      console.log('activeIndex after setting:', this.activeIndex);
      this.$emit('update-active-index', this.activeIndex);
      this.$emit('reset-data-id');
    },
    saveDataToLocalStorage() {
      const cellData = this.dataField[this.activeIndex].dataField.flat();
      localStorage.setItem('cellData', JSON.stringify(cellData));
    }
  },
  mounted() {
    console.log('activeIndex on mount:', this.activeIndex);
  }
};
</script>

<style scoped>
.name-wrapper {
  display: flex;
  flex-direction: column;
  width: fit-content;
}

.solution-item {
  cursor: pointer;
  padding: 5px;
  text-align: center;
  border: 1px solid black;
  background-color: #E54814;
  color: #EFEFEF;
  font-family: "Black Ops One", system-ui;
  font-size: 20px;
  font-weight: bold;
}

.solution-item.active {
  background-color: black;
}

p {
  margin: 0;
}
.solution-item:hover {
  background-color: black;
}

</style>
